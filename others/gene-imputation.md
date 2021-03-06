# 分型补全

## 方案设计

1. 比较BEAGLE、GeneImp软件（后续可测试Impute2、Minimac3等）对当前芯片数据的适用性与准确度评估；
2. 搭建芯片数据的补全流程；

## GeneImp
### dependencies
* gfortran
* curl-config
* xml2-config
* libmysqlclient

```
sudo apt-get install gfortran libcurl4-gnutls-dev libxml2-dev libmysqlclient-dev
```

### 数据要求
- 参考集样本数大于200
- 二等位
- vcf文件必须包含PL列（芯片数据转化时参考confidence信息）
- vcf必须用bgzip压缩，用tabix创建index

### 运行命令
```
docker run --name imputation --mount type=bind,source=/home/sumin/workdir/GenotypeImputation/data,target=/data imputation Rscript /data/test.R
```
### 参数测试
| | 准确率 | 时间 |
| :---: | :---: | :---: |
| kl=10| 94.89% |224min|
| kl=20(default) | 93.68% | 59min  |
| kl=50 | 90.22% | 35min |

| | 准确率 | 时间 |
| :---: | :---: | :---: |
| haps=20 | 92.59% | 28min |
| haps=100 | 93.57% | 41min |
| haps=200(default) | 93.68% | 59min |
| haps=500 | 93.71% | 122min |
| haps=1000 | 93.72% | 260min |


| | 准确率 | 时间 |
| :---: | :---: | :---: |
| flank=0.1 | 94.64% | 124min |
| flank=0.5(default) | 93.73% | 59min |
| flank=0.8 | 93.07% | 48min |



## BEAGLE
### 数据要求
- ID列不为空
- vcf已排好序
- 1Mb内有marker

### 运行命令
```
java -jar bref.08Jun17.d8b.jar ref.vcf.gz
java -jar beagle.08Jun17.d8b.jar ref=ref.bref gt=target.vcf.gz out=prefix
```
### 参数测试
| | 准确率 | 时间 |
| :---: | :---: | :---: |
| markers=10M| 90.11% | 18min |
| markers=50M(default) | 90.40% | 22min |
| markers=100M | 90.36% | 25min |

| | 准确率 | 时间 |
| :---: | :---: | :---: |
| iteration=5(default) | 90.40% | 22min|
| iteration=20 | 90.42% | 47min |
| iteration=100 | 90.38% | 180min |

| | 准确率 | 时间 |
| :---: | :---: | :---: |
| err=0.00001| 90.11% | 18min |
| err=0.0001(default) | 90.40% | 22min |
| err=0.001 | 90.44% | 22min |
| err=0.01 | 90.21% | 22min |


## 结果比较
| | GeneImp | BEAGLE |
| :---: | :---: | :---: |
| 运行时间 | 59min | 28min |
| 准确率 | 93% | 90% |
| 与芯片原始数据一致率 | 97.79% | 93.55% |
|GeneImp与BEAGLE一致率|97.88%|97.88%|
| 资源消耗|400G|8G|

- conversion type对位点推断准确性影响

初始：MonoHighResolution：843； PolyHighResolution: 565; NoMinorHom: 440

|<0.6 | GeneImp | BEAGLE |
| :---: | :---: | :---: |
|PolyHighResolution|36|97|
|MonoHighResolution|1|1|

|<0.5 | GeneImp | BEAGLE |
| :---: | :---: | :---: |
|PolyHighResolution|8|30|
|MonoHighResolution|1|1|
