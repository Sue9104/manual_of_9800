#　数据分型

## 过滤条件
### 样本过滤
- DQC ≥ 0.92
- 样本CallRate ≥ 97%
### 探针过滤
- 过滤掉ConversionType为CallRateBelowThreshold
- 多个探针对应同一rs号，按PolyHighResolution, NoMinorHom, MonoHighResolution，Hemizygous，OTV的优先级和检出率选择最终保留的探针
- 探针CallRate ≥ 96%
- 单基因病位点杂合率 > 5%





