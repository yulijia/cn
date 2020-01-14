---
published: ture
layout: post
title: "Perl的没落"
author: Yu
categories: 生物信息
tags:
- Perl
---

Perl一直是生信领域工作人员习惯使用的编程语言，在处理序列文本方面有着得天独厚的优势。但是，目前生信领域可使用 Perl 的场景也都可以使用 Python，另外 Python 还在是数据分析机器学习相关方法的重要编程语言，我认为 Perl 会逐渐退出生信分析的历史舞台。由于Perl 5 和 Perl 6 不相互兼容，Perl 6在去年正式改名叫<q>Raku</q>，不少人也会从 Perl 转向其他社区活跃的编程语言。早在2010年左右，国内的 Perl China 还在组织一些定期的交流活动，但是现在已经找不到这个网站。使用Perl的这批人，已经进入了中年，没有时间和精力活跃在社区。Perl China 邮件列表里上一封邮件的发送日期还是2019年5月，目前估计都转战其他联系平台（微信群和slack）。

那么为啥现在还有那么多生信初学者在学习Perl呢？个人观点是由于目前做到PI的人，在他们学习生信的时期，主要用的是 Perl 语言，所以由于这种<q>惯性</q>，我们还会在很多 lab 招聘信息上看到要求应聘的生信博士们要会Perl。常用的由Perl编写的最有名生信软件是`Annovar`。除此之外，`bcftools`和`samtools`里一些小工具是Perl编写的，如果你用不到的话，可能根本就没注意过这些Perl代码。

翻了翻我自己写的 Perl 代码，基本上就做了以下10件事情，以前写东西特别 naive，最后一个代码超级长且都是不必要的重复。最近，我写 Perl 代码的时候越来越少了，除了修改代码 bug 或者写一行命令搞定个小测试外，已经用不到 Perl。


### 1.计算序列中某些信息的出现频率（GC content）


```perl
#!usr/bin/perl -w
$name="Homo_sapiens.GRCh37.66.dna.chromosome";
$input="/data/GENE_transcripLoc.bed";
open FILE,"$input"|| die "Couldn't open $input: $!";

while (defined ($eachline =<FILE>)) {
  chomp $eachline;
  ($chr,$begin,$end,$strand,$geneID,$transID,$other)=();
  ($chr,$begin,$end,$strand,$geneID,$transID,$other)=split /\t/, $eachline;
  $data="/data/data4/yu/homo_sapiens_dna/$name.$chr.fa";
  open DATA,"$data" or die "Couldn't open $data: $!";
  chomp(@DNA = <DATA>);
  $line=join("",@DNA);
        $str=substr($line,$begin,$end); 
        my $num_a    = $str =~ tr/A//;
        my $num_c    = $str =~ tr/C//;
        my $num_g    = $str =~ tr/G//;
        my $num_t    = $str =~ tr/T//;
        #my $num_o    = length($str) - $num_a - $num_c - $num_g - $num_t;
        my $gc       =( $num_c + $num_g ) / length($str)  * 100 ;
        $outpromoter="/data/data4/yu/GCcontent_genebody.bed";
        open PLOG,">>$outpromoter" or die "Couldn't open $outputpromoter: $!";
        print PLOG "$chr\t$begin\t$end\t$strand\t$geneID\t$transID\t$gc\n";
        close PLOG;
  close DATA;
}
close FILE;
```

### 2.剪切序列（trim）


```perl
#!/usr/bin/perl -w

while (<DATA>) {
    s/^(?!>)...(.*)..../$1/;
    #       ^^^    ^^^^  
    #       x=3    y=4
    print;
}

__DATA__
>HWI-EAS158_40_3_1_46_535
GTGAATGCGTGATACAGGAATGTTCGTTGTGACCAT
>HWI-EAS158_40_3_1_47_579
AAAGTGAATGCGTGATACAGGAATGTTCGTTGTGAC
>HWI-EAS158_40_3_1_46_731
GTGTCATGCGTGATACAGGAATGTTCGTTGTGAAAA
GTGTCATGCGTGATACAGGAATGTTCGTTGTGAAAA
```


### 3. 密码子转氨基酸 (抄自《Beginning Perl for Bioinformatics》)


```perl
#!/usr/bin/perl
use strict;
use warnings;
#Initialize variables
my $dna='CGACGTCTCGTACGG';
my $protein=''
my $codon;
#Translate each three-base codon into an amino acid,and append to a protein
for(my$i=0;$i<(length($dna)-2);$i+=3){
  $codon=substr($dna,$i,3);
    $protein.=codon2aa($codon);
}
printf"I translated the DNA\n\n$dna\n\n into the protein\n\n$protein\n\n"
exit;
#codon2aa
#A subroutine to translate a DNA 3- character codon to n amino acid
sub codon2aa{
  my($codon)=@_;
    if ($codon=~/GC./i){return'A'} #Alanine
      elsif ($codon=~/TG[TC]/i){return'C'} #Cysteine
        elsif ($codon=~/GA[TC]/i){return'D'} #Aspartic Acid
        elsif ($codon=~/GA[AG]/i){return'E'} #Glutamic Acid
        elsif ($codon=~/TT[Tc]/i){return'F'} #Phenylalanine
        elsif ($codon=~/GC./i){return'G'} #Glycine
        elsif ($codon=~/CA[TC]/i){return'H'} #Histidine
        elsif ($codon=~/AT[TCA]/i){return'I'} #Isoleucine
        elsif ($codon=~/TT[AG]|CT./i){return'L'} #Leucine
        elsif ($codon=~/ATG/i){return'M'} #Methionine
        elsif ($codon=~/AA[TC]/i){return'N'} #Asparagine
        elsif ($codon=~/CC./i){return'P'} #Proline
        elsif ($codon=~/CA[AG]/i){return'Q'} #Glutamine
        elsif ($codon=~/CG.|AG[AG]/i){return'R'} #Arginine
        elsif ($codon=~/TC.|AG[TC]/i){return'S'} #$erine
        elsif ($codon=~/AC./i){return'T'} #Threonine
        elsif ($codon=~/GT./i){return'V'} #Valine
        elsif ($codon=~/TGG/i){return'W'} #Tryptophan
        elsif ($codon=~/TA[TC]/i){return'Y'} #Tyrosine
        elsif ($codon=~/TA[AG]|TGA/i){return'_'} #Stop
    else{
      print STDERR"Bad codon\"$codon"!!\n";
        exit;
    }
}
```

### 4.下载序列信息（wget）

超级不建议用这个程序，要安装LWP模块，其实`wget`加个循环就可以下载了。

```perl
#!/usr/bin/perl
#use strict;
#use warnings;

my @down;
while($line=<DATA>){
  chomp $line;
  my $url= "http://www.ncbi.nlm.nih.gov/nuccore/$line?report=gilist&log\$=seqview&format=text";
  use LWP::Simple;
  my $content = get $url;
  print "Got $line Gi ID!\n";
  if($content=~/<pre>(.*)\n<\/pre>/s){
    push @download, $1;
  }
} 

getstore("http://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&rettype=fasta&retmode=text&id=".join(",",@download),"seqs.fasta");
print "Download all sequences!\n";
__DATA__
GU132860
GU132861
GU132862
GU132863
```

### 5.计算kmer组合

这个代码可以学习`push`和`shift`这样的操作。

```perl
#!/usr/bin/perl

$k = shift;
@bases = ('A','C','G','T');
@words = @bases;
for $i (1..$k-1){
  undef @newwords;
  foreach $w (@words){
    foreach $b (@bases){
      push (@newwords,$w.$b);
    }
  }
  undef @words;
  @words = @newwords;
}
foreach $w (@words){
  print "$w\n";
}
```

### 6.分割FASTA文件

这段代码可以学习`$/`，`$1`这样的标志是什么意思。

```perl
#!/usr/bin/perl   
usestrict;   
my($file, $dir) = @ARGV; #取得输入文件和输出文件夹   
open FILE, $file  
    or die "cannotopen$file:$!";    #打开文件   
local $/ = ">"; #设置读取结束标记为>,默认为\n   
my $i = 1;  #为输出文件编号   
while(<FILE>){   
    if(/^>$/){   
        next;   
    }   
    s/>//;  #去掉序列结束位置的>号   
    s/(\w+)/>$1/;   #为分割出来的序列第一行添加>号   
    my $name = $1;  #以fasta序列第一行的一个单词作为文件名   
    open OUTPUT, ">", $dir . '/' . $name . '_' . $i . '.fa';   
    print OUTPUT$_;   
    close OUTPUT;   
    $i++;   
}   
close FILE;  
```

### 7.将一段长序列变成FASTA格式

```perl
#!usr/bin/perl -w
$name="FRT.40A.chromosome";
$data="/share/test";
open DATA,"$data" or die "Couldn't open $data: $!";
chomp(@DNA = <DATA>);
$line=join("",@DNA);
my $length=length($line);
my $re=$length%50;
my $num=($length-$re)/50;
 
for ($i=1;$i<=$num;$i=$i+1){
    $str=substr($line,($i-1)*50+1,50);
    $output="/share/disk5-1/zhangzhhgroup/yulij/result/$name.fa";
    open LOG,">>$output" or die "Couldn't open $output: $!";
    print LOG "$str\n";
    close LOG;
  }

close DATA;
```

### 8.查找子序列位置

同`KMP`算法功能类似。

```perl
#usr/bin/perl -w
# initialize the original string
my $input = "Perl index, Perl chop, Perl hex";
my $pos = 0;

my @positions = ();

while(1){
  $pos = index(lc $input, "perl", $pos);
  last if($pos < 0);
  push(@positions, $pos++);
}       

if(scalar (@positions) > 0){
  print "substring found at positions: ", "@positions\n";
}else{
  print "substring not found\n";
}
```

### 9.找到与已知信息匹配的行

其实就是个`grep`命令。

```perl
#!usr/bin/perl -w
#$gen_file="/root/testperl.txt";
#open DATA, $gen_file or die "cannot open file";
$id="590168";
while (<DATA>) {
    print $_ if $_ =~ /$id/;
}
#close DATA;

__DATA__
COG1110 604354.TSIB_0530        1       1212
COG1110 604354.TSIB_0530        1       1212
COG1110 604354.TSIB_0530        1       1212
COG1110 598659.NAMH_1071        1       1060 
COG1110 593117.TGAM_1679        1       1216 
COG1110 590168.Tnap_0803        1       1104 
COG1110 579137.Metvu_1264       1       865 
COG1110 573064.Mefer_0049       6       869 
COG1110 563041.HPG27_964        428     531
COG1110 590168.Tnap_0803        1       1104
```

### 10. 用Perl提取网页信息

这是用perl写过的最长的一个程序，抓取和讯网站上的董秘信息，可能现在改改代码还能用。
如果让我现在写这个程序，肯定直接用Python美丽汤（Beautiful Soup）。

```perl
#!usr/bin/perl -w
#use WWW::Mechanize;
#use HTTP::Cookies;

use   LWP;
use   LWP::Simple; 
use LWP::UserAgent;
use Encode qw/encode decode from_to/;


use encoding "utf-8";
binmode(STDIN, ':utf8');
binmode(STDOUT, ':utf8');
binmode(STDERR, ':utf8');


print "股票代码|公司简称|公司全称|法定代表人|董秘|联系电话|传真|注册地址|办公地址|邮编|邮箱\n";
my @k="300001".."300999";
my $k;
foreach $k(@k){
my $url = "http://stockdata.stock.hexun.com/gszl/s$k.shtml";#"http://stockdata.stock.hexun.com/gszl/s000001.shtml";#'http://vip.stock.finance.sina.com.cn/corp/go.php/vCI_CorpInfo/stockid/000001.phtml';

my $content = get $url;
die "Couldn't get $url" unless defined $content;

my $begin="\<\!--平安银行公司简介--\>";
my $end="\<\!--平安银行公司简介--\>";


if($content=~ m/$begin(.*)$end/sgm){
  my $a="公司简称";
  my $b="股票代码";
  my $yyy=$1;
  
  if ($yyy=~m#$a(.*?)$b#sgm){
    my $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sgm){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}

}else {
  print "匹配失败|";
}
 
$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="股票代码";
  my $b="公司全称";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}


$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="公司全称";
  my $b="公司英文名称";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}



$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="法定代表人";
  my $b="独立董事";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}




$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="联系人";
  my $b="邮政编码";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}


$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="董秘";
  my $b="公司传真";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}



$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="公司传真";
  my $b="电子邮箱";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}




$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="注册地址";
  my $b="所得税率";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}



$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="办公地址";
  my $b="主要产品";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}


$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="邮政编码";
  my $b="公司简介";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/<td>(.*?)<\/td>/sg){
        print "$1|";
      }else {
  print "匹配失败|";
}
  }else {
  print "匹配失败|";
}
}else {
  print "匹配失败|";
}



$content = get $url;
die "Couldn't get $url" unless defined $content;

$begin="\<\!--平安银行公司简介--\>";
$end="\<\!--平安银行公司简介--\>";

if($content=~ m/$begin(.*)$end/sg){
  my $a="mailto:";
  my $b="公司网址";
  my $yyy=$1;
  if ($yyy=~m#$a(.*?)$b#sg){
    $zzz=$1;
    if ($zzz=~m/target=\"_blank\">(.*?)<\/a>/sg){
        print "$1\n";
      }else {
  print "匹配失败\n";
}
  }else {
  print "匹配失败\n";
}
}else {
  print "匹配失败\n";
}


}
```
