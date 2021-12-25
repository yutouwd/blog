---
title: kaldi中的声纹识别
tags:
  - kaldi
  - 声纹识别
  - ivector
categories: 
  - 声纹识别
  - kaldi
comments: true
abbrlink: 364e185b
date: 2019-01-31 09:18:34
---


前段时间一直到在使用kaldi来做声纹识别，算是可以把整个ivector的例程可以跑下来，也可以根据例程来改写脚本，使用自己的数据来训练和测试。接下来可能要去做其他的项目了，所以要趁着还记得的时候赶紧写个总结，也算是对之前的工作也算是归纳一下。
<!-- more -->
## kaldi的安装
kaldi在Linux下的安装总的来说还是比较简单的，首先是先进入tools中运行extras/check_dependenices.sh看下还有哪些依赖项没有安装，然后就可以按照他的提示来安装依赖项目。安装完依赖项之后就分别进入tools目录和src目录下执行命令make -j8，其中8时cpu可以同时运行的线程数量。这个过程还是需要一定时间的。在make完之后就可以运行一个小的例程来看下有没有成功地安装kaldi，我们进入到egs/yesno/s5目录下然后运行run.sh脚本，这是一个判断语音中说的是yes还是no的程序，他会自动下载数据并训练和测试，最终可以有0.0%的WER，这就代表kaldi安装成功啦✌️

## 运行aishell例程
首先我们来看下kaldi下的目录：

![](/upload_image/1.png)

* egs：保存了各种例程，均使用脚本编写，以使用的数据库的名字命名。在下一级目录中以s开头的文件是语音识别，以v开头的是声纹识别，一般v1就是使用i-vector的方法来进行声纹识别。
* src：保存了kaldi的C++代码。
* tools：包括了kaldi依赖的库和一些实用的脚本。
* windows：包括了在Windows下安装需要的一些工具和配置文件

接下来我们就来跑一下aishell的声纹识别例程，在egs/aishell/v1中的run.sh就包括了整个声纹识别的流程，最好将run.sh中的命令复制到另外一个脚本中，一句一句地执行，这样就能及时发现错误然后修改。

```Bash
data=/export/a05/xna/data
data_url=www.openslr.org/resources/33

. ./cmd.sh
. ./path.sh

set -e # exit on error

local/download_and_untar.sh $data $data_url data_aishell
local/download_and_untar.sh $data $data_url resource_aishell

# Data Preparation
local/aishell_data_prep.sh $data/data_aishell/wav $data/data_aishell/transcript

```

首先是数据准备阶段，如果没有下载数据，脚本也可以自动下载和解压；如果下载好了就要把data的路径改成自己存放数据的路径。之后的cmd.sh和path.sh分别是设置执行命令的方式和kaldi的路径。如果我们是在自己的电脑上运行，就需要进入到cmd.sh中，把queue.pl修改成run.pl。path.sh就是设置和kaldi相关的路径，如果是例程的话就不用修改了。配置好之后就开始下载和解压数据。

之后就是最关键的部分了，准备一些下面环节需要的文档，使用aishell_data_prep.sh这个脚本来生成。声纹识别需要用到的分别是utt2spk spk2utt wav.scp这三个文件。其中utt指的是utterance代表一个音频文件的文件名，spk代表speaker是说话人的ID，这里在下一节做详细的介绍。如果是做语音识别，还需要text文件，这里就不做介绍了。

```Bash
# Now make MFCC  features.
# mfccdir should be some place with a largish disk where you
# want to store MFCC features.
mfccdir=mfcc
for x in train test; do
  steps/make_mfcc.sh --cmd "$train_cmd" --nj 10 data/$x exp/make_mfcc/$x $mfccdir
  sid/compute_vad_decision.sh --nj 10 --cmd "$train_cmd" data/$x exp/make_mfcc/$x $mfccdir
  utils/fix_data_dir.sh data/$x
done
```

在准备好数据之后就要开始提取mfcc特征了（make_mfcc的过程中也包括了分帧加窗），进行端点检测（VAD），以及检查文件符不符合要求对文件进行排序（其实我也没有看太懂fix_data_dir.sh这个脚本到底做了什么😑)

```Bash
# train diag ubm
sid/train_diag_ubm.sh --nj 10 --cmd "$train_cmd" --num-threads 16 \
  data/train 1024 exp/diag_ubm_1024

#train full ubm
sid/train_full_ubm.sh --nj 10 --cmd "$train_cmd" data/train \
  exp/diag_ubm_1024 exp/full_ubm_1024

#train ivector
sid/train_ivector_extractor.sh --cmd "$train_cmd --mem 10G" \
  --num-iters 5 exp/full_ubm_1024/final.ubm data/train \
  exp/extractor_1024
```

再接下来就是训练UBM和ivector extractor了，这里需要注意的是训练ivector extractor的脚本会默认同时执行程序非常多，会占用很高的内存导致内存溢出。我们需要进入train_ivector_extractor.sh中修改一下。它默认同时执行的程序数量为nj\*num_thread\*num_processes,在16G内存下我把这三个参数都改为2才能跑通。这里也还有两个超参数可以修改，分别是UBM的维数和ivector的维数，UBM的维数就直接在run.sh中修改就行，train_diag_ubm.sh中data/train后面那个参数就是UBM的维数，默认为1024。要修改ivector的维数就同样需要进到train_ivector_extractor.sh中修改ivector_dim，默认为400。

```Bash
#extract ivector
sid/extract_ivectors.sh --cmd "$train_cmd" --nj 10 \
  exp/extractor_1024 data/train exp/ivector_train_1024

#train plda
$train_cmd exp/ivector_train_1024/log/plda.log \
  ivector-compute-plda ark:data/train/spk2utt \
  'ark:ivector-normalize-length scp:exp/ivector_train_1024/ivector.scp  ark:- |' \
  exp/ivector_train_1024/plda
```

训练完ivector之后就要开始提取训练集的ivector了，然后用训练集的ivector来训练plda模型用于打分。

```Bash
# split the test to enroll and eval
mkdir -p data/test/enroll data/test/eval
cp data/test/{spk2utt,feats.scp,vad.scp} data/test/enroll
cp data/test/{spk2utt,feats.scp,vad.scp} data/test/eval
local/split_data_enroll_eval.py data/test/utt2spk  data/test/enroll/utt2spk  data/test/eval/utt2spk
trials=data/test/aishell_speaker_ver.lst
local/produce_trials.py data/test/eval/utt2spk $trials
utils/fix_data_dir.sh data/test/enroll
utils/fix_data_dir.sh data/test/eval
```

之后就要将测试集分为注册集和验证集，这一步主要通过loacl/split_data_enroll_eval.py这个脚本来完成，我们先来看一下这个脚本：

```python
# split_data_enroll_eval.py
import sys,random

dictutt = {}

for line in open(sys.argv[1]):
  line = line.rstrip('\r\t\n ')
  utt, spk = line.split(' ')
  if spk not in dictutt:
    dictutt[spk] = []
  dictutt[spk].append(utt)

fenroll = open(sys.argv[2], 'w')
feval = open(sys.argv[3], 'w')

for key in dictutt:
  utts = dictutt[key]
  random.shuffle(utts)
  for i in range(0, len(utts)):
    line = utts[i] + ' ' + key
    if(i < 3):
      fenroll.write(line + '\n')
    else:
      feval.write(line + '\n')

fenroll.close()
feval.close()

```

这个脚本首先先将每个spk和与其对应的utt存入dictutt中，然后再将spk的utt顺序随机打乱，重新分配到enroll（注册集）和eval（评估集）中。可以看到在程序的倒数第六行中，if(i<3):就将utt写入enroll中，否则就写入eval中。所以我们可以通过改这个值来改变注册集和评估集中的语音数。

在重新生成完utt2spk之后，就要生成trials了。trials通过loacl/product_trials.py来生成。trials是指需要进行打分的注册说话人和不同的语音的一个列表，它的格式为(举个例子🌰）：

| uttID | spkID | target/nontarget |
| --- | --- | --- |
| spkA-utt1 | spkA | target |
| spkA-utt2 | spkB | nontarget |
| spkB-utt1 | spkA | nontarget |
| spkB-utt1 | spkB | target |
| ... | ... | ... |

```Bash
#extract enroll ivector
sid/extract_ivectors.sh --cmd "$train_cmd" --nj 10 \
  exp/extractor_1024 data/test/enroll  exp/ivector_enroll_1024
#extract eval ivector
sid/extract_ivectors.sh --cmd "$train_cmd" --nj 10 \
  exp/extractor_1024 data/test/eval  exp/ivector_eval_1024

#compute plda score
$train_cmd exp/ivector_eval_1024/log/plda_score.log \
  ivector-plda-scoring --num-utts=ark:exp/ivector_enroll_1024/num_utts.ark \
  exp/ivector_train_1024/plda \
  ark:exp/ivector_enroll_1024/spk_ivector.ark \
  "ark:ivector-normalize-length scp:exp/ivector_eval_1024/ivector.scp ark:- |" \
  "cat '$trials' | awk '{print \\\$2, \\\$1}' |" exp/trials_out

#compute eer
awk '{print $3}' exp/trials_out | paste - $trials | awk '{print $1, $4}' | compute-eer -
```

在将测试集分成注册集和评估集之后，就开始分别提取注册集和评估集的ivector，然后按照生成的trials打分，最终打分结果输出在trials_out中,最终跑出来的结果为eer为0.183%。

## 使用TIMIT数据库进行声纹识别
在了解了kaldi中整个声纹识别的流程后，我们就可以AISHELL的例程来改写使用自己数据的声纹识别系统，这里我使用TIMIT数据库。

我们首先看下AISHELL和TIMIT数据库中的数据划分。AISHELL中一共有400人，默认分为train、dev和test集。其中train里面有340人；dev里面有40人；test里面有20人。在例程中，使用train作为训练集，test作为测试集，并没有使用dev。AISHELL里每个人大概有300多段语音，每段语音是一句话，每段语音大概在2~6s。在TIMIT数据库中一共有630人，分为train和test。训练集中有462人，测试集中有168人。每个人分别有10段语音，每段语音大概在2~4s。这里就直接使用TIMIT的原本的分配方式，用462人作为训练集，168人作为测试集。

不过使用TIMIT数据库还有一个问题就是，TIMIT数据库中文件存放以及命名的方式和AISHELL不太一样。TIMIT数据库下文件存放的结构是，/TRAIN/DR*/SPEARKER_ID/UTTERANCE_ID.wav，train代表是训练集或者测试集，DR\*（1～8）代表了说话人的方言类型，然后是说话人的ID文件夹，文件夹下存放了10段语音。TIMIT数据库中不同的人会说同一段话，说的话的内容是一样的话文件名就是一样的，我不知道如果有相同的文件名会不会引发错误，稳妥起见还是把每个文件都重新命名了。我写了个程序，将文件都重新命名为说话人的ID加上音频的序号，并且将其重新保存在/TRAIN/SPEAKER_ID这样的目录下，这样就在下面的程序就可以不用修改太多。

在了解完两个数据库的区别和整个声纹识别的流程之后，我们就可以开始改写我们的程序了。其实整个过程中需要改的地方并不多，主要就是在准备数据阶段和生成trials的过程需要修改一下。首先是数据准备阶段，我们就可以根据哈aishell_data_prepare.sh这个脚本来改写自己的timit_data_prepare.sh了。数据准备阶段就要生成utt2spk spk2utt和wav.scp这三个文件。这三个文件的格式如下：

| 文件名 | 格式 |
| --- | --- |
| utt2spk | [音频文件名] [说话人ID] |
| spk2utt | [说话人名] [音频文件名] [音频文件名] [音频文件名] |
| wav.scp | [音频文件名] [音频文件的具体路径] |

```Bash
. ./path.sh || exit 1;

if [ $# != 2 ]; then
  echo "Usage: $0 <audio-path> <text-path>"
  echo " $0 /export/a05/xna/data/data_aishell/wav /export/a05/xna/data/data_aishell/transcript"
  exit 1;
fi

aishell_audio_dir=$1
aishell_text_dir=$2

train_dir=data/local/train
dev_dir=data/local/dev
test_dir=data/local/test

mkdir -p $train_dir
mkdir -p $dev_dir
mkdir -p $test_dir

# data directory check
if [ ! -d $aishell_audio_dir ] || [ ! -d $aishell_text_dir ]; then
  echo "Error: $0 requires two directory arguments"
  exit 1;
fi

# find wav audio file for train, dev and test resp.
find $aishell_audio_dir -iname "*.wav" | grep -i "wav/train" > $train_dir/wav.flist || exit 1;
find $aishell_audio_dir -iname "*.wav" | grep -i "wav/dev" > $dev_dir/wav.flist || exit 1;
find $aishell_audio_dir -iname "*.wav" | grep -i "wav/test" > $test_dir/wav.flist || exit 1;
```

前面首先是检查路径和创建用来存放文件的路径，由于在TIMIT中没有dev集，所以要把带有dev的都删掉。接下来脚本查找目录下的所有wav文件。

```Bash
n=`cat $train_dir/wav.flist $dev_dir/wav.flist $test_dir/wav.flist | wc -l`
[ $n -ne 141925 ] && \
  echo Warning: expected 141925 data data files, found $n

# Transcriptions preparation
for dir in $train_dir $test_dir; do
  echo Preparing $dir transcriptions
  sed -e 's/\.wav//' $dir/wav.flist | awk -F '/' '{print $NF}' > $dir/utt.list
  sed -e 's/\.wav//' $dir/wav.flist | awk -F '/' '{i=NF-1;printf("%s %s\n",$NF,$i)}' > $dir/utt2spk_all
  paste -d' ' $dir/utt.list $dir/wav.flist > $dir/wav.scp_all
  utils/filter_scp.pl -f 1 $dir/utt.list $aishell_text_dir/*.txt > $dir/transcripts.txt
  awk '{print $1}' $dir/transcripts.txt | sort -u > $dir/utt.list
  utils/filter_scp.pl -f 1 $dir/utt.list $dir/utt2spk_all | sort -u > $dir/utt2spk
  utils/filter_scp.pl -f 1 $dir/utt.list $dir/wav.scp_all | sort -u > $dir/wav.scp
  sort -u $dir/transcripts.txt > $dir/text
  utils/utt2spk_to_spk2utt.pl $dir/utt2spk > $dir/spk2utt
done

mkdir -p data/train data/test
for f in spk2utt utt2spk wav.scp text; do
  cp $train_dir/$f data/train/$f || exit 1;
  cp $test_dir/$f data/test/$f || exit 1;
done

echo "$0: AISHELL data preparation succeeded"
exit 0;
```

接下来就检查找到的wav文件加起来有没有141924个，然后就开始做wav.scp、utt2spk和spk2utt以及用于语音识别的transcripts.txt，这里我们就要找到脚本中和transcripts.txt相关的，然后删掉就可以了。

再做完准备数据的阶段之后，我们就可以开始按照上面的流程来进行声纹识别了。还需要注意的一点是trials，如果一个人只有两三段语音的话，就需要修改分配enroll集和eval集的比例。不过由于TIMIT数据库每个人有10段语音，所以不用修改也是可以的。这里就用3段语音去注册，然后剩下的7段语音用于验证。

最终跑出来的等错误率在4.5%左右，虽然是一个还可以接受的结果，但是和AISHELL的0.18%的等错误率相比还是差了很多的。分析一下原因：首先是用于训练的语音较少，虽然人数有462人，但是每个人只有10段语音，和AISHELL中340人用于训练，每个人300多段语音相比差了很多。同样的，TIMIT中测试集中一共有168人，相比于AISHELL中测试集只有40人多了很多。而且，AISHELL默认的训练的UBM阶数和ivector的维度都非常高，所以这两点可能导致了等错误率比较高。如果想进一步降低等错误率可以尝试降低训练的UBM和ivector的维度。我把UBM和ivector的维度都降低后，等错误率最终可以达到1.53%。

## kaldi中声纹识别的流程
总结一下，kaldi中声纹的识别（ivector）的流程图如下：

![](/upload_image/2.png)

首先，将数据集分为训练集和测试集。然后对先对训练集做处理，先提取训练集的mfcc特征，然后训练UBM和ivector extractor，接着提取训练集的ivector，并使用训练集的ivector去训练plda模型。之后就开始对测试集进行处理，先把测试集分为注册集和验证集，分别提取mfcc然后在提取ivector，在用plda进行打分。这就是整个kaldi中ivector声纹识别的流程了。