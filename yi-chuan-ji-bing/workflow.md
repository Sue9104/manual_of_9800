# 流程

## 位点过滤
1. 对于本批次杂合率 > 0.05的位点进行删除
2. 对芯片参考数据中Minor Allele Frequency > 0.01进行过滤
3. 疾病的ClinVar ClinicalSignificance不是Pathogenic，Likely pathogenic，PATHOGENIC

## 结果判断
统计基因型匹配Alt的次数N

### 常染色体显性
- 可能致病：$$N \ge 1$$
- 正常

### 常染色体隐性
- 可能致病：$$N \ge 2$$
- 携带：$$N \ge 1$$
- 正常

### X连锁显性
- 可能致病：$$N \ge 1$$
- 正常

### X连锁隐性
- 男
 - 可能致病：$$N \ge 1$$
 - 正常

- 女
- 可能致病：$$N \ge 2$$
- 携带：$$N \ge 1$$
- 正常

### 线粒体
- 可能致病：$$N \ge 1$$
- 正常

### 尚不明确
- 未知：$$N \gt 1$$



