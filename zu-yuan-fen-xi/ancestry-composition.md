# 民族成分

参考资料： [https://www.23andme.com/ancestry-composition-guide/](https://www.23andme.com/ancestry-composition-guide/)

## 数据来源

### 数据库

|  | 23andMe | 乐土 |
| :---: | :---: | :---: |
| HGDP-CEPH | √ | √ |
| 1000Genomes | √ | √ |
| HapMap | √ | × |
| iControlDB | √ | × |
| PGG | × | × |
| others | √ | × |

* PGG.Population:包含来自107个国家356个民族的7122个人
* HapMap ：2016-06-16 宣布有安全漏洞，NCBI停止维护，1000Genomes提供更多的信息
* iControlDB是Illumina的一个样本数据库

### 训练集规模

|  | 民族 | 人数 |
| :---: | :---: | :---: |
| 23andMe | 31 | 10,418 |
| 乐土 | 57 | 1,730 |

### 数据过滤

|  | 23andMe | 乐土 |
| :---: | :---: | :---: |
| 样本 | 1.挑选有4个祖父母在同一个地区（除美国、加拿大、澳大利亚等移民国家）的人；2. 去除亲缘关系较近的人；3. 去除统计结果和填写的民族不一致的人 | 暂无 |
| 民族 | 1.挑选500年前就已存在的民族；2. 历史上没有移民 | 人工判断，关系较近或移民混合去除 |
| 偏好 | 主要为欧洲人 | 亚洲人 |

## 分析步骤

### 乐土

1. 从1000Genomes和HGDP数据库下载，人工进行民族的挑选，构建训练集；
2. 根据位点频率，挑选差异显著的位点用于下一步的分析；
3. 随机森林确定各个民族的成分；

### 23andMe

1. Phasing:  Finch（BEAGLE的23andMe版）确定哪些marker组成一个染色体
2. Window Classfication: 100个Marker做一个窗口，SVM判断每个窗口的民族来源；
3. Smooth： Hidden Markov Models进行拟合（unusual assignment；switch error）
4. Re-calibration: 矫正训练集所造成的偏好
5. Aggregation & Reporting: 各个窗口结果加和

![](/assets/Chromosome_Painting.png)

>Using Close Family Members, you will get a very high-quality chromosome pharing result

## Ancestry Timeline (2017 23andMe)
> https://customercare.23andme.com/hc/en-us/articles/115004342967


![](/assets/Timeline.png)

假设前提：  each ancestry was inherited from a single ancestor. It's not true for highly admixed populations.
结果

分析原理：The Ancestry Timeline feature analyzes the pattern of ancestry in your genome by looking at both the number and size of segments that came from a particular ancestry as well as their distribution across your chromosomes. 

颇受争议：
1. https://dna-explained.com/2017/01/17/calling-hogwash-on-23andmes-ancestry-timeline/
2. http://www.rootsandrecombinantdna.com/2017/01/new-23andme-ancestry-timeline-tool.html




