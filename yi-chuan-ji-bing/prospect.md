# 展望

## 数据库
### 目前进展
1. 下载基因每个位点的遗传信息，需爬虫；
2. 通过ClinVar的rs信息，确定基因位点对应的表型MIM;
3. 对表型进行过滤
 - phenotype prefix, 保留‘Number Sign’；
 - phenotype mapping key，保留‘3’； 
 - phenotype inheritance，过滤掉‘digenic recessive’,‘isolated cases’,'isolated cases, somatic mutation','somatic mosaicism','somatic mutation', 以及包含‘multifactorial’的条目；此列‘空白’的条目保留；
 - Phenotype full name，过滤掉包含‘{}’‘[]’‘?’的条目；
4. 位点与目前芯片位点取交集；
5. clinical significance过滤，只保留包括‘pathogenic’、‘likely pathogenic’和‘空白’
6. 删除phenotype包含‘somatic’的条目
7. variant phenotype MIM空白的进行人工补充和修正(在clinVar中未找到)
8. 过滤表型没有遗传模式


## 分析流程
- 重新搭建单基因病数据库
- 考虑位点个数以及位点遗传模式，重写流程

## 展示
- 总体结果图

## 报告
- 新版报告实现