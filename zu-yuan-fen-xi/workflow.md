# 分析流程

## Requirements
- perl 
 - Modern::Perl
 - Data::Dumper
 - IO::All
 - Cwd
 - FindBin
 - Getopt::Long::Descriptive
 - File::Basename
 - JSON;
 - MCE::Loop
 - DBI

 
- python
 - numpy
 - sklearn

### 主流程

```
perl ancestry_analysis_csv.pl                                                                                                                                            

Usage:
Ancestry Analysis [-ciov] [long options...] <some-arg>
    -c STR --csv STR     芯片样本的csv文件
    -i STR --step STR    步骤参数：
        0： 结果分析
        1： 分析结果更新至数据库

    -o STR --outdir STR  结果输出目录
```

## Y单倍群

```
perl bin/generate_Y_group.pl                    

Usage:
Y haplogroup [-bjov] [long options...] <some-arg>
    -j STR --json STR  样本分型的json文件
    -o STR --out STR   Y单倍体群结果

    -b STR --base STR  Y tree位点基因型信息
    -t STR --tree STR  Y tree结构的json文件
```

## MT单倍群

```
perl bin/generate_MT_group.pl                   

Usage:
MT haplogroup [-bjotv] [long options...] <some-arg>
    -j STR --json STR 样本分型的json文件
    -o STR --out STR MT单倍体群结果
    -b STR --base STR MT tree位点基因型信息
    -t STR --tree STR MT tree结构的json文件
```

## 民族成分

```
python bin/random_forest.py <train.input> <population.txt> <test.input> <test.region.out>

Usage:
    train.input 训练集样本基因型结果
    population.txt　训练集样本的民族信息
    test.input　样本的基因型结果
    test.region.out　样本的民族成分分析结果
```

## 分析结果上传数据库

```
 perl bin/create_ancestry_db.pl               

 Usage:
Create or Update Ancestry Database [-abcmnrsvYy] [long options...] <some-arg>
    -r STR --region STR  民族成分结果 
    -y STR -Y STR         Y单倍体群结果
    -m STR --MT STR       MT单倍体群结果
    -s INT --step INT     步骤说明：
        0: 数据库初始化
        1：分析结果上传数据库
```

## 结果目录

```
├── *.ancestry.csv             　　#样本在祖源分析位点的基因型信息
├── A01_10003836.ancestry.json    #样本在祖源分析位点的基因型信息的json文件
├── A01_10003836.region.out    　　#样本的民族成分结果
├── A01_10003836.MT.out　　　　　　　#样本的MT单倍体群结果
├── A01_10003836.Y.out 　　　　　　　#样本的Y单倍体群结果
└── RF                            #民族成分分析的中间文件
    ├── A01_10003836.test.input
    └── A01_10003836.train.input
```



