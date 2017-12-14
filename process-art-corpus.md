
Alicia Sigmon

als333@pitt.edu

11/19/2017

# Discourse Analysis of the Australian Radio Talkback Corpus
This file creates data frames for speakers, lines of text, and back channels. See [analysis.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.md) for my analysis.

### Table of Contents
- [About the Corpus](#About-the-Corpus)
- [Discourse Analysis Goals](#Discourse-Analysis-Goals)
- [Getting the Files](#Getting-the-Files)
- [Getting the Texts](#Getting-the-Texts)
    - [Original Speaker Data Format in the Raw Text Files](#Original-Speaker-Data-Format-in-the-Raw-Text-Files)
    - [Splitting NAT4-raw.txt into 2 files](#Splitting-NAT4-raw.txt-into-2-files)
    - [Trial Run Splitting Texts by Lines](#Trial-Run-Splitting-Texts-by-Lines)
- [Data Cleaning](#Data-Cleaning)
- [Speaker Information](#Speaker-Information)
    - [Creating Unique Speaker Ids](#Creating-Unique-Speaker-Ids)
    - [Speaker Dictionary](#Speaker-Dictionary)
    - [Speaker Data Frame](#Speaker-Data-Frame)
- [Splitting the Texts by Line](#Splitting-the-Texts-by-Line)
     - [List of Each Line of Text](#List-of-Each-Line-of-Text)
     - [Text Lines Data Frame](#Text-Lines-Data-Frame)
- [Adding Number of Utterances per Speaker to the Speaker Data Frame](#Adding-Number-of-Utterances-per-Speaker-to-the-Speaker-Data-Frame)
- [Creating Separate Presenter, Caller, and Expert Data Frames](#Creating-Separate-Presenter,-Caller,-and-Expert-Data-Frames)
- [Calculating Average Sentence and Word Lengths by Speaker Type](#Calculating-Average-Sentence-and-Word-Lengths-by-Speaker-Type)
    - [Trial Run Word and Sentence Tokeninzation](#Trial-Run-Word-and-Sentence-Tokeninzation)
    - [Word and Sentence Tokenization](#Word-and-Sentence-Tokenization)
    - [Expanding art_df to Include Word and Sentence Information](#Expanding-art_df-to-Include-Word-and-Sentence-Information)
- [Back Channels](#Back-Channels)
    - [Trial Run](#Trial-Run)
    - [Finding Back Channels](#Finding-Back-Channels)
    - [Back Channels Data Frame](#Back-Channels-Data-Frame)
- [Writing Data Frames to CSV files](#Writing-Data-Frames-to-CSV-files)
- [Analysis](#Analysis)

## About the Corpus
- The Australian Radio Talkback corpus contains raw text files of telephone conversations.
- These conversations include the speaker's role (presenter, expert, or caller), name, and gender.
- The conversations include other verbal cues such as laughter <laugh> and where a speaker says something during another speaker's turn <E1 yeah>. It also notes corrections to the transcription in squirrley brackets {}.

## Discourse Analysis Goals
- commparing speakers by role and gender
- aspects to consider:
    - back channels (yeah, uhhu, that's great!)
    - vocabulary size (avg word length)
    - number of turns, sentences, and words


```python
%pprint
```

    Pretty printing has been turned OFF
    


```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
from nltk.corpus import PlaintextCorpusReader
import pandas as pd
import nltk
import numpy as np
import glob
```


```python
ART_fids=glob.glob('C:\\Users\\sigmo\\Documents\\Data_Science\\Discourse-Analysis-ART-Corpus\\data_files\\AustralianRadioTalkback\\files\\Raw\\*.txt')
```

**Each filename contains 3-5 letters followed by a number. They all end in -raw.txt.**

    ex: ABCE1-raw.txt, NAT4-raw.txt
    
## Getting the Files


```python
# having trouble with glob..

print("There are " + str(len(ART_fids)) + " files in this corpus:") # 26
for x in ART_fids: 
    print(x)
```

    There are 26 files in this corpus:
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\ABCE1-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\ABCE2-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\ABCE3-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\ABCE4-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\ABCNE1-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\ABCNE2-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COME1-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COME2-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COME3-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COME5-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COME6-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COME7-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE1-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE2-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE3-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE4-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE5-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE6-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\COMNE7-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT1-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT2-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT3-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT4-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT6-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT7-raw.txt
    C:\Users\sigmo\Documents\Data_Science\Discourse-Analysis-ART-Corpus\data_files\AustralianRadioTalkback\files\Raw\NAT8-raw.txt
    


```python
dir(ART_fids)
```




    ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']



## Getting the Texts


```python
# Creating a dictionary of each files' text
    # keys = filenames
    
rawtext_dict = {}
for fid in ART_fids:     
    f=open(fid, 'r')  
    last_slash=fid.rindex('\\') # the key will be only the file name, not the entire location
    rawtext_dict[fid[last_slash+1:]] = f.read()
    f.close() 
```


```python
rawtext_dict['ABCE1-raw.txt'][:1000]
# Within this glimpse of the data, the speaker information data format is shown through Presenter 1.
```




    "[Presenter 1: Simon Marnie, M] Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.\n\n[Expert 1: Angus Stewart, M] I guess yeah yeah <laughs>.\n\n[P1] He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twen"



### Original Speaker Data Format in the Raw Text Files

   *There are multiple exceptions to this format that I will address later in the script.*

All speaker information is contained within [ ].

Each first instance of a speaker is in the following order:
    - Speaker Type
        - Presenter, Caller, or Expert
    - Speaker Number
        - the first presenter in a file is Presenter 1, the second presenter is Presenter 2, etc..
    - The Speaker's Name
        - ex: Simon Marnie
    - The Speaker's gender:
        - M / F
    
For every other instance of a speaker's line, the speaker is indicated by P, C, or E followed by their number.
    - Ex: [Presenter 1: Simon Marnie, M] == [P1]


```python
# print(rawtext_dict['NAT4-raw.txt']) # both NAT4-raw.txt and NAT5-raw.txt are contained within this file
# also, Caller 33b: Chris, male <-- fix gender
```

### Splitting NAT4-raw.txt into 2 files

**NAT4-raw.txt and NAT5-raw.txt**


```python
# Modifying the text keys to separate the two radio talk shows from within NAT4-raw.txt to NAT4-raw.txt and NAT5-raw.txt

seg2_start = rawtext_dict['NAT4-raw.txt'].rindex('[Presenter 1')   # Location of last mention of Presenter 1
seg1 = rawtext_dict['NAT4-raw.txt'][:seg2_start]
seg2 = rawtext_dict['NAT4-raw.txt'][seg2_start:]
seg2[:500]

rawtext_dict['NAT4-raw.txt'] = seg1
rawtext_dict['NAT5-raw.txt'] = seg2

files = sorted(rawtext_dict.keys()) # creates an accurate file list (ART_fids is missing NAT5-raw.txt!!)
```




    "[Presenter 1: John Cleary, M] So now it's welcome first to our expert panel. Dr Brian Edgar he is director of theology and public policy for the Evangelical Alliance a mainstream Protestant agency which have a website that canvases electoral issues. Brian welcome <Expert 1: Brian Edgar, M thank you John> to you.\n\n[E1] Thank you very much glad to <P1 Victoria> be here.\n\n[P1] Victoria Kearney is one of the coordinators of a website called PolMin which looks at lobbying for policies in harmony with"



### Trial Run: Splitting Texts by Lines


```python
# How to split lines using regular expressions 
    # some lines appeared to contain \r while most contained \n
import re
foo = "Hello world\n\nhow are you\na new line\r\nanother newline\n"
re.split(r'[\n\r]+', foo)
re.split(r'[\n\r]+', foo.strip())
```




    ['Hello world', 'how are you', 'a new line', 'another newline', '']






    ['Hello world', 'how are you', 'a new line', 'another newline']




```python
# Splitting the texts by line:
    # Trial run on the first 3 files and their first 20 lines:

for fid in files[:3]: # files includes  NAT5-raw.txt
    rawtext = rawtext_dict[fid] # already includes NAT5-raw.txt
    rawlines = re.split(r'[\n\r]+', rawtext.strip())[:20]
#     print(fid)
    for l in rawlines:
        if ']' in l:
            where = l.index(']')
            speaker = l[:where+1]
            utterance = l[where+2:]
#             print(speaker+' '+utterance)
        else: 
#             print('***'+l+'******')    # {program advert}. What to do with these? 
            pass
#     print()
```

## Data Cleaning
**Fixing Formatting Errors**


```python
# Data Cleaning:

rawtext_dict['ABCE4-raw.txt'] = rawtext_dict['ABCE4-raw.txt'].replace('[E2]', '[E1]')

# There is no E2 in this segment, but E2 is erroneously mentioned. Replacing. 

# $ grep Expert  ABCE4-raw.txt 
# [Expert 1: Ric Nattrass, M] Uh blue-tongues'd be {break} unlikely ...

# $ grep E2  ABCE4-raw.txt 
# [E2] Yeah.
# [E2] Yeah okay so your yours up there is the spotted catbird if you're on <C3 mm> ...


rawtext_dict['COME2-raw.txt'] = rawtext_dict['COME2-raw.txt'].replace('[C5: Jenny, F]', '[Caller 5: Jenny, F]')


# $ grep "C5" COME2-raw.txt 
# [C5: Jenny, F] Hello how are you.
# [C5] That's good. Um I was just wondering for some information on my house at ...
# [C5] Oh have I.

rawtext_dict['ABCE3-raw.txt'] = rawtext_dict['ABCE3-raw.txt'].replace('[Caller 11, Robyn, F]', '[Caller 11: Robyn, F]')
rawtext_dict['COME1-raw.txt'] = rawtext_dict['COME1-raw.txt'].replace('[Caller 23, Maureen, F]', '[Caller 23: Maureen, F]')
rawtext_dict['NAT7-raw.txt'] = rawtext_dict['NAT7-raw.txt'].replace('[Caller 12, Brian, M]', '[Caller 12: Brian, M]')
rawtext_dict['NAT8-raw.txt'] = rawtext_dict['NAT8-raw.txt'].replace('[Caller 10, Brett, M]', '[Caller 10: Brett, M]')

rawtext_dict['NAT4-raw.txt'] = rawtext_dict['NAT4-raw.txt'].replace('[Caller 33b: Chris, male]', '[Caller 33b: Chris, M]')


# $ grep -P 'Caller \d+,' *
# ABCE3-raw.txt:[Caller 11, Robyn, F] Hi um I read the book quite a while ago and ...
# COME1-raw.txt:[Caller 23, Maureen, F] Yes good morning.
# NAT7-raw.txt:[Caller 12, Brian, M] Yeah.
# NAT8-raw.txt:[Caller 10, Brett, M] How're you going.


rawtext_dict['COME3-raw.txt'] = rawtext_dict['COME3-raw.txt'].replace('[Caller 9 Maureen, F]', '[Caller 9: Maureen, F]')

# $ grep -P '\[\S+ \d+ ' *
# COME3-raw.txt:[Caller 9 Maureen, F] Good morning Dr Graham.


rawtext_dict['COME3-raw.txt'] = rawtext_dict['COME3-raw.txt'].replace('[CE1]', '[E1]')

# $ grep CE1 *
# COME3-raw.txt:[CE1] If it did become serious <,> 


rawtext_dict['COME6-raw.txt'] = rawtext_dict['COME6-raw.txt'].replace('P1a', 'P1')
rawtext_dict['COME6-raw.txt'] = rawtext_dict['COME6-raw.txt'].replace('[P1b Paul Murray, M]', '[P1]').replace('P1b', 'P1')

# COME6 presenter encoding scheme was generally messed up.


rawtext_dict['COMNE4-raw.txt'] = rawtext_dict['COMNE4-raw.txt'].replace('[C14: Noelene, F]', '[Caller 14: Noelene, F]')

rawtext_dict['NAT1-raw.txt'] = rawtext_dict['NAT1-raw.txt'].replace('[C11]', '[C10]')

rawtext_dict['NAT5-raw.txt'] = rawtext_dict['NAT5-raw.txt'].replace('[E1] Thank you very much glad to', '[Expert 1: Brian Edgar, M] Thank you very much glad to')
rawtext_dict['NAT5-raw.txt'] = rawtext_dict['NAT5-raw.txt'].replace('<Expert 1: Brian Edgar, M thank you John>', '<E1 thank you John>')

rawtext_dict['COME3-raw.txt'] = rawtext_dict['COME3-raw.txt'].replace('[C4 Nah <E1 it ih thi> and because','[C4] Nah <E1 it ih thi> and because')
rawtext_dict['COME3-raw.txt'] = rawtext_dict['COME3-raw.txt'].replace('[E1 No no no <P1 we haven\'t had one> we','[E1] No no no <P1 we haven\'t had one> we')

# This is Marianna's only line - her speach is untranscribed: therefore I will skip her as a speaker
# print(rawtext_dict['NAT7-raw.txt'])
# rawtext_dict['NAT7-raw.txt'] = rawtext_dict['NAT7-raw.txt'].replace('{Caller 2: Marianna, F untranscribed overseas caller 04:32-07:18}','[Caller 2: Marianna, F untranscribed overseas caller 04:32-07:18]')

# print(rawtext_dict['COME3-raw.txt'])
rawtext_dict['COME3-raw.txt'] = rawtext_dict['COME3-raw.txt'].replace('of\ncholesterol excess cigarette smoking and of course a lack of exercise and uh central truncal obesity','of cholesterol excess cigarette smoking and of course a lack of exercise and uh central truncal obesity')

rawtext_dict['COME1-raw.txt'] = rawtext_dict['COME1-raw.txt'].replace('remember the name\n<inaudible> chrysanthemums','remember the name <inaudible> chrysanthemums')

# grep -P "Juicy" "COME6-raw.txt"
rawtext_dict['COME6-raw.txt'] = rawtext_dict['COME6-raw.txt'].replace('from a beautiful name called Juicy.\n\nJuicy.','from a beautiful name called Juicy. Juicy.')

# discovered while word and sentence tokenizing -- I was looking at all items within { } and < > so that I could remove them for the tokenization
# and saw that in this line, P1 is quoting Michelle, and the quote is inside { } -- I decided to remove the { } since it is still P1 speaking. I also added a period at the end.

# grep -P '{Hi Linda I have a Chinese lucky' 'COME1-raw.txt'
rawtext_dict['COME1-raw.txt'] = rawtext_dict['COME1-raw.txt'].replace("{Hi Linda I have a Chinese lucky bamboo that is looking very sick. It is kept in a narrow glass vase with glass rocks the roots appear to be orange and the smell of the water is disgusting <E1 laughs>. I have two shoots one is yellow half way up the stem the other appears to be okay. The leaves are wilting and yellow can I save my plant love Michelle}","Hi Linda I have a Chinese lucky bamboo that is looking very sick. It is kept in a narrow glass vase with glass rocks the roots appear to be orange and the smell of the water is disgusting <E1 laughs>. I have two shoots one is yellow half way up the stem the other appears to be okay. The leaves are wilting and yellow can I save my plant love Michelle.") 

# discovered while looking through speaker_df: COME5-E2, Kate's name begins with the numbres (a time?) 33:16
# grep -P "33:16 Kate" "COME5-raw.txt"
rawtext_dict['COME5-raw.txt'] = rawtext_dict['COME5-raw.txt'].replace("[Expert 2: 33:16 Kate Curzon, F]","[Expert 2: Kate Curzon, F]")

# discovered while looking at back channels: 
    # ABCNE2-raw.txt: C8 mislabeled as C18
rawtext_dict['ABCNE2-raw.txt'] = rawtext_dict['ABCNE2-raw.txt'].replace("[E1] Um to kill ivy look um blackberry and tree killer <C18 yeah>","[E1] Um to kill ivy look um blackberry and tree killer <C8 yeah>")
    # COME1-raw.txt: C22 mislabeled as C32
rawtext_dict['COME1-raw.txt'] = rawtext_dict['COME1-raw.txt'].replace("keep him off it for a a week which is <C32 inaudible> sometimes difficult but yeah probably","keep him off it for a a week which is <C22 inaudible> sometimes difficult but yeah probably")
    # COME3-raw.txt: C8 mislabeled as E8 (talking to E1)
rawtext_dict['COME3-raw.txt'] = rawtext_dict['COME3-raw.txt'].replace("the medication that you're taking is doing any good <E8 yes>. But you are at risk."," the medication that you're taking is doing any good <C8 yes>. But you are at risk.")

# Eddie, Caller 7 in NAT8-raw.txt
    # first mention is a back channel - change to C7
rawtext_dict['NAT8-raw.txt'] = rawtext_dict['NAT8-raw.txt'].replace("Let's talk to Eddie in Brisbane now g'day Eddie <Caller 7: Eddie, M hey how you going Gab>. Thanks","Let's talk to Eddie in Brisbane now g'day Eddie <C7 hey how you going Gab>. Thanks f")
    # first full line, speaker information 
rawtext_dict['NAT8-raw.txt'] = rawtext_dict['NAT8-raw.txt'].replace("[C7] That's right mate they're all from England or Scotland Ireland or Welsh I mean my my grandfather","[Caller 7: Eddie, M] That's right mate they're all from England or Scotland Ireland or Welsh I mean my my grandfather")

# <E1mm> has no space, P1 is reading and his text is in { } 
rawtext_dict['COMNE4-raw.txt'] = rawtext_dict['COMNE4-raw.txt'].replace("[P1] Oh dear. Here we go {a picture of an unhappy happy plant I had to cut} <E1mm> { its head off as I was having} <E1 laughs> {a pergola built}. Ruthless {and it was in the way it was too tall could you please tell me if I can cut it into a few pieces and} <E1 mm> {grow them. I've still got about three foot of the existing plant still in the place it was also could you tell me if I can cut my hibiscus back it's getting just too big} you've seen those haven't you.","[P1] Oh dear. Here we go a picture of an unhappy happy plant I had to cut <E1 mm> its head off as I was having <E1 laughs> a pergola built. Ruthless and it was in the way it was too tall could you please tell me if I can cut it into a few pieces and <E1 mm> grow them. I've still got about three foot of the existing plant still in the place it was also could you tell me if I can cut my hibiscus back it's getting just too big you've seen those haven't you.")

# Caller 33a not Caller 33
rawtext_dict['NAT4-raw.txt'] = rawtext_dict['NAT4-raw.txt'].replace("Uh <C33 laughs> the uh that is uh Sweet Corn. Suh someone <C33 ah> some somebody gave me","Uh <C33a laughs> the uh that is uh Sweet Corn. Suh someone <C33a ah> some somebody gave me")
rawtext_dict['NAT4-raw.txt'] = rawtext_dict['NAT4-raw.txt'].replace("that dangling I think <C33 yeah> twenty-three what what is the name of the","that dangling I think <C33a yeah> twenty-three what what is the name of the")
rawtext_dict['NAT4-raw.txt'] = rawtext_dict['NAT4-raw.txt'].replace("Men are from Mars Women are from Venus <C33 I>. They made an absolute stack out of it.","Men are from Mars Women are from Venus <C33a I>. They made an absolute stack out of it.")
rawtext_dict['NAT4-raw.txt'] = rawtext_dict['NAT4-raw.txt'].replace("[P1] Mm <C33 Alinghi> and it's and it's uh it's had a","[P1] Mm <C33a Alinghi> and it's and it's uh it's had a")

# missing space again
rawtext_dict['NAT7-raw.txt'] = rawtext_dict['NAT7-raw.txt'].replace("An organic fruit <C7because I'm a> juicer.","An organic fruit <C7 because I'm a> juicer.")

```


```python
# Looking at all {...} lines to find errors.
# The above cell accounts for the errors found here

for fid in files:
    rawtext = rawtext_dict[fid]
    rawlines = re.split(r'[\n\r]+', rawtext.strip())
#     print(fid)
    for l in rawlines:
        if ']' in l:
            where = l.index(']')
            speaker = l[:where+1]
            utterance = l[where+2:]
#             print(speaker+' '+utterance)
        else: 
#             print('***'+l+'*****')    # {program advert}. What to do with these? 
            pass
#     print()
```

## Speaker Information
### Creating Unique Speaker Ids


```python
foo1 = "[Presenter 1: Simon Marnie, M]"
foo2 = "[Expert 1: Les, M]"
foo3 = "[Caller 10: Suzanne, F]"

def get_speaker(fid, sp):
    seg = fid[:-8]  # ABCE3-raw.txt -> ABCE3
    col = sp.index(':')
    
    if sp.startswith('[Presenter') :
        name = sp[col+2:-4].strip()
        return (seg+'-P'+sp[11:col], seg, 'P', sp[-2].upper(), name)
    elif sp.startswith('[Expert') :
        name = sp[col+2:-4].strip()
        return (seg+'-E'+sp[8:col], seg, 'E', sp[-2].upper(), name)
    elif sp.startswith('[Caller') :
        name = sp[col+2:-4].strip()
        return (seg+'-C'+sp[8:col], seg, 'C', sp[-2].upper(), name)
    else:
        return ()
get_speaker('ABCE3-raw.txt', foo1)
get_speaker('COMNE7-raw.txt', foo2)
get_speaker('ABCE3-raw.txt', foo3)
```




    ('ABCE3-P1', 'ABCE3', 'P', 'M', 'Simon Marnie')






    ('COMNE7-E1', 'COMNE7', 'E', 'M', 'Les')






    ('ABCE3-C10', 'ABCE3', 'C', 'F', 'Suzanne')



### Speaker Dictionary
**speaker_dict**

- Key: unique speaker ID
- Values:
    - segment (ex: ABCE1, ABCE2, etc..)
    - role (P/C/E)
    - gender (F/M)
    - name
    
**NOTE: speaker_dict will be used to create the data frame speaker_df**    


```python
# Creating a dictionary for each unique speaker

speaker_dict = {}

for fid in files: # includes NAT5-raw.txt
    rawtext = rawtext_dict[fid]
    rawlines = re.split(r'[\n\r]+', rawtext.strip())
#     print(fid)
    for l in rawlines:
        if ']' in l:
            where = l.index(']')
            speaker = l[:where+1]
            if speaker.startswith('[Presenter') or speaker.startswith('[Expert') or speaker.startswith('[Caller'):
                #print(speaker)
                (uniq_id, seg, role, gender, name) = get_speaker(fid, speaker)
#                 print(uniq_id, seg, role, gender, name)
                speaker_dict[uniq_id] = (seg, role, gender, name)
        else: 
            #print('***'+l)    # {program advert}. What to do with these? 
            pass
#     print()
```


```python
# looking at each item in speaker_dict:

# for s in sorted(speaker_dict):
#     print (s, speaker_dict[s]) 
len(sorted(speaker_dict))
```




    430



### Speaker Data Frame
**speaker_df**


```python
speaker_df = pd.DataFrame(columns=['Segment', 'Speaker_Type', 'Gender', 'Name'], index=sorted(speaker_dict.keys()))
speaker_df.head()
speaker_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NAT8-C6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NAT8-C7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NAT8-C8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NAT8-C9</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
speaker_df['Segment'] = speaker_df.index.map(lambda x: speaker_dict[x][0])
speaker_df['Speaker_Type'] = speaker_df.index.map(lambda x: speaker_dict[x][1])
speaker_df['Gender'] = speaker_df.index.map(lambda x: speaker_dict[x][2])
speaker_df['Name'] = speaker_df.index.map(lambda x: speaker_dict[x][3])
speaker_df.head()
speaker_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Suzanne</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Beth</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lynne</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>M</td>
      <td>Jack</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lisa</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NAT8-C6</th>
      <td>NAT8</td>
      <td>C</td>
      <td>F</td>
      <td>Britney</td>
    </tr>
    <tr>
      <th>NAT8-C7</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Eddie</td>
    </tr>
    <tr>
      <th>NAT8-C8</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Peter</td>
    </tr>
    <tr>
      <th>NAT8-C9</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Michael</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>Gaby Brown</td>
    </tr>
  </tbody>
</table>
</div>




```python
speaker_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NAT8-C6</th>
      <td>NAT8</td>
      <td>C</td>
      <td>F</td>
      <td>Britney</td>
    </tr>
    <tr>
      <th>NAT8-C7</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Eddie</td>
    </tr>
    <tr>
      <th>NAT8-C8</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Peter</td>
    </tr>
    <tr>
      <th>NAT8-C9</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Michael</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>Gaby Brown</td>
    </tr>
  </tbody>
</table>
</div>



## Splitting the Texts by Line

### List of Each Line of Text
**art_list**

- unique speaker id for the line (ex: ABCE1-P1)
- utterance number of the *file*
- segment (ex: ABCE1)
- role (P/C/E)
- gender (M/F)
- line of text

**NOTE: art_list will be used to create the data frame art_df**


```python
speaker_dict["NAT8-C7"]
```




    ('NAT8', 'C', 'M', 'Eddie')




```python
# Creating a list of all the lines of text including the unique speaker id, utterance number (of the file), segment, and text line
    
art_list = []

for fid in files:
    rawtext = rawtext_dict[fid]
    rawlines = re.split(r'[\n\r]+', rawtext.strip())
#     print(fid)
    utterance_num = 0
    for l in rawlines:
        if ']' in l:
            where = l.index(']')
            speaker = l[:where+1]
            utterance = l[where+2:]
            if speaker.startswith('[Presenter') or speaker.startswith('[Expert') or speaker.startswith('[Caller'):
                (uniq_id, seg, role, gender, name) = get_speaker(fid, speaker)
            else:
#                 print(l)
                seg = fid[:-8] # removes "-raw.txt"
                uniq_id = seg+'-'+speaker[1:-1]   # ex: ABCE1-C1
                (seg, role, gender, name) = speaker_dict[uniq_id]
            utterance_num += 1
            art_list.append((uniq_id, utterance_num, seg, role, gender, utterance))
        else: 
#             print('***'+l)    # {program advert}. What to do with these? 
            pass
```


```python
# Examples from art_list:

art_list[0] # starts with ABCE1-raw.txt
art_list[1]
art_list[2]
art_list[3]
art_list[-1] # ends with NAT8-raw.txt
```




    ('ABCE1-P1', 1, 'ABCE1', 'P', 'M', "Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.")






    ('ABCE1-E1', 2, 'ABCE1', 'E', 'M', 'I guess yeah yeah <laughs>.')






    ('ABCE1-P1', 3, 'ABCE1', 'P', 'M', "He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twenty-seven and Katoomba twenty-five degrees currently around town on the coast it's seventeen that's four below <,> r Richmond and Bankstown are fifteen degrees Penrith sixteen Katoomba thirteen and Gosford twelve. One of the jewels in the open garden scheme crown is opening today and this is just a garden to envy how would you like <,> to have <,> a beautiful sandstone cottage nestled underneath a waterfall with a little pond and then a creek that runs through with thousands of water dragons so tame they come up and just <,> kiss you. Would you like to live there.")






    ('ABCE1-E1', 4, 'ABCE1', 'E', 'M', 'Okay.')






    ('NAT8-C17', 363, 'NAT8', 'C', 'M', "Um and now that last caller I was just gunna say the thing about what you say uh I don't think you should really look at people as if n n they're tools that can be used for you but anyway I think it comes down to that like in this country we have uh like we're just lucky to be born here basically we're lucky to be and it's just by chance that you end up here Australia isn't uh Australia needs to like ignore their like uh commercial news outlets that don't show you what happens in the rest of the world but you need to look out and you need to like maybe meet some of the people who've been in these situations. And we can't comprehend what kind of hell they've been through. And then we bring 'em here 'n' we put 'em in jail. 'N' make it worse. And so I think it just comes down to looking at yourself and going well am I glad that I'm in this country do I know how good it <inaudible>.")



### Text Lines Data Frame
**art_df**

Content reminder:
- unique speaker ID
- utterance number
- segment
- role
- gender
- line of text

**Note: The Data Frame will be indexed by unique speaker and the utterance number of the corresponding file.**


```python
# art_df = pd.DataFrame(columns=['Speaker', 'Utterance_Number', 'Segment', 'Speaker_Type', 'Gender', 'Text'], data=art1+art2+art3+art4+art5+art6+art7+art8+art9+art10)
art_df = pd.DataFrame(columns=['Speaker', 'Utterance_Number', 'Segment', 'Speaker_Type', 'Gender', 'Text'], data=art_list)
art_df.head()
art_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
      <td>1</td>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Thanks for that John Hall now John Hall will b...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
      <td>2</td>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>I guess yeah yeah &lt;laughs&gt;.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-P1</td>
      <td>3</td>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>He's also known &lt;E1 sounds reasonable&gt; for his...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-E1</td>
      <td>4</td>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>Okay.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-P1</td>
      <td>5</td>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Jeanne Villani does and we'll find out the sec...</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9024</th>
      <td>NAT8-C16</td>
      <td>359</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Thanks for that.</td>
    </tr>
    <tr>
      <th>9025</th>
      <td>NAT8-P1</td>
      <td>360</td>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>Uh let's see if we can just squeeze in one mor...</td>
    </tr>
    <tr>
      <th>9026</th>
      <td>NAT8-C17</td>
      <td>361</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Um okay yeah thanks for that Gaby.</td>
    </tr>
    <tr>
      <th>9027</th>
      <td>NAT8-P1</td>
      <td>362</td>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>That's alright.</td>
    </tr>
    <tr>
      <th>9028</th>
      <td>NAT8-C17</td>
      <td>363</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Um and now that last caller I was just gunna s...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sets the index to the speaker and utterance number

art_df = art_df.set_index(keys=["Speaker","Utterance_Number"])
art_df.head()
art_df.tail() 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <th>1</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Thanks for that John Hall now John Hall will b...</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>2</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>I guess yeah yeah &lt;laughs&gt;.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>3</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>He's also known &lt;E1 sounds reasonable&gt; for his...</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>4</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>Okay.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>5</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Jeanne Villani does and we'll find out the sec...</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NAT8-C16</th>
      <th>359</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Thanks for that.</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <th>360</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>Uh let's see if we can just squeeze in one mor...</td>
    </tr>
    <tr>
      <th>NAT8-C17</th>
      <th>361</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Um okay yeah thanks for that Gaby.</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <th>362</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>That's alright.</td>
    </tr>
    <tr>
      <th>NAT8-C17</th>
      <th>363</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Um and now that last caller I was just gunna s...</td>
    </tr>
  </tbody>
</table>
</div>



## Adding Number of Utterances per Speaker to the Speaker Data Frame


```python
# utterance dictionary
utt_dict=dict(art_df.groupby("Speaker").size())
# for s in sorted(utt_dict):
#     print (s, utt_dict[s]) 
(len(sorted(utt_dict)))
```




    430




```python
# Reminder what speaker_df looks like:
speaker_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Suzanne</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Beth</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lynne</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>M</td>
      <td>Jack</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lisa</td>
    </tr>
  </tbody>
</table>
</div>




```python
utt_df = pd.DataFrame(columns=['Number_of_Utterances'], index=sorted(utt_dict.keys()))
utt_df['Number_of_Utterances'] = utt_df.index.map(lambda x: utt_dict[x])
utt_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>10</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>12</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
# For this cell, I referenced Kyle Landin's project for his use of pd.merge

speaker_df=pd.merge(speaker_df,utt_df,right_index=True,left_index=True)
```


```python
speaker_df.head()
speaker_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Suzanne</td>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Beth</td>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lynne</td>
      <td>10</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>M</td>
      <td>Jack</td>
      <td>12</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lisa</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NAT8-C6</th>
      <td>NAT8</td>
      <td>C</td>
      <td>F</td>
      <td>Britney</td>
      <td>15</td>
    </tr>
    <tr>
      <th>NAT8-C7</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Eddie</td>
      <td>8</td>
    </tr>
    <tr>
      <th>NAT8-C8</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Peter</td>
      <td>13</td>
    </tr>
    <tr>
      <th>NAT8-C9</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Michael</td>
      <td>11</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>Gaby Brown</td>
      <td>188</td>
    </tr>
  </tbody>
</table>
</div>



## Creating Separate Presenter, Caller, and Expert Data Frames


```python
# dataframe of presenters
P_df=speaker_df.loc[speaker_df["Speaker_Type"]=='P',:]
P_df.head()

# dataframe of callers
C_df=speaker_df.loc[speaker_df["Speaker_Type"]=='C',:]
C_df.head()

# dataframe of experts
E_df=speaker_df.loc[speaker_df["Speaker_Type"]=='E',:]
E_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Simon Marnie</td>
      <td>155</td>
    </tr>
    <tr>
      <th>ABCE2-P1</th>
      <td>ABCE2</td>
      <td>P</td>
      <td>M</td>
      <td>Simon Marnie</td>
      <td>233</td>
    </tr>
    <tr>
      <th>ABCE3-P1</th>
      <td>ABCE3</td>
      <td>P</td>
      <td>F</td>
      <td>Lynne Haultain</td>
      <td>129</td>
    </tr>
    <tr>
      <th>ABCE3-P2</th>
      <td>ABCE3</td>
      <td>P</td>
      <td>F</td>
      <td>Jurate Sasnaitis</td>
      <td>56</td>
    </tr>
    <tr>
      <th>ABCE4-P1</th>
      <td>ABCE4</td>
      <td>P</td>
      <td>F</td>
      <td>Kelly Higgins-Devine</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Suzanne</td>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Beth</td>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lynne</td>
      <td>10</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>M</td>
      <td>Jack</td>
      <td>12</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lisa</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-E1</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>Angus Stewart</td>
      <td>139</td>
    </tr>
    <tr>
      <th>ABCE1-E2</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>F</td>
      <td>Jeanne Villani</td>
      <td>27</td>
    </tr>
    <tr>
      <th>ABCE2-E1</th>
      <td>ABCE2</td>
      <td>E</td>
      <td>M</td>
      <td>Les</td>
      <td>192</td>
    </tr>
    <tr>
      <th>ABCE2-E2</th>
      <td>ABCE2</td>
      <td>E</td>
      <td>M</td>
      <td>Pete</td>
      <td>166</td>
    </tr>
    <tr>
      <th>ABCE2-E3</th>
      <td>ABCE2</td>
      <td>E</td>
      <td>M</td>
      <td>John Hall</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
speaker_df["Speaker_Type"].value_counts().reindex(["P","C","E"])
```




    P     31
    C    362
    E     37
    Name: Speaker_Type, dtype: int64



## Calculating Average Sentence and Word Lengths by Speaker Type


```python
# art_list content reminder:
art_list[0]

for x in art_list[:2]:
    print(x[5])
```




    ('ABCE1-P1', 1, 'ABCE1', 'P', 'M', "Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.")



    Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.
    I guess yeah yeah <laughs>.
    


```python
# How to replace part of a string using regular expressions (re.sub):

# help(re)
help(re.sub)

foo = "mary {had} a <little> lamb"

re.sub(r' <.*?>','',foo)
re.sub(r' {.*?}','',foo)
# re.findall(r'<.*?>',foo)
# re.findall(r'{.*?}',foo)
```

    Help on function sub in module re:
    
    sub(pattern, repl, string, count=0, flags=0)
        Return the string obtained by replacing the leftmost
        non-overlapping occurrences of the pattern in string by the
        replacement repl.  repl can be either a string or a callable;
        if a string, backslash escapes in it are processed.  If it is
        a callable, it's passed the match object and must return
        a replacement string to be used.
    
    




    'mary {had} a lamb'






    'mary a <little> lamb'




```python
# Checking the contents of { } and < > before ignoring them
squir = []
for x in art_list:
    if re.findall(r'{.*?}',x[5]):
        squir.append([x[0],x[1],re.findall(r'{.*?}',x[5])]) # addressed issue with COME1-raw.txt line in the Data Cleaning Cell
# print(squir)

carr = []
for x in art_list:
    if re.findall(r'<.*?>',x[5]):
        carr.append(re.findall(r'<.*?>',x[5])) # addressed issue with COME1-raw.txt line in the Data Cleaning Cell
# print(carr)
```

### Trial Run Word and Sentence Tokeninzation


```python
# Trial run on the first two lines:
word_toks = []
sents = []

for x in art_list[:2]:
    line = x[5]
    print(line)
    
    line = re.sub(r' <.*?>','',line)
    line = re.sub(r' {.*?}','',line) # for now, removing all spelling corrections
    
    print(line)
    
    speaker=x[0]
    utt_num=x[1]
    
    # for now, including the speaker and utterance number of the file to make sure that word_toks and sents line up with art_df's indices
    word_toks.append([speaker,utt_num,nltk.word_tokenize(line)]) 
    sents.append([speaker,utt_num,nltk.sent_tokenize(line)])  
    
word_toks
sents
```

    Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.
    Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.
    I guess yeah yeah <laughs>.
    I guess yeah yeah.
    




    [['ABCE1-P1', 1, ['Thanks', 'for', 'that', 'John', 'Hall', 'now', 'John', 'Hall', 'will', 'be', 'listening', 'for', 'the', 'next', 'hour', "'cos", 'Angus', 'Stewart', 'is', 'here', 'to', 'take', 'your', 'calls', 'eight-triple-three-one-thousand', 'one-eight-hundred-eight-hundred-seven-oh-two', 'something', 'in', 'the', 'garden', 'that', "'s", 'causing', 'you', 'problems', 'give', 'us', 'a', 'call', 'right', 'now', 'and', 'Angus', 'can', 'I', 'mean', "y'know", 'he', 'is', 'known', 'in', 'the', 'trade', 'as', 'Mr', 'popergation', 'Mr', 'propagation', '.', 'He', "'s", 'also', 'known', 'for', 'his', 'passion', 'for', 'natives', 'and', 'his', 'love', 'of', 'o', 'orchids', 'am', 'I', 'right', 'so', 'far', '.']], ['ABCE1-E1', 2, ['I', 'guess', 'yeah', 'yeah', '.']]]






    [['ABCE1-P1', 1, ["Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation Mr propagation.", "He's also known for his passion for natives and his love of o orchids am I right so far."]], ['ABCE1-E1', 2, ['I guess yeah yeah.']]]



### Word and Sentence Tokenization


```python
speaker_df.loc["COME6-C4"]
```




    Segment                 COME6
    Speaker_Type                C
    Gender                      M
    Name                    Ruben
    Number_of_Utterances        3
    Name: COME6-C4, dtype: object




```python
# Word and Sentence Tokenziation:
word_toks = []
sents = []
num_words = []
num_sents = []
avg_word_len = []

for x in art_list:
    word_len=0
    
    line = x[5]

    # regular expressions
    line = re.sub(r'<.*?>','',line)
    line = re.sub(r'{.*?}','',line) # for now, removing all spelling corrections
    
    # tokenizing and calculating the length
    word_toks_1 = nltk.word_tokenize(line)
    sents_1 = nltk.sent_tokenize(line)
    num_words_1 = len(word_toks_1)
    num_sents_1 = len(sents_1)

    # COME6-C7 Ruben's first line is <inaudible>, but all items within < > were removed, resulting in a length of 0
        # this loop sets all 0 values to "NaN" <- This only occurs in Ruben's line.
    if num_words_1==0 or num_sents_1==0:
#         num_words_1 = "NaN"
#         num_sents_1 = "NaN"
        num_words_1 = 1
        num_sents_1 = 1
   
    # finding the average word length for the line
    for word in word_toks_1:
        word_len+=len(word)
    
    # average word length for the line
        # skips Ruben
#     if num_words_1 != "NaN":
#         avg_word_len.append(word_len/num_words_1)
#     else: 
#         avg_word_len.append("NaN")

    avg_word_len.append(word_len/num_words_1)

    # appending to the lists of word tokens, sentences, and number of words
    word_toks.append(word_toks_1)
    sents.append(sents_1)    
    num_words.append(num_words_1)
    num_sents.append(num_sents_1)
    
# checking the lists
print("Word Tokens:")
word_toks[:5]
len(word_toks)

print("\nNumber of Words:")
num_words[:5]
len(num_words)

print("\nAverage Word Length:")
avg_word_len[:10]
len(avg_word_len)

print("\nSentences:")
sents[:20]
len(sents)

print("\nNumber of Sentences:")
num_sents[:20]
len(num_sents)
```

    Word Tokens:
    




    [['Thanks', 'for', 'that', 'John', 'Hall', 'now', 'John', 'Hall', 'will', 'be', 'listening', 'for', 'the', 'next', 'hour', "'cos", 'Angus', 'Stewart', 'is', 'here', 'to', 'take', 'your', 'calls', 'eight-triple-three-one-thousand', 'one-eight-hundred-eight-hundred-seven-oh-two', 'something', 'in', 'the', 'garden', 'that', "'s", 'causing', 'you', 'problems', 'give', 'us', 'a', 'call', 'right', 'now', 'and', 'Angus', 'can', 'I', 'mean', "y'know", 'he', 'is', 'known', 'in', 'the', 'trade', 'as', 'Mr', 'popergation', 'Mr', 'propagation', '.', 'He', "'s", 'also', 'known', 'for', 'his', 'passion', 'for', 'natives', 'and', 'his', 'love', 'of', 'o', 'orchids', 'am', 'I', 'right', 'so', 'far', '.'], ['I', 'guess', 'yeah', 'yeah', '.'], ['He', "'s", 'also', 'known', 'for', 'his', 'ability', 'to', 'open', 'cosposting', 'toilets', 'so', 'he', 'can', 'tell', 'you', 'anything', 'worm', 'farm', 'problems', 'certainly', 'helped', 'us', 'and', 'although', 'I', "'m", 'still', 'confused', 'about', 'dry', 'ingredients', 'we', 'might', 'talk', 'about', 'that', 'as', 'well', 'but', 'eight-triple-three-one-thousand', 'one-eight-hundred-eight-hundred-seven-oh-two', 'fine', 'sunny', 'day', 'today', 'top', 'temperatures', 'on', 'the', 'coast', 'of', 'twenty-seven', 'inland', 'thirty', 'degrees', 'Bowral', 'enjoying', 'twenty-seven', 'and', 'Katoomba', 'twenty-five', 'degrees', 'currently', 'around', 'town', 'on', 'the', 'coast', 'it', "'s", 'seventeen', 'that', "'s", 'four', 'below', 'r', 'Richmond', 'and', 'Bankstown', 'are', 'fifteen', 'degrees', 'Penrith', 'sixteen', 'Katoomba', 'thirteen', 'and', 'Gosford', 'twelve', '.', 'One', 'of', 'the', 'jewels', 'in', 'the', 'open', 'garden', 'scheme', 'crown', 'is', 'opening', 'today', 'and', 'this', 'is', 'just', 'a', 'garden', 'to', 'envy', 'how', 'would', 'you', 'like', 'to', 'have', 'a', 'beautiful', 'sandstone', 'cottage', 'nestled', 'underneath', 'a', 'waterfall', 'with', 'a', 'little', 'pond', 'and', 'then', 'a', 'creek', 'that', 'runs', 'through', 'with', 'thousands', 'of', 'water', 'dragons', 'so', 'tame', 'they', 'come', 'up', 'and', 'just', 'kiss', 'you', '.', 'Would', 'you', 'like', 'to', 'live', 'there', '.'], ['Okay', '.'], ['Jeanne', 'Villani', 'does', 'and', 'we', "'ll", 'find', 'out', 'the', 'secret', 'of', 'her', 'open', 'garden', 'and', 'give', 'you', 'the', 'address', 'so', 'that', 'you', 'can', 'go', 'along', 'today', 'and', 'tomorrow', 'to', 'see', 'Waterfall', 'Cottage', 'which', 'is', 'a', 'part', 'of', 'the', 'open', 'garden', 'scheme', 'all', 'this', 'and', 'more', 'because', 'it', 'is', 'Saturday', '.']]






    9029



    
    Number of Words:
    




    [80, 5, 159, 2, 50]






    9029



    
    Average Word Length:
    




    [4.7, 3.0, 5.062893081761007, 2.5, 3.98, 8.692307692307692, 3.0, 2.5, 2.6666666666666665, 2.9]






    9029



    
    Sentences:
    




    [["Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation  Mr propagation.", "He's also known for his passion for natives and his love of o orchids am I right so far."], ['I guess yeah yeah .'], ["He's also known  for his ability to open cosposting  toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twenty-seven and Katoomba twenty-five degrees currently around town on the coast it's seventeen that's four below  r Richmond and Bankstown are fifteen degrees Penrith sixteen Katoomba thirteen and Gosford twelve.", 'One of the jewels in the open garden scheme crown is opening today and this is just a garden to envy how would you like  to have  a beautiful sandstone cottage nestled underneath a waterfall with a little pond and then a creek that runs through with thousands of water dragons so tame they come up and just  kiss you.', 'Would you like to live there.'], ['Okay.'], ["Jeanne Villani does and we'll find out the secret of her open garden and give you the address so that you can go along today and tomorrow to see Waterfall Cottage which is a part of the open garden scheme all this and more because it is Saturday."], ["Eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two Suzanne's on the line in McMahon's Point and."], ['Hello.'], ['How are you.'], ["I'm good thank you."], ["You've got a big fat  Morton Bay fig."], ["Well it's not that bit it's um it's about three feet 'cos I only know feet .", "About three feet high and um it's been doing so well my partner actually grew it from a seed we picked it up in a church garden  and our intention was to buy a house and plant it but we haven't got the house yet.", "So we've still got the fig and it's doing so well until recently.", "My um I think it's under stress God knows why  it's only on a balcony in a pot but it's getting a sort first of all I thought it was sunburn but the the leaves are getting oh um a pale ring and then after a while they crack .", "And  and then they break off first of all I thought oh golly it's a bug or something eating it.", "But no it seems to be happening as they're growing they're perfectly fine and then intermittently they get this it's it's as if somebody has um um put some hydrogen peroxide on them or something and then."], ['Is there plenty of drainage in the pot.'], ["Yes uhuh um plenty I'm just wondering well obviously it's gotta come out of the pot and be planted in   a proper place but."], ["You think it's a case of Free Willy it wants to just go into the  into the open."], ["It does 'cos it's meant."], ["I don't know Angus is that the case."], ['Well the symptoms you describe um it it sounds could it possibly be water stress.', 'Do you think the plant could be drying out from time to time.'], ["Yeah well it could be maybe I'm not giving it enough."], ["Yeah they uh I mean they are a a rainforest tree that that's used to fairly constant moisture and and mulch y'know plenty of leaf mulch uh froh in the natural sort of environment um."], ['Should I feed it some more.', 'Ih feed it .']]






    9029



    
    Number of Sentences:
    




    [2, 1, 3, 1, 1, 1, 1, 1, 1, 1, 6, 1, 1, 1, 1, 1, 2, 1, 1, 2]






    9029




```python
# art_df content reminder:
art_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <th>1</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Thanks for that John Hall now John Hall will b...</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>2</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>I guess yeah yeah &lt;laughs&gt;.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>3</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>He's also known &lt;E1 sounds reasonable&gt; for his...</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>4</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>Okay.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>5</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Jeanne Villani does and we'll find out the sec...</td>
    </tr>
  </tbody>
</table>
</div>



### Expanding art_df to Include Word and Sentence Information
- word tokens 
- number of words
- average word length
- sentences
- number of sentences


```python
# Adding Data Frame columns:

art_df["Word_Toks"] = word_toks
art_df["Num_Words"] = num_words
art_df["Avg_Word_Length"] = avg_word_len
art_df["Sents"] = sents
art_df["Num_Sents"] = num_sents
art_df.head()
art_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
      <th>Word_Toks</th>
      <th>Num_Words</th>
      <th>Avg_Word_Length</th>
      <th>Sents</th>
      <th>Num_Sents</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <th>1</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Thanks for that John Hall now John Hall will b...</td>
      <td>[Thanks, for, that, John, Hall, now, John, Hal...</td>
      <td>80</td>
      <td>4.700000</td>
      <td>[Thanks for that John Hall now John Hall will ...</td>
      <td>2</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>2</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>I guess yeah yeah &lt;laughs&gt;.</td>
      <td>[I, guess, yeah, yeah, .]</td>
      <td>5</td>
      <td>3.000000</td>
      <td>[I guess yeah yeah .]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>3</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>He's also known &lt;E1 sounds reasonable&gt; for his...</td>
      <td>[He, 's, also, known, for, his, ability, to, o...</td>
      <td>159</td>
      <td>5.062893</td>
      <td>[He's also known  for his ability to open cosp...</td>
      <td>3</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>4</th>
      <td>ABCE1</td>
      <td>E</td>
      <td>M</td>
      <td>Okay.</td>
      <td>[Okay, .]</td>
      <td>2</td>
      <td>2.500000</td>
      <td>[Okay.]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>5</th>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
      <td>Jeanne Villani does and we'll find out the sec...</td>
      <td>[Jeanne, Villani, does, and, we, 'll, find, ou...</td>
      <td>50</td>
      <td>3.980000</td>
      <td>[Jeanne Villani does and we'll find out the se...</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Text</th>
      <th>Word_Toks</th>
      <th>Num_Words</th>
      <th>Avg_Word_Length</th>
      <th>Sents</th>
      <th>Num_Sents</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NAT8-C16</th>
      <th>359</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Thanks for that.</td>
      <td>[Thanks, for, that, .]</td>
      <td>4</td>
      <td>3.50000</td>
      <td>[Thanks for that.]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <th>360</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>Uh let's see if we can just squeeze in one mor...</td>
      <td>[Uh, let, 's, see, if, we, can, just, squeeze,...</td>
      <td>32</td>
      <td>3.53125</td>
      <td>[Uh let's see if we can just squeeze in one mo...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>NAT8-C17</th>
      <th>361</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Um okay yeah thanks for that Gaby.</td>
      <td>[Um, okay, yeah, thanks, for, that, Gaby, .]</td>
      <td>8</td>
      <td>3.50000</td>
      <td>[Um okay yeah thanks for that Gaby.]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>NAT8-P1</th>
      <th>362</th>
      <td>NAT8</td>
      <td>P</td>
      <td>F</td>
      <td>That's alright.</td>
      <td>[That, 's, alright, .]</td>
      <td>4</td>
      <td>3.50000</td>
      <td>[That's alright.]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>NAT8-C17</th>
      <th>363</th>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
      <td>Um and now that last caller I was just gunna s...</td>
      <td>[Um, and, now, that, last, caller, I, was, jus...</td>
      <td>200</td>
      <td>3.49000</td>
      <td>[Um and now that last caller I was just gunna ...</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
speaker_df["Gender"].value_counts().reindex(["M","F"])
```




    M    218
    F    212
    Name: Gender, dtype: int64



## Back Channels 
### Trial Run


```python
# # Regular Expressions - Trial run with back channels: 

bk_chnl_list = []
bk_chnls = []

foo=art_list[:20]
# foo[:3]

for x in foo:
    
    speaker=x[0]
    utt=x[1]
    segment=x[2]
    role=x[3]
    gender=x[4]
    line=x[5]
    
    print(speaker)
    print(utt)
    print(segment)
    print(gender)
    print(line)
    
#     re.findall(r'<.*?>',line)) # includes <,>, <inaudible>, <laughs>, etc... but these are not back channels
    re.findall(r'<[PCE]+[0-9]+.*?>',line)

    bk_chnl_list.append(re.findall(r'<[PCE]+[0-9]+.*?>',line)) # every instance of a < > containing a different speaker
    
#     print("speaker:")
#     found = re.findall(r'<[PCE]+[0-9]+',line) # includes < 

    for b in bk_chnl_list[-1]:
    # a for loop to remove '<' from the other speakers list and replace with the segment (creating unique speaker ID):
    
        b=str(b) # CONVERT TO STRING FOR NEXT FOR LOOP
#         print("STRINGY",b)
#         print("BKchan",str(bk_chnl_list[-1]))
        b_index=bk_chnl_list[-1].index(b)
#         bk_chnl_list[-1]
        
#         print(b_index)
        space=b.index(" ")
#             bk_chnl_list[-1][b_index]=b.replace('<',segment+"-")
        channel = b[space+1:-1]
        channel_speaker = segment+"-"+b[1:space]
        channel_role = b[1]
        channel_gen = speaker_df.loc[channel_speaker]["Gender"]
#             bk_chnl_list[-1][b_index].replace(b,[speaker,utt,segment,channel_speaker,channel])

        bk_chnls.append([channel_speaker,channel_role,channel_gen,channel,speaker,utt,segment,role,gender])
#         bk_chnls[-1]
        
bk_chnl_list
bk_chnls
```

    ABCE1-P1
    1
    ABCE1
    M
    Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.
    




    []



    ABCE1-E1
    2
    ABCE1
    M
    I guess yeah yeah <laughs>.
    




    []



    ABCE1-P1
    3
    ABCE1
    M
    He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twenty-seven and Katoomba twenty-five degrees currently around town on the coast it's seventeen that's four below <,> r Richmond and Bankstown are fifteen degrees Penrith sixteen Katoomba thirteen and Gosford twelve. One of the jewels in the open garden scheme crown is opening today and this is just a garden to envy how would you like <,> to have <,> a beautiful sandstone cottage nestled underneath a waterfall with a little pond and then a creek that runs through with thousands of water dragons so tame they come up and just <,> kiss you. Would you like to live there.
    




    ['<E1 sounds reasonable>']



    ABCE1-E1
    4
    ABCE1
    M
    Okay.
    




    []



    ABCE1-P1
    5
    ABCE1
    M
    Jeanne Villani does and we'll find out the secret of her open garden and give you the address so that you can go along today and tomorrow to see Waterfall Cottage which is a part of the open garden scheme all this and more because it is Saturday.
    




    []



    ABCE1-P1
    6
    ABCE1
    M
    Eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two Suzanne's on the line in McMahon's Point and.
    




    []



    ABCE1-C1
    7
    ABCE1
    F
    Hello.
    




    []



    ABCE1-P1
    8
    ABCE1
    M
    How are you.
    




    []



    ABCE1-C1
    9
    ABCE1
    F
    I'm good thank you.
    




    []



    ABCE1-P1
    10
    ABCE1
    M
    You've got a big fat <C1 laughs> Morton Bay fig.
    




    ['<C1 laughs>']



    ABCE1-C1
    11
    ABCE1
    F
    Well it's not that bit it's um it's about three feet 'cos I only know feet <P1 yes>. About three feet high and um it's been doing so well my partner actually grew it from a seed we picked it up in a church garden <E1 mm> and our intention was to buy a house and plant it but we haven't got the house yet. So we've still got the fig and it's doing so well until recently. My um I think it's under stress God knows why <E1 mm> it's only on a balcony in a pot but it's getting a sort first of all I thought it was sunburn but the the leaves are getting oh um a pale ring and then after a while they crack <E1 mm>. And <,> and then they break off first of all I thought oh golly it's a bug or something eating it. But no it seems to be happening as they're growing they're perfectly fine and then intermittently they get this it's it's as if somebody has um um put some hydrogen peroxide on them or something and then.
    




    ['<P1 yes>', '<E1 mm>', '<E1 mm>', '<E1 mm>']



    ABCE1-P1
    12
    ABCE1
    M
    Is there plenty of drainage in the pot.
    




    []



    ABCE1-C1
    13
    ABCE1
    F
    Yes uhuh um plenty I'm just wondering well obviously it's gotta come out of the pot and be planted in <,> <P1 mm> a proper place but.
    




    ['<P1 mm>']



    ABCE1-P1
    14
    ABCE1
    M
    You think it's a case of Free Willy it wants to just go into the <C1 mhm> into the open.
    




    ['<C1 mhm>']



    ABCE1-C1
    15
    ABCE1
    F
    It does 'cos it's meant.
    




    []



    ABCE1-P1
    16
    ABCE1
    M
    I don't know Angus is that the case.
    




    []



    ABCE1-E1
    17
    ABCE1
    M
    Well the symptoms you describe um it it sounds could it possibly be water stress. Do you think the plant could be drying out from time to time.
    




    []



    ABCE1-C1
    18
    ABCE1
    F
    Yeah well it could be maybe I'm not giving it enough.
    




    []



    ABCE1-E1
    19
    ABCE1
    M
    Yeah they uh I mean they are a a rainforest tree that that's used to fairly constant moisture and and mulch y'know plenty of leaf mulch uh froh in the natural sort of environment um.
    




    []



    ABCE1-C1
    20
    ABCE1
    F
    Should I feed it some more. Ih feed it <inaudible>.
    




    []






    [[], [], ['<E1 sounds reasonable>'], [], [], [], [], [], [], ['<C1 laughs>'], ['<P1 yes>', '<E1 mm>', '<E1 mm>', '<E1 mm>'], [], ['<P1 mm>'], ['<C1 mhm>'], [], [], [], [], [], []]






    [['ABCE1-E1', 'E', 'M', 'sounds reasonable', 'ABCE1-P1', 3, 'ABCE1', 'P', 'M'], ['ABCE1-C1', 'C', 'F', 'laughs', 'ABCE1-P1', 10, 'ABCE1', 'P', 'M'], ['ABCE1-P1', 'P', 'M', 'yes', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-P1', 'P', 'M', 'mm', 'ABCE1-C1', 13, 'ABCE1', 'C', 'F'], ['ABCE1-C1', 'C', 'F', 'mhm', 'ABCE1-P1', 14, 'ABCE1', 'P', 'M']]



### Finding Back Channels


```python
# How to locate specific items in a data frame:
    # I will use this to find the gender of the back channel speaker
speaker_df.head()
speaker_df.loc["ABCE1-C1","Gender"]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Segment</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Name</th>
      <th>Number_of_Utterances</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Suzanne</td>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Beth</td>
      <td>17</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lynne</td>
      <td>10</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>M</td>
      <td>Jack</td>
      <td>12</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
      <td>Lisa</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>






    'F'




```python
art_list[:5]
```




    [('ABCE1-P1', 1, 'ABCE1', 'P', 'M', "Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far."), ('ABCE1-E1', 2, 'ABCE1', 'E', 'M', 'I guess yeah yeah <laughs>.'), ('ABCE1-P1', 3, 'ABCE1', 'P', 'M', "He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twenty-seven and Katoomba twenty-five degrees currently around town on the coast it's seventeen that's four below <,> r Richmond and Bankstown are fifteen degrees Penrith sixteen Katoomba thirteen and Gosford twelve. One of the jewels in the open garden scheme crown is opening today and this is just a garden to envy how would you like <,> to have <,> a beautiful sandstone cottage nestled underneath a waterfall with a little pond and then a creek that runs through with thousands of water dragons so tame they come up and just <,> kiss you. Would you like to live there."), ('ABCE1-E1', 4, 'ABCE1', 'E', 'M', 'Okay.'), ('ABCE1-P1', 5, 'ABCE1', 'P', 'M', "Jeanne Villani does and we'll find out the secret of her open garden and give you the address so that you can go along today and tomorrow to see Waterfall Cottage which is a part of the open garden scheme all this and more because it is Saturday.")]




```python
# Regular Expressions - back channels: 

bk_chnl_list = []
bk_chnls = []

for x in art_list:
    
    speaker=x[0]
    utt=x[1]
    segment=x[2]
    role=x[3]
    gender=x[4]
    line=x[5]
    
    # sometimes there are 2 speakers in 1 back channel (ex: <P1 and E1 laugh>)
    bk_chnl_list.append(re.findall(r'<[PCE]+[0-9]+.*?>',line)) # every instance of a < > containing a different speaker than the line's speaker

    for b in bk_chnl_list[-1]:
    # a for loop to remove '<' from the other speakers list and replace with the segment (creating unique speaker ID):

        b=str(b) # CONVERT TO STRING FOR NEXT FOR LOOP
        b_index=bk_chnl_list[-1].index(b)
        
        # finding all back channels with multiple speakers
        if re.findall(r'and [PCE]+[0-9]+',b):
#             print(b)
            
            # NOTE: the 2-speaker back channels are all only one word (laugh or yes)
            # so the right space separates the speakers from the back channels
            
            # space separating the speakers from the back channel (one word)
            rspace = b.rindex(" ")
            # space after the first speaker
            lspace = b.index(" ")
            
            # extracting the back channel
            channel = b[rspace+1:-1]
            
            # separating the 2 speakers, giving them their unique speakekr identities, and saving their roles 
            speaker1 = segment+"-"+b[1:lspace]
            speaker1_role = b[1]
            speaker2 = segment+"-"+b[lspace+5:rspace]
            speaker2_role = b[lspace+5:rspace-1]
            
            # the 2 channel speakers' genders
            speaker1_gen = speaker_df.loc[speaker1]["Gender"]
            speaker2_gen = speaker_df.loc[speaker2]["Gender"]
            
            # Self-Check
#             print(channel)
#             print(speaker1)
#             print(speaker1_role)
#             print(speaker1_gen)
#             print(speaker2)
#             print(speaker2_role)
#             print(speaker2_gen)
            
            # appending the separate back channels to the overall list
            bk_chnls.append([speaker1,speaker1_role,speaker1_gen,channel,speaker,utt,segment,role,gender])
            bk_chnls.append([speaker2,speaker2_role,speaker2_gen,channel,speaker,utt,segment,role,gender])
            
        else:
            
            # space separating the speaker from the back channel
            space=b.index(" ")
            
            # extracting the back channel, speaker, and role 
            channel = b[space+1:-1]
            channel_speaker = segment+"-"+b[1:space]
            channel_role = b[1]
            
            # finding back channel speaker gender
            channel_gen = speaker_df.loc[channel_speaker]["Gender"]
            
            # appending the back channels to the overall list
            bk_chnls.append([channel_speaker,channel_role,channel_gen,channel,speaker,utt,segment,role,gender])
        
len(bk_chnl_list)
len(bk_chnls)
bk_chnls[:20]
bk_chnls[-20:]
```




    9029






    4646






    [['ABCE1-E1', 'E', 'M', 'sounds reasonable', 'ABCE1-P1', 3, 'ABCE1', 'P', 'M'], ['ABCE1-C1', 'C', 'F', 'laughs', 'ABCE1-P1', 10, 'ABCE1', 'P', 'M'], ['ABCE1-P1', 'P', 'M', 'yes', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 11, 'ABCE1', 'C', 'F'], ['ABCE1-P1', 'P', 'M', 'mm', 'ABCE1-C1', 13, 'ABCE1', 'C', 'F'], ['ABCE1-C1', 'C', 'F', 'mhm', 'ABCE1-P1', 14, 'ABCE1', 'P', 'M'], ['ABCE1-C1', 'C', 'F', 'uh', 'ABCE1-E1', 23, 'ABCE1', 'E', 'M'], ['ABCE1-E1', 'E', 'M', 'mhm', 'ABCE1-C1', 24, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'laugh', 'ABCE1-C1', 24, 'ABCE1', 'C', 'F'], ['ABCE1-C1', 'C', 'F', 'laugh', 'ABCE1-C1', 24, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'mm', 'ABCE1-C1', 24, 'ABCE1', 'C', 'F'], ['ABCE1-E1', 'E', 'M', 'yeah', 'ABCE1-C1', 30, 'ABCE1', 'C', 'F'], ['ABCE1-C1', 'C', 'F', 'mm', 'ABCE1-E1', 31, 'ABCE1', 'E', 'M'], ['ABCE1-C1', 'C', 'F', 'yes', 'ABCE1-E1', 31, 'ABCE1', 'E', 'M'], ['ABCE1-C1', 'C', 'F', 'inaudible', 'ABCE1-E1', 35, 'ABCE1', 'E', 'M'], ['ABCE1-C1', 'C', 'F', 'laugh', 'ABCE1-E1', 35, 'ABCE1', 'E', 'M'], ['ABCE1-E1', 'E', 'M', 'laugh', 'ABCE1-E1', 35, 'ABCE1', 'E', 'M'], ['ABCE1-P1', 'P', 'M', 'hundred years', 'ABCE1-E1', 44, 'ABCE1', 'E', 'M']]






    [['NAT8-P1', 'P', 'F', 'inaudible', 'NAT8-C14', 321, 'NAT8', 'C', 'M'], ['NAT8-C14', 'C', 'M', 'bye', 'NAT8-P1', 328, 'NAT8', 'P', 'F'], ['NAT8-P1', 'P', 'F', 'mhm', 'NAT8-C15', 333, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C15', 335, 'NAT8', 'C', 'F'], ['NAT8-C15', 'C', 'F', 'so', 'NAT8-P1', 336, 'NAT8', 'P', 'F'], ['NAT8-P1', 'P', 'F', 'mhm', 'NAT8-C15', 337, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'yeah', 'NAT8-C15', 339, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C15', 341, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'mhm', 'NAT8-C15', 341, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C15', 341, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'tt', 'NAT8-C15', 341, 'NAT8', 'C', 'F'], ['NAT8-P1', 'P', 'F', 'yeah', 'NAT8-C15', 341, 'NAT8', 'C', 'F'], ['NAT8-C15', 'C', 'F', 'bye', 'NAT8-P1', 346, 'NAT8', 'P', 'F'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C16', 351, 'NAT8', 'C', 'M'], ['NAT8-P1', 'P', 'F', 'sighs', 'NAT8-C16', 351, 'NAT8', 'C', 'M'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C16', 351, 'NAT8', 'C', 'M'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C16', 351, 'NAT8', 'C', 'M'], ['NAT8-P1', 'P', 'F', 'mhm', 'NAT8-C16', 353, 'NAT8', 'C', 'M'], ['NAT8-P1', 'P', 'F', 'yeah', 'NAT8-C16', 353, 'NAT8', 'C', 'M'], ['NAT8-P1', 'P', 'F', 'mm', 'NAT8-C16', 353, 'NAT8', 'C', 'M']]



During this process, I found 3 more errors in the transcription, where speakers listed as the speakers of a back channel did
not exist, because there was a typo. This means that there are likely more typos, but that the typo is a speaker that does exist.

### Back Channels Data Frame
**bk_df**

The first 4 columns are the new information about the back channel: 
- back channel speaker
- back channel speaker type
- back channel speaker gender
- back channel

The last 5 columns are the information from art_df about the line that the back channel comes from:
- line speaker
- segment's utterance nubmer 
- segment
- line's speaker type
- line's speaker gender


```python
bk_df=pd.DataFrame(columns=["Speaker","Speaker_Type","Speaker_Gender","Back_Channel","Line_Speaker","Segment_Utterance_Number","Segment","Line_Speaker_Type","Line_Speaker_Gender"], data=bk_chnls)
bk_df.head()
bk_df.tail() # still has an inaudible, but it was spoken by someone besides the line's speaker
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
      <th>Speaker_Type</th>
      <th>Speaker_Gender</th>
      <th>Back_Channel</th>
      <th>Line_Speaker</th>
      <th>Segment_Utterance_Number</th>
      <th>Segment</th>
      <th>Line_Speaker_Type</th>
      <th>Line_Speaker_Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-E1</td>
      <td>E</td>
      <td>M</td>
      <td>sounds reasonable</td>
      <td>ABCE1-P1</td>
      <td>3</td>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-C1</td>
      <td>C</td>
      <td>F</td>
      <td>laughs</td>
      <td>ABCE1-P1</td>
      <td>10</td>
      <td>ABCE1</td>
      <td>P</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-P1</td>
      <td>P</td>
      <td>M</td>
      <td>yes</td>
      <td>ABCE1-C1</td>
      <td>11</td>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-E1</td>
      <td>E</td>
      <td>M</td>
      <td>mm</td>
      <td>ABCE1-C1</td>
      <td>11</td>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-E1</td>
      <td>E</td>
      <td>M</td>
      <td>mm</td>
      <td>ABCE1-C1</td>
      <td>11</td>
      <td>ABCE1</td>
      <td>C</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
      <th>Speaker_Type</th>
      <th>Speaker_Gender</th>
      <th>Back_Channel</th>
      <th>Line_Speaker</th>
      <th>Segment_Utterance_Number</th>
      <th>Segment</th>
      <th>Line_Speaker_Type</th>
      <th>Line_Speaker_Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4641</th>
      <td>NAT8-P1</td>
      <td>P</td>
      <td>F</td>
      <td>mm</td>
      <td>NAT8-C16</td>
      <td>351</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4642</th>
      <td>NAT8-P1</td>
      <td>P</td>
      <td>F</td>
      <td>mm</td>
      <td>NAT8-C16</td>
      <td>351</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4643</th>
      <td>NAT8-P1</td>
      <td>P</td>
      <td>F</td>
      <td>mhm</td>
      <td>NAT8-C16</td>
      <td>353</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4644</th>
      <td>NAT8-P1</td>
      <td>P</td>
      <td>F</td>
      <td>yeah</td>
      <td>NAT8-C16</td>
      <td>353</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4645</th>
      <td>NAT8-P1</td>
      <td>P</td>
      <td>F</td>
      <td>mm</td>
      <td>NAT8-C16</td>
      <td>353</td>
      <td>NAT8</td>
      <td>C</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>



## Writing Data Frames to CSV files

Because I am not allowed to distribute the data, these csv files are sent to my data_files folder, whose contents are not visible on GitHub.


```python
# Writing data frames to CSV files
speaker_df.to_csv("data_files/Speakers.csv")
art_df.to_csv("data_files/Texts.csv")
bk_df.to_csv("data_files/Back_Channels.csv")
```

## Analysis
This concludes the construction of the 3 data frames. The analysis can be found in a separate file, [analysis.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.ipynb).
