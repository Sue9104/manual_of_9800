# workflow
> Illumina GSA分型目前只提供Windows版本，并没有实现自动化

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

- rust
 - xsv

## 使用方法
```
perl ~/workdir/SNParray/data_processing_9800/run.pl

必选参数：
	-i STR --indir STR   下机CEL文件路径
	-o STR --outdir STR  结果输出路径
可选参数：	                   
	-p STR --para STR    分析用的参数文件
	-s STR --step STR    选择步骤，默认全选
				1：样本质控QC
				2：初步分型
				3：OTV Caller
				4: 探针过滤和选择
				5：样本分型和格式化输出
```

## 结果目录
```
├── cel_list1.txt #下机CEL文件列表
├── cel_list2.txt #样本DQC过滤后合格的CEL文件列表
├── cel_list3.txt #样本CallRate过滤后合格的CEL文件列表

├── QC #质控结果
	├── apt-geno-qc.txt
	├── AxiomGT1.calls.txt
	├── AxiomGT1.confidences.txt
	├── AxiomGT1.report.txt

├── AxiomGT1.calls.txt #初次分型结果
├── AxiomGT1.confidences.txt
├── AxiomGT1.report.txt
├── AxiomGT1.snp-posteriors.txt
├── AxiomGT1.summary.txt
├── Ps.performance.txt

├── raw_data #初次分型对应的样本数据
├── raw.txt

├── *.ps #各种ConversionType对应的探针列表

├── OTV_Caller #OTV分型结果

├── cmd.sh #运行命令
├── data #最终结果
	├──final 最终过滤后的样本结果
	├──used  分析中用到位点的样本结果	
├── final
	├── sample.callrate.txt #样本检出率以及杂合率的最终统计结果
	├── probe.callrate.txt  #探针检出率以及ConversionType的最终统计结果

```