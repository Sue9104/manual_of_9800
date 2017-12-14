# 相关介绍

## 数据库

### PharmGKB

PharmGKB (药物遗传学和药物基因组学知识库) 由美国国立卫生研究院（NIH）创建，收集了史上最完整的与药物基因组相关的基因型和表型信息，并将这些信息系统地归类。
![](/assets/pharmgkb.png)


截止2017-10-25，共收录的信息统计如下：
![](/pngs/pharmgkb_stat.png)

截止2017-10-25，pharmGKB手工注释的信息统计如下：
![](/pngs/pharmgkb.sources.png)

- 网址: [https://www.pharmgkb.org](https://www.pharmgkb.org)
- 文献: [https://www.ncbi.nlm.nih.gov/pubmed/22992668](https://www.ncbi.nlm.nih.gov/pubmed/22992668)
- 下载：[https://api.pharmgkb.org/](https://api.pharmgkb.org/)

#### 专业词汇
##### PGx
 
PharmGKB annotates drug labels containing pharmacogenetic information approved by FDA, EMA, PMDA, HCSC. PharmGKB annotations provide a brief summary of the PGx in the label, an excerpt from the label.

- **Testing required**: PharmGKB considers labels that state the variant is an indication for the drug, as implying a test requirement.

- **Testing recommended**: The label states or implies that some sort of gene, protein or chromosomal testing, including genetic testing, functional protein assays, cytogenetic studies, etc., is recommended before using this drug. 

- **Actionable PGx**:The label may mention contraindication of the drug in a particular subset of patients but does not require or recommend gene, protein or chromosomal testing.

- **Informative PGx**:The label mentions a gene or protein is involved in the metabolism or pharmacodynamics of the drug, but there is no information to suggest that variation in these genes/proteins leads to different response.

##### 证据等级
![](/assets/level_of_evidence.png)

- **Level 1A**: Annotation for a variant-drug combination in a CPIC or medical society-endorsed PGx guideline, or implemented at a PGRN site or in another major health system.

- **Level 1B**:Annotation for a variant-drug combination where the preponderance of evidence shows an association. The association must be replicated in more than one cohort with significant p-values, and preferably will have a strong effect size.

- **Level 2A**: Annotation for a variant-drug combination that qualifies for level 2B where the variant is within a VIP (Very Important Pharmacogene) as defined by PharmGKB. The variants in level 2A are in known pharmacogenes, so functional significance is more likely.

- **Level 2B**: Annotation for a variant-drug combination with moderate evidence of an association. The association must be replicated but there may be some studies that do not show statistical significance, and/or the effect size may be small.

- **Level 3**: Annotation for a variant-drug combination based on a single significant (not yet replicated) study or annotation for a variant-drug combination evaluated in multiple studies but lacking clear evidence of an association.

- **Level 4**: Annotation based on a case report, non-significant study or in vitro, molecular or functional assay evidence only.

### 芯片pharmGKB注释结果对比

| 证据等级 | Illumina | Affy |
| -- | -- | -- |
| 1A | 29 | 21 |
| 1B | 15 | 12 |
| 2A | 66 | 46 |
| 2B | 80 | 49 |
| 3 | 1863 | 788 |
| 4 | 214 | 124 |
| 总计 | 2267 | 1040 |

### 国内综合型数据库

涵盖药物研发（药物注册以及转让、专利信息、研发阶段）、生产检验（药品标准、参比制剂）、合理用药（药品说明书、医保目录、药物相互作用）、市场信息（政策法规、售价、上市信息）以及化学结构等一系列过程。
- 药智： [https://db.yaozh.com/](https://db.yaozh.com/)
- Insight：[http://db.dxy.cn/v5/home](http://db.dxy.cn/v5/home)


## 分析原理

### 数据库过滤
1. 过滤掉证据等级为4的位点；
2. **to be continued**

### 优选等级判定

- 根据一种药物的不同等级的毒性和有效性个数，确定x、y、z

| 个数 | 有效性等级 | 毒性等级 |
| -- | -- | -- |
| x | 好 | 小 |
| y | 中间等级 | 中间等级 |
| z | 差 | 大 |

- 根据x、y、z，分别进行有效性(a)和毒性(b)的评分

|  | 有效性(a) | 毒性(b) |
| -- | -- | -- |
| x=y=z=0 | 0 | 0 |
| x >= y+z && x!=z | 10 | 5 |
| x+y < z | 2 | 1 |
| x+y >=z | 8 | 4 |

- 根据有效性和毒性的评分，判定优选等级L

L= floor( (a + b) )/4 + 2


## 行业动态

### 23andMe

共12项

参考网址： https://www.23andme.com/en-gb/health/reports

### wegene

共11项

参考网址：https://www.wegene.com/demo/female/report/detail/1481

### 23魔方

6大类，共57种。

参考网址：https://www.23mofang.com/sample/drug
