# 结果数据库

## 分析结果上传以及更新
### 数据上传 
- 导入数据库

```
mongoimport -h 192.168.1.205 --port 27019 -d Annotation -c probesets --type=csv --headerline {}.csv
```

- 数据库样品信息删除
```
mongo mongodb://192.168.1.205:27019/Annotation <<< 'db.probesets.deleteMany({ "Sample ID": "A02_10002781" })'
```

### 系统更新
```
cd SNParray/SNParray
node bin/report-upgrade.js -i A01 -S 123:1 -S 1234:1 -E 123
```

参数解析：
- -i 样品的芯片编号
- -S 风险修改（针对健康风险），高风险2，中风险1，低风险0　
- -E 表型删除

### 报告生成
```
yarn start
yarn global add serve
serve -s build
```

## 展望
- 数据库结构调整
- 定期备份的docker实现
