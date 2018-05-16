# 9800流程操作

## 数据上传
下机数据（CEL文件）路径上传至 /data2/cifs/Axiom/Data/,  并按日期进行命名

## 数据处理

```
genotyping from cel to csv
USAGE:
    snpr-base-calling [OPTIONS] <DATA> <OUT> --para <PARA> --plateid <PLATE>
FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information
OPTIONS:
    -d, --dashqc <DQC>       Sets thresold for sample dashqc [default: 0.92]
    -t, --hetratio <HR>      Sets thresold for monogenic site hetratio [default: 0.05]
    -a, --para <PARA>        Sets environment path for apt-tools and annotation db
    -l, --plateid <PLATE>    Sets plateid
    -p, --probecr <CR>       Sets thresold for site callratio [default: 96]
    -c, --samplecr <CR>      Sets thresold for sample callratio [default: 97]
    -s, --step <STEP>
            1, qc
            2, pre-calling
            3, calling
            4, classification
            5, otv-caller
            6, merge
            7, filt
            8, format [default: 1,2,3,4,5,6,7,8]
ARGS:
    <DATA>    Sets cel file directory
    <OUT>     Sets output genotyping directory
```

代码路径： **git@git.clgene.com:snpr/snpr.git （snpr-calling）**

命令举例： **snpr-base-calling /data2/cifs/Axiom/Data/20180506/ 20180506 --para ~/workdir/snpr/snpr-calling/assets --plateid 20180506**

结果实例：
**/home/sumin/workdir/test/affy_data_analysis_20180115/20180506**


## 药物反应
```
Drug Reaction Pipeline [-dgopsuv] [long options...] <some-arg>
	-s STR --step STR      0: database initialize; 1: drug_analysis; 2:
	                       upload results to database
	                     
	-g STR --genotype STR  genotype directory or file
	-d STR --gender STR    sample genotype file
	                     
	-p STR --para STR      share dir default is
	                       /home/sumin/perl5/perlbrew/perls/perl-5.24.1/lib/site_perl/5.24.1/auto/share/dist/Drug-Reaction
	-u STR --db_url STR    drug reaction database url default is
	                       postgres://postgres:123456@192.168.1.205:5439/pharmgkb
	-o STR --outdir STR    output directory default is
	                       drug-reaction_results
```
代码路径： **git@git.clgene.com:snpr/snpr.git （perl-drug-reaction）**

数据库以及api: /home/sumin/workdir/SNParray/pharmgkb_api

命令举例： **drug-reaction -s 1,2 -g filtered  -d ../../20th_20180506_gender.csv  -o drug-reaction-result**

结果实例：/home/sumin/workdir/test/affy_data_analysis_20180115/20180506/format/drug-reaction-result

## 祖源分析 (分样品)
```
Ancestry Analysis [-ciov] [long options...] <some-arg>
	-c STR --csv STR     sample genotype csv file
	-i STR --step STR    0 for generate result, 1 for result and addto db
	                   
	-o STR --outdir STR  output dirname
	                   
	-v --verbose         print extra stuff
	--help               print usage message and exit

```
代码路径： **git@git.clgene.com:snpr/snpr.git （snpr-calling）**

数据库以及api: /home/sumin/workdir/SNParray/ancestry_api/

命令举例： **perl ancestry_analysis_csv.pl  -c ~/workdir/test/affy_data_analysis_20180115/20170506/format/filtered/20180506-A02_10007946.csv -i 1 -o 20180506/20180506-A02_10007946**

结果实例：/home/sumin/workdir/SNParray/ancestry/20180506/20180506-A02_10007946


## 基因分型导入数据库
```
mongoimport -h 192.168.1.205 --port 27019 -d Annotation -c probesets --type=csv --headerline 20th_used/20180506-A01_10021098.csv
```

## 数据更新
```
cd SNParray/SNParray
node bin/report-upgrade.js -i 样本的芯片编号
```
- 如需进行健康风险的修改 node bin/report-upgrade.js -i 样本的芯片编号 -S 疾病编号:1 
- 如需进行单基因病的删除 node bin/report-upgrade.js -i 样本的芯片编号 -E 疾病编号

命令举例：
```
node bin/report-upgrade.js -i B04_10021091 -S 9:1 -S 141:1 -S 249:1 -E 902 -E 108 -E 1654
```

## 生成报告
```
snpr-gen-pdf --encrypt 1 --sample 样本对应的芯片编号 --order_id 样本编号 --name 姓名 -o 结果目录 -u http://192.168.1.205:8083 --compress --product 检测产品编号
```

命令举例： 
```snpr-gen-pdf --encrypt 1 --sample A01_10021098 --order_id 10021098 --name '郭臧明' -o 20180506/CL01001 -u http://192.168.1.205:8083 --compress --product CL01001```

## 文件上传云盘
上传PDF文件到云盘https://oc.git.clgene.com/index.php， Bioinformatics -> Reports -> 产品编号 -> 日期