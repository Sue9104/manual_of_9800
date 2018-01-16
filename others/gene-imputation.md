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
| kl=10|||
| kl=20 | |  |
| kl=50 | 90.22% | 35min |
| haps=100 | % | min |
| haps=200 | % | min |
| haps=500 | % | min |
| flank=10 | % | min |
| flank=50 | % | min |
| flank=100 | % | min |



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
| markers=50M | 90.40% | 22min |
| markers=100M | 90.36% | 25min |

| | 准确率 | 时间 |
| :---: | :---: | :---: |
| iteration=5 | 90.40% | 22min|
| iteration=20 | 90.42% | 47min |
| iteration=100 | % | min |

## 结果比较
| | GeneImp | BEAGLE |
| :---: | :---: | :---: |
| 运行时间 | 32min | 28min |
| 准确率 | 93% | 90% |
| 资源消耗|400G|8G|
