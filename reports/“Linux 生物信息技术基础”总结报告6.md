# “Linux 生物信息技术基础”总结报告 6

> 组：G04<br/>次：6<br/>组长：高大可<br/>讨论记录：邓昆月<br/>参与人员：高大可、邓昆月、唐明川、吴航锐<br/>上课时地：2023 年 4 月 3 日，15:10-17:00，35 楼 B104<br/>讨论时地：2023 年 4 月 9 日，13:00-15:00，35 楼 B107A

# 上课内容

## vim 文本编辑器

vim 快捷键：

三个模式：命令模式、输入模式、底线命令模式

### 输入模式

输入模式切换：`i``+Enter` 进入，`Esc` 退出

左下角会显示 `--INSERT--` 状态

### 命令模式

光标切换：`上下左右键/hjkl`

切换多行：`数字键+方向键`

切换到特定行：`数字+gg`

绝对行首和绝对行尾：`0`, `$`

切换到下一个单词第一个字符：w

切换到上一个单词第一个字符：b

复制：`yy`, 多行复制 `2yy`

粘贴：`p`, 粘贴到光标下

选取特定区域复制、粘贴：在选取开始位置 `v` 进入 `--VISUAL--`，移动后高光部分为选区的部分，可进行 `yy`、`dd` 等操作

删除：`d`, 多行操作与复制相同

删除某一行到末尾（例如第三行）：3，g d

插入分段：`o`

合并两行：`J`

撤销和重做：`u`, `Ctrl+R`

搜索：`/<search content>`, 搜索光标以下内容，`<search content>` 为搜索内容，`n` 正向搜索，`N` 反向

搜索：`?<search content>`, 搜索光标以上内容，`<search content>` 为搜索内容，`n` 正向搜索，`N` 反向

因为某些特殊原因造成操作中断，会生成一个隐藏文件，删除该隐藏文件的方法：

### 底线命令模式

在命令模式下输入 `:` 进入底线命令模式

`:w`：写入

`:wq`：写入并退出

`:q!`：强制退出不保存

![](static/Mw25b0uq7o1LjrxmNDscxeeqnAh.png)

> ### 参考资料<br/>[菜鸟教程](https://www.runoob.com/linux/linux-vim.html)

## Shell 编程

作为一个 linux 系统的编程语言

```powershell
vim test.sh # 创建文件
var_name=var_data # 创建变量
$var_name # 引用变量
echo this is a string
echo $var_name
```

通过 $ 调用变量

shell 中所有的变量都是字符串

```powershell
x=1
y=2
z=x+y
echo $z # output:x+y
let z=x+y     # output:3
z=$[x+y]      # output:3
z=$((x+y))    # output:3
```

注意，变量名和等号之间不能有空格

### shell 逻辑结构

#### 判断：if

```powershell
if condition
then
    do commmand
elif condition2
then
    do command
else
then
    do command
fi

if [$x -lt 5]
then
    echo yes
else
    echo no
fi
```

#### 循环：for

```powershell
for var in item1 item2 item3 item4
do
    echo command
done
```

#### 循环：while/until

```powershell
x=1
while [$x -lt 5]
do
    x=$[x+1]
fi
```

#### 条件：case

```powershell
case expression in
    pattern1)
        command1
        ;;
    pattern2)
        command2
        ;;
    pattern3|pattern4)
        command3
        ;;
    *)
        default_command
        ;;
esac
```

> ### 参考资料<br/>[菜鸟教程-](https://www.runoob.com/linux/linux-shell.html)[Shell 教程](https://www.runoob.com/linux/linux-shell.html)

# <strong>讨论主题</strong>

1. 如何使用项目/Assignment 来提高对 vim、shell 编程等工具的掌握程度？
2. cat，nano，vim 不同命令的区别？

# 内容

## cat，vim，nano 等命令的差异

cat 命令是 linux 系统下一个文本打印的命令，用于输出一个文本的信息到控制台上，该命令的输入类似于使用 word 打开一个文档，但是该文档不能编辑

vi/vim 命令是 linux 系统下用于文本查看、编辑的命令，不仅仅可以查看，还可以编辑

nano 命令类似于 vim 命令的功能，命令语句为：nano p（打开 p 文件）

> 原文链接：[https://blog.csdn.net/a22635798/article/details/103555342](https://blog.csdn.net/a22635798/article/details/103555342)

## 重要讨论成果

确立学习思路：利用 new bing 或 ChatGPT 根据课堂内容布置相关的综合项目，通过完成项目来掌握各类比对软件、代码等，培养综合能力

### <strong>Assignment: Write a shell script to automate BLAST searches</strong>

In this assignment, you will write a shell script that automates the process of performing BLAST searches on multiple FASTA files.

Your script should take the following inputs:

- The path to a directory containing FASTA files
- The path to an output directory where the BLAST results will be saved

Your script should perform the following tasks:

1. Loop through all the FASTA files in the input directory
2. For each FASTA file, run a BLAST search using the `blastn` command
3. Save the results of the BLAST search to a file in the output directory with the same name as the input FASTA file, but with a `.blast` extension

Your script should be well-documented with comments explaining what each part of the code does.

Submit your completed script as a `.sh` file.

#### Reference answer

```powershell
#!/bin/bash

# Check that the correct number of arguments were provided
if [ $# -ne 2 ]; then
    echo "Usage: $0 <input_dir> <output_dir>"
    exit 1
fi

# Set the input and output directories
input_dir=$1
output_dir=$2

# Create the output directory if it doesn't already exist
mkdir -p $output_dir

# Loop through all the FASTA files in the input directory
for fasta_file in $input_dir/*.fasta;  do
    # Get the base name of the FASTA file (without the .fasta extension)
    base_name=$(basename $fasta_file .fasta) # basename means "basic name"

    # Set the name of the output BLAST file
    blast_file=$output_dir/$base_name.blast

    # Run BLAST on the current FASTA file
    blastn -query $fasta_file -db nt -out $blast_file
done
```

This script takes two arguments: the path to the input directory containing FASTA files and the path to the output directory where the BLAST results will be saved. It checks that the correct number of arguments were provided and exits with an error message if not.

The script sets the `input_dir` and `output_dir` variables to the values provided by the user. It then creates the output directory if it doesn’t already exist using `mkdir -p`.

The script uses a `for` loop to iterate over all the FASTA files in the input directory. Inside the loop, it uses `basename` to get the base name of the current FASTA file (without the `.fasta` extension) and sets the `blast_file` variable to the path of the output BLAST file (using `$output_dir/$base_name.blast`).

The script then runs BLAST on the current FASTA file using `blastn -query $fasta_file -db nt -out $blast_file`. This command specifies the input FASTA file using `-query $fasta_file`, specifies that it should search against the `nt` database using `-db nt`, and specifies that it should save the results to a file using `-out $blast_file`.

### <strong>Assignment: Write a shell script to automate RNA-Seq data processing</strong>

In this assignment, you will write a shell script that automates the process of processing RNA-Seq data.

Your script should take the following inputs:

- The path to a directory containing FASTQ files
- The path to a reference genome file in FASTA format
- The path to an output directory where the processed data will be saved

Your script should perform the following tasks:

1. Loop through all the FASTQ files in the input directory
2. For each FASTQ file, perform quality control checks using FastQC
3. Trim low-quality reads using a tool like Trimmomatic
4. Align the trimmed reads to the reference genome using a tool like HISAT2
5. Assemble the aligned reads into transcripts using a tool like StringTie
6. Save the assembled transcripts to a file in the output directory with the same name as the input FASTQ file, but with a `.gtf` extension

Your script should be well-documented with comments explaining what each part of the code does.

Submit your completed script as a `.sh` file.

#### reference answer

```powershell
# Author<strong>@吴航锐</strong> 
# 2023/4/9 14:10:00

##### 1 trimmatic
mkdir clean
cd clean

find /home/wuhangrui/rawdata/20221024/01.RawData -name "*fq.gz" |grep 1.fq.gz | sort > 1.txt
find /home/wuhangrui/rawdata/20221024/01.RawData -name "*fq.gz" |grep 2.fq.gz | sort > 2.txt
paste 1.txt 2.txt > config1

#mkdir {fastqc,multiqc_result,fastqc_filtered,multiqc_result_filtered}

echo "trimmomatic cut adapters starts at $(date)"
cat config1 |while read id
do
arr=(${id})
fq1=${arr[0]}
fq2=${arr[1]}
filename=echo $(basename $fq1 _1.fq.gz)
trimmomatic PE -threads 20 -phred33 $fq1 $fq2 \
-baseout ${filename}.fq.gz \
ILLUMINACLIP:/home/wuhangrui/miniconda3/pkgs/trimmomatic-0.39-hdfd78af_2/share/trimmomatic-0.39-2/adapters/NexteraPE-PE.fa:2:30:10 SLIDINGWINDOW:5:20 LEADING:5 TRAILING:5 MINLEN:40 HEADCROP:13
echo "trimomatic cut adapters finished at $(date)"
done


##### 2 fastqc
cd clean

mkdir {fastqc,multiqc_result,fastqc_filtered,multiqc_result_filtered}
echo "fastqc started at $(date)"

cat config1 |while read id
do
arr=(${id})
fq1=${arr[0]}
fq2=${arr[1]}
filename=`echo $(basename $fq1 _1.fq.gz)`

fq11=${filename}_1P.fq.gz
fq22=${filename}_2P.fq.gz
fastqc $fq1 $fq2 -q --noextract -t 20 -o fastqc
fastqc $fq11 $fq22 -q --noextract -t 20 -o fastqc_filtered

done

multiqc fastqc -o multiqc_result
multiqc fastqc_filtered -o multiqc_result_filtered

echo "fastqc finished at $(date)"


##### 3 hisat2
cd clean

mkdir aligndata_hisat2

echo "hisat2 started at $(date)"

cat config1  |while read id
do
arr=(${id})
fq1=${arr[0]}
fq2=${arr[1]}
filename=`echo $(basename $fq1 _1.fq.gz)`

fq11=${filename}_1P.fq.gz
fq22=${filename}_2P.fq.gz

hisat2 -p 20 -x /home/wuhangrui/database/ref/hg38/hisat2/grch38/genome -1 $fq11 -2 $fq22 -S ${filename}.sam  
 
mv *.sam aligndata_hisat2
cd aligndata_hisat2

samtools view -S ${filename}.sam -b > ${filename}.bam

samtools sort ${filename}.bam -o ${filename}_sorted.bam

samtools index ${filename}_sorted.bam

cd ../

done
echo "hisat2 finished at $(date)"

##### 3 also you can use STAR to align
cd clean2

mkdir aligndata_star

echo "STAR started at $(date)"

# 第一次运行程序需要执行star index这行命令，生成index文件
### get star index
#STAR \
#--runThreadN 40 \
#--runMode genomeGenerate \
#--genomeDir /home/wuhangrui/database/ref/hg38/star \
#--genomeFastaFiles /home/wuhangrui/database/ref/hg38/GRCh38.p13.genome.fa \
#--sjdbGTFfile /home/wuhangrui/database/ref/hg38/gencode.v42.chr_patch_hapl_scaff.annotation.gtf \
#--sjdbOverhang 149 \

for i in *_1P.fq

do
filename=`echo $(basename $i _1P.fq)`

fq11=${filename}_1P.fq
fq22=${filename}_2P.fq

STAR \
--runThreadN 40 \
--genomeDir /home/wuhangrui/database/ref/hg38/star \
--readFilesIn $fq11 $fq22 \
--sjdbOverhang 149 \
--outFileNamePrefix ./aligndata_star/${filename} 

cd aligndata_star

samtools view -S ${filename}Aligned.out.sam -b > ${filename}.bam

samtools sort ${filename}.bam -o ${filename}_sorted.bam

samtools index ${filename}_sorted.bam

cd ../

done
echo "STAR finished at $(date)"


##### 4 htseq and salmon_quant to obtain expression Matrix
cd clean2

mkdir htseq
mkdir salmon_quant

echo "htseq+salmon started at $(date)"

find /home/wuhangrui/rawdata/20221024/01.RawData -name "*fq.gz" |grep 1.fq.gz | sort > 1.txt
find /home/wuhangrui/rawdata/20221024/01.RawData -name "*fq.gz" |grep 2.fq.gz | sort > 2.txt
paste 1.txt 2.txt > config1

cat config1 |while read id
do
arr=(${id})
fq1=${arr[0]}
fq2=${arr[1]}
filename=`echo $(basename $fq1 _1.fq.gz)`

fq11=${filename}_1P.fq
fq22=${filename}_2P.fq

# htseq-count 得到表达矩阵
nohup htseq-count -f bam -r name -s no -a 10 -t exon -i gene_id -m union ./aligndata_star/${filename}_sorted.bam /home/wuhangrui/database/ref/hg38/gencode.v42.chr_patch_hapl_scaff.annotation.gtf > ./htseq/${filename}_star_htseq_count.txt 2>log &

# salmon_quant 得到表达矩阵，与htseq-count可替代，选择一个使用即可
# salmon_quant 不用提供bam文件，可以直接提供fastq文件
cd salmon_quant
salmon quant --gcBias -i /home/wuhangrui/database/ref/hg38/salmon_index_gencode -l A -1 ../$fq11 -2 ../$fq22 -g /home/wuhangrui/database/ref/hg38/gencode.v42.chr_patch_hapl_scaff.annotation.gtf -o ./${filename}_salmon_quant
#salmon quant -i /home/wuhangrui/database/ref/hg38/salmon_index_gencode -l A -1 ../$fq11 -2 ../$fq22 -g /home/wuhangrui/database/ref/hg38/Homo_sapines.GRCh38.108.chr_patch_hapl_scaff.annotation.gtf -o ./${filename}_salmon_quant

awk '$4>1{print$0}' ${filename}_salmon_quant/quant.genes.sf > ${filename}_tpm.txt
wc -l ${filename}_tpm.txt >> tpm.txt
cd ../

done

echo "htseq+salmon finished at $(date)"
```

#### Reference answer from bing

```bash
#!/bin/bash

# Check that the correct number of arguments were provided
if [ $# -ne 3 ]; then
    echo "Usage: $0 <input_dir> <reference_genome> <output_dir>"exit 1
fi

# Set the input and output directories and the reference genome file
input_dir=$1
reference_genome=$2
output_dir=$3

# Create the output directory if it doesn't already exist
mkdir -p $output_dir

# Loop through all the FASTQ files in the input directory
for fastq_file in $input_dir/*.fastq; do
    # Get the base name of the FASTQ file (without the .fastq extension)
    base_name=$(basename $fastq_file .fastq)

    # Set the names of the intermediate and output files
    fastqc_output=$output_dir/$base_name\_fastqc.html
    trimmed_fastq=$output_dir/$base_name\_trimmed.fastq
    aligned_sam=$output_dir/$base_name\_aligned.sam
    assembled_gtf=$output_dir/$base_name.gtf

    # Run FastQC on the current FASTQ file
    fastqc $fastq_file -o $output_dir
    
    # Trim low-quality reads using Trimmomatic
    trimmomatic SE $fastq_file $trimmed_fastq LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36

    # Align the trimmed reads to the reference genome using HISAT2
    hisat2 -x $reference_genome -U $trimmed_fastq -S $aligned_sam
    
    # Assemble the aligned reads into transcripts using StringTie
    stringtie $aligned_sam -o $assembled_gtf -p 8 -G $reference_genomedone
```

This script takes three arguments: the path to the input directory containing FASTQ files, the path to a reference genome file in FASTA format, and the path to an output directory where the processed data will be saved. It checks that the correct number of arguments were provided and exits with an error message if not.

The script sets the `input_dir`, `reference_genome`, and `output_dir` variables to the values provided by the user. It then creates the output directory if it doesn’t already exist using `mkdir -p`.

The script uses a `for` loop to iterate over all the FASTQ files in the input directory. Inside the loop, it uses `basename` to get the base name of the current FASTQ file (without the `.fastq` extension) and sets several variables to specify the names of intermediate and output files that will be generated during processing.

The script then runs FastQC on the current FASTQ file using `fastqc $fastq_file -o $output_dir` to perform quality control checks. It trims low-quality reads from the FASTQ file using `trimmomatic SE $fastq_file $trimmed_fastq LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36`. It aligns the trimmed reads to the reference genome using `hisat2 -x $reference_genome -U $trimmed_fastq -S $aligned_sam`. Finally, it assembles the aligned reads into transcripts using `stringtie $aligned_sam -o $assembled_gtf -p 8 -G $reference_genome`.

### <strong>Assignment: Write a shell script to automate variant calling</strong>

In this assignment, you will write a shell script that automates the process of calling variants from whole-genome sequencing data.

Your script should take the following inputs:

- The path to a directory containing BAM files
- The path to a reference genome file in FASTA format
- The path to an output directory where the variant calls will be saved

Your script should perform the following tasks:

1. Loop through all the BAM files in the input directory
2. For each BAM file, perform variant calling using a tool like FreeBayes
3. Save the variant calls to a file in the output directory with the same name as the input BAM file, but with a `.vcf` extension

Your script should be well-documented with comments explaining what each part of the code does.

Submit your completed script as a `.sh` file.

#### Reference answer

只针对使用的软件写了代码，<strong>没有下载数据实操</strong>

```powershell
# Author<strong>@高大可</strong> 
# 2023/4/9 14:37:00

#去除两端低质量区域
fastp -i read_1.fastq.gz -I read_2.fastq.gz -o read_clean_1.fastq.gz -O read_clean_2.fastq.gz -u 50 -n 5 -q 20 -5 -3 -M 4 -l 50 --html read.html --json read.json >read_fastp.log 2>&1

#-u 50 -q 20    去除质量低于20的位点占50%以上的read
#-n 5    去除有5个以上N的reads
#-5 -3 -M 4    从两端去除平均质量低于20的区域，以4个碱基为单位。
#-l 50 去除小于50bp的reads（修剪前长度） 

#mapping
bwa mem -t 6 -M -R ‘@RG\tID:$sample\tSM:$sample\tLB:$sample’ \
    $sample_R1.fq.gz  $sample_R2.fq.gz >$sample.sam
# -t INT 使用的线程数目
# -M 加入-M后，可将shorter split hits标记为次优
# -R STR        read group header line such as '@RG\tID:foo\tSM:bar' [null]
samtools fixmate -O bam $sample.sam $sample.bam 
# samtools fixmate <in.nameSrt.bam> <out.nameSrt.bam>
# fix mate information
samtools sort -O bam -o $sample_sort.bam -T $sample_tmp  $sample.bam


#mark duplicates, remove optical duplicates
java -Xmx80g -jar picard.jar MarkDuplicates  REMOVE_SEQUENCING_DUPLICATES=true 
      I=$sample_sort.bam  
      O=$sample_mkdup.bam 
      M=$sample_dup_metrics.txt 
#去除duplicates
samtools index -b $sample_mkdup.bam


#call snp with FreeBayes
freebayes -f ${fasta_reference}.fasta -L bam.list -r 2L:0-1000000 \
        -m 20 -q 20 -v out.vcf
#call snp一般使用freebayes
# -f fasta参考文件
# -r --region <chrom>:<start_position>-<end_position>
# -m --min-mapping-quality Q
# -q --min-base-quality Q
```
