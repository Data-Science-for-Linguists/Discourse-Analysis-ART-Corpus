Alicia Sigmon

als333@pitt.edu

12/11/2017

# Final Report

### Table of Contents

- [1. Overview of the Discourse Analysis Project](#1.-Overview-of-the-Discourse-Analysis-Project) 
	- [1.1 Choosing a Topic and Finding Data](#1.1-Choosing-a-Topic-and-Finding-Data)
	- [1.2 The Australian Radio Talkback Corpus](#1.2-The-Australian-Radio-Talkback-Corpus)
		- [1.2.1 Format of the Australian Radio Talkback Corpus Raw Files](#1.2.1-Format-of-the-Australian-Radio-Talkback-Corpus-Raw-Files)
	- [1.3 Discourse Analysis](#1.3-Discourse-Analysis)
	- [1.4 Presentation](#1.4-Presentation)
		- [1.4.1 Data Frames Overview](#1.4.1-Data-Frames-Overview)
		- [1.4.2 Bar Graphs](#1.4.2-Bar-Graphs)
- [2. Choosing a License](#2.-Choosing-a-License)
	- [2.1 The MIT License](#2.1-The-MIT-License)
	- [2.2 Why an Open License?](#2.2-Why-an-Open-License?)
- [3. Reformatting Data](#3.-Reformatting-Data)
	- [3.1 Reading in the Texts](#Reading-in-the-Texts)
		- [3.1.1 Method 1 (Lists)](#3.1-Method-1-(Lists))
		- [3.1.2 Method 2 (Dictionary)](#3.2-Method-2-(Dictionary))
	- [3.2 Unique Speaker IDs](#3.2-Unique-Speaker-IDs)
	- [3.3 Data Frames](#3.3-Data-Frames)
		- [3.3.1 Speaker Data Frame](#Speaker-Data-Frame)
		- [3.3.2 Text Data Frame](#Text-Data-Frame)
		- [3.3.3 Back Channel Data Frame](#Back-Channel-Data-Frame)
- [4. Data Formatting Errors](#4.-Data-Formatting-Errors)
- [Distribution of Speakers by Type and Gender](#Distribution-of-Speakers-by-Type-and-Gender)
- [Speaker Type Analysis](#Speaker-Type-Analysis) 
- [Gender Analysis](#Gender-Analysis)
- [Back Channel Distribution by Speaker Type and Gender](#Back-Channel-Distribution-by-Speaker-Type-and-Gender)
- [Caller Back Channel Analysis](#Caller-Back-Channel-Analysis)
- [Future Work](#Future-Work)

## 1. Overview of the Discourse Analysis Project

Please visit my [Project Plan](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/project_plan.md) 
to see a bulleted version of my plan.

### 1.1 Choosing a Topic and Finding Data

When I originally began this project, my goal was to compare Dialects of English. One of the first data sources that I found was the Australian Radio
Talkback Corpus, which is still used for this project. I also looked at BNC Baby and used the Twitter IPA to scrape tweets from Australia. The work for this
orignal idea can be found in the folder [previous_code](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/tree/master/previous_code).
The code for how I found tweets is in [twitter.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/previous_code/twitter.ipynb)
and my [BNC Baby code](https://render.githubusercontent.com/view/ipynb?commit=6f7f8ef7ec89b5503b8588046a299712bc38dcec&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f366637663865663765633839623535303362383538383034366132393937313262633338646365632f70726576696f75735f636f64652f776f726b696e675f6f6e5f646174612e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=previous_code%2Fworking_on_data.ipynb&repository_id=109528849&repository_type=Repository#BNC) 
and [Australian Radio Talkback Corpus code](https://render.githubusercontent.com/view/ipynb?commit=6f7f8ef7ec89b5503b8588046a299712bc38dcec&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f366637663865663765633839623535303362383538383034366132393937313262633338646365632f70726576696f75735f636f64652f776f726b696e675f6f6e5f646174612e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=previous_code%2Fworking_on_data.ipynb&repository_id=109528849&repository_type=Repository#Australian-Radio-Talkback)
are in the file working_on_data.ipynb.

This file was abandoned part-way through because I realized that I needed to try a new topic and new methods. I then chose to do a Discourse Analysis based off of the 
Australian Radio Talkback Corpus, because it gave speaker information and had a user-friendly format, or so it seemed.

### 1.2 The Australian Radio Talkback Corpus
The [Australian Radio Talkback Corpus](https://www.ausnc.org.au/corpora/art) is freely downloadable for fair use, but is a relatively closed data set. I will 
discuss licensing later in this report, but you may click [here](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md#choosing-a-license) 
to move to Section 1.5 of the report to learn more about the license for the corpus and how I chose the license for my code.
 
The corpus contains 27 raw and text files of transcribed recordings of national, regional, and commercial Australian
Talkback Radio. For this project, I will be using the *raw files,* because the text files do not contain speaker information. 


#### 1.2.1 Format of the Australian Radio Talkback Corpus Raw Files

The first instance of a Speaker in the Corpus is labeled as follows: [SpeakerType+Number: Name, Gender]. 
Each following instance of a speaker has an abbreviated label within a file, which includes their speaker type and number. Presenters are labeled as *P,* Callers
as *C,* and Experts as *E.* For example, in ABCE1-raw.txt, the first speaker is introduced as [Presenter 1: Simon Marnie, M]. When he speaks again, 
he is referred to as [P1]. This method is used in all files.

To see this example from the full text, please click 
[here](https://render.githubusercontent.com/view/ipynb?commit=d7e2875149d7364aab232bff885c8bdfb2e9c10a&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f643765323837353134396437333634616162323332626666383835633862646662326539633130612f70726f636573732d6172742d636f727075732e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=process-art-corpus.ipynb&repository_id=109528849&repository_type=Repository#Getting-the-Texts) 
to visit my code. 

Also contained in the raw text files are spelling corrections, program advertisements, breaks, and music, indicated by curly brackets { }, and 
laughter, pauses, inaudible speech, and overlapping speech, indicated by angle brackets < >. 
For the purpose of this project, I ignored the items within curly brackets. I then looked at
items within angle brackets that were uttered by speakers other than the speaker of the line. I considered all overlapping speech to be a backchannel, though 
some of these "back channels" are really interruptions and should be analyzed separately. For recommendations on future research with information in the 
curly brackets and angle brackets, please 
visit my [Future Work](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md#future-work) section. 

### 1.3 Discourse Analysis
I analyzed aspects of speech like sentence and word length, number of turns, and average number of turns to get an idea of how much the speakers were talking. 
For my main discourse analysis I decided to focus on back channels. Who is uttering back channels, and when are they uttering them? Part of each speaker's identity 
is their role in the talkback radio show and their gender. How do these factors affect the conversation? 

### 1.4 Presentation

#### 1.4.1 Data Frames Overview
In order to be able to do an analysis, I organized the data into 3 main pandas data frames. 
- speaker_df: a data frame of all unique speakers in the corpus
- art_df: a data frame of all lines of text in the corpus
- bk_df: a data frame of all back channels in the corpus

Click [here](https://render.githubusercontent.com/view/ipynb?commit=755bd39beb57f0266c9ad528edaa35107ef6f481&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f373535626433396265623537663032363663396164353238656461613335313037656636663438312f616e616c797369732e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=analysis.ipynb&repository_id=109528849&repository_type=Repository#Data-Frames-Summary) 
to see the completed data frames.

Click [here]() to read in more detail about the data frames.

#### 1.4.2 Bar Graphs
I used bar graphs to create visualizations of speaker distributions across speaker types and speaker genders. I also created bar graphs to show the most common back channels, 
and how back channels differed between men and women. These graphs can be found in the Analysis portions of my report.

## 2. Choosing a License
The Australian Radio Talkback Corpus is a relatively closed corpus with a [limited license](https://www.ausnc.org.au/about-1/terms-of-use), 
and I am using the corpus under the Fair Dealings Policy, which is Section 3.3. Users are allowed to download one copy of the corpus, but are not allowed to re-license the data.
My *data_files* folder is then hidden from GitHub because I am not allowed to redistribute the data. However, if you would like to download the corpus for yourself, you
may do so at the [Australian National Corpus website](https://www.ausnc.org.au/corpora/art). 

At first, I thought I would be unable to license my code due to the strict regulations, but I am able to license my code as long as I am not re-licensing the 
data itself.

To read more about the process of choosing a license, please visit my [License Notes](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/license_notes.md).

### 2.1 The MIT License
The [MIT License](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/LICENSE.md) is an open license 
that will allow others to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies my code.

### 2.2 Why an Open License?
My code is useful because it fixes many errors in transcription and puts the corpus into a useable format for all files. 
Thus, I chose the MIT License because it is open source so that others can expand upon my research to further analyze discourse.

## 3. Reformatting Data
My goal in using data frames was to make the speaker information and lines of text accessable, and to be able to compare the speakers across files. 
To get the data into data frames, I had to figure out the most effective way to retrieve the data. 

### 3.1 Reading in the Texts
First I tried using *lists,* and then I tried a *dictionary,* which was much more effective. 

#### 3.1.1 Method 1 (Lists)
When I first began working with the Australian Radio Talkback Corpus, my methods were flawed. I began with a list of all lines of text, which I called [ART_lines](http://localhost:8888/notebooks/previous_code/reformatting_raw_files.ipynb#Creating-lists-for-data),
where I append each line of data directly from the files. In the following cells, I created for loops that found gender, speaker, speaker type, utterance number, 
and filename for each line and appended those values to new lists.

While the lists were equal lengths, the rows did not line up across lists, and my data format was unreliable. I also found many transcription errors and 
had to modify each list individually to correct the issues. I then decided that a dictionary would be a 
more effective, efficient, and reliable method for storing my data.

#### 3.1.2 Method 2 (Dictionary)
My second attempt involved first appending all the texts into a dictionary, which I called [rawtext_dict](https://render.githubusercontent.com/view/ipynb?commit=552c6aba66aee9b5949eb72b98891cbe82573aa5&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f353532633661626136366165653962353934396562373262393838393163626538323537336161352f70726f636573732d6172742d636f727075732e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=process-art-corpus.ipynb&repository_id=109528849&repository_type=Repository#Getting-the-Texts), 
where the keys were the filenames and the values were the texts. This allowed me to fix transcription errors in the texts themselves instead of working in lists
of fragmented data.

### 3.2 Unique Speaker IDs
As previously discussed in the [Section 1.2.1](#Format-of-the-Australian-Radio-Talkback-Corpus-Raw-Files), each speaker is given a unique ID for within their file.
However, these identifiers do not allow for cross-file analyses. 
For example, Presenter 1 [P1] in ABCE1-raw.txt is Simon Marnie, but Presenter 1 [P1] in COME1-raw.txt is Luke Bona. My code creates a
[Unique Speaker ID ](https://render.githubusercontent.com/view/ipynb?commit=1e1745a4d0843db171a796d80b11785629c48e1e&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f316531373435613464303834336462313731613739366438306231313738353632396334386531652f70726f636573732d6172742d636f727075732e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=process-art-corpus.ipynb&repository_id=109528849&repository_type=Repository#Creating-Unique-Speaker-Ids)
for each speaker in the corpus, corresponding to their speaker type and their file number. 
This transforms the previous two Presenter 1s from [P1] to [ABCE1-P1] and [COME1-P1].

### 3.3 Data Frames
#### 3.3.1 Speaker Data Frame
#### 3.3.2 Text Data Frame
#### 3.3.3 Back Channel Data Frame

## 4. Data Formatting Errors
In transcriptions there is always room for human error. In this corpus, I originally thought that the data would not be difficult to transform into data frames.
However, I discovered that the standard method of introducing speakers varied, and speakers were sometimes even mislabeled in later turns. Similarly, sometimes 
information was in the incorrect type of bracket. I created a single 
[Data Cleaning cell](https://render.githubusercontent.com/view/ipynb?commit=552c6aba66aee9b5949eb72b98891cbe82573aa5&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f353532633661626136366165653962353934396562373262393838393163626538323537336161352f70726f636573732d6172742d636f727075732e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=process-art-corpus.ipynb&repository_id=109528849&repository_type=Repository#Data-Cleaning) 
where I added each new transcription error and fixed them in my dictionary of raw texts. 
This allowed me to append the corrected lines to my lists for the data frames.

NAT4-raw.txt specifically contained 2 files, which I separated into [NAT4-raw.txt and NAT5-raw.txt.](https://render.githubusercontent.com/view/ipynb?commit=1e1745a4d0843db171a796d80b11785629c48e1e&enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f446174612d536369656e63652d666f722d4c696e6775697374732f446973636f757273652d416e616c797369732d4152542d436f727075732f316531373435613464303834336462313731613739366438306231313738353632396334386531652f70726f636573732d6172742d636f727075732e6970796e62&nwo=Data-Science-for-Linguists%2FDiscourse-Analysis-ART-Corpus&path=process-art-corpus.ipynb&repository_id=109528849&repository_type=Repository#Splitting-NAT4-raw.txt-into-2-files) 
The index *NAT4-raw.txt* in the dictionary of raw texts contains the first segement from the original NAT4-raw.txt, and the second segement is under the new key *NAT5-raw.txt.*



## Distribution of Speakers by Type and Gender

## Speaker Type Analysis

## Gender Analysis 

*include Languague Log Article*

## Back Channel Distribution by Speaker Types and Gender

## Caller Back Channel Analysis

## Future Work

1. It would be good to keep curly bracket information so that turns can be analyzed for topic boundaries.
2. Overlapping speech in angle brackets should be sepearted into back channels, laughter, inaudible, and interruptions for analyses.