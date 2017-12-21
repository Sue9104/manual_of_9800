# 分型补全

## 方案设计

1. 比较BEAGLE、GeneImp软件（后续可测试Impute2、Minimac3等）对当前芯片数据的适用性与准确度评估；
2. 搭建芯片数据的补全流程；

## 数据处理
### 芯片数据处理
- 芯片数据格式转换为vcf,PL列参考confidence
- 用bgzip压缩，并用tabix创建index

### vcf位点过滤
- 过滤多等位的位点

## GeneImp

### dependencies

* gfortran
* curl-config
* xml2-config
* libmysqlclient

```
sudo apt-get install gfortran libcurl4-gnutls-dev libxml2-dev libmysqlclient-dev
```



