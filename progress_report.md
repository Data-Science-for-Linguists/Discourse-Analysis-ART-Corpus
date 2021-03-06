Alicia Sigmon

als333@pitt.edu

# Discourse Analysis of the Australian Radio Talkback Corpus

## 12/14/17
I have reread my files for typos and organzation, and I believe my project is done for now, but there are many more paths for research with this corpus.
I have a couple of ideas listed in my final report under Section 10, 
[Future Work](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md#10-future-work). 


## 12/13/17 
Today I created markdown versions of all of my code files. I also wrote my [Final Report](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md).
This file contains all of my analyses and summarizes the process of my project. The project is essentially completed. I am struggling to get the TOC links 
to function properly, so I will revisit the project tomorrow to make my last report.

## 12/12/17
I have created the headings for [final_report.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md), 
so I will be writing the overall report tonight and tomorrow.
I have also been working on organazing [process-art-corpus.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/process-art-corpus.ipynb)
and [analysis.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.ipynb) and adding the Table of Contents to both files.

## 12/10/17
*As of today, my repo is **public,** and my original repo has been **removed.***

Today I removed the analysis from process-art-corpus.ipynb, so now process-art-corpus.ipynb creates data frames and the analysis
can be found in analysis.ipynb. I also did a Caller Gender Analysis instead of a Presenter Gender Analysis because the number of 
Males and Females is more equally matched for Callers. 

Finally, I added a Table of Contents to process-art-corpus.ipynb.

Next time I work on this project, I will futher work on analysis.ipynb, add a table of contents, and begin final_report.md.

## 12/07/17
I discovered that I was only looking at the first 10 files when creating art_list. I solved this issue but had to fix many 
transcription errors before my code would fully run again. I also discovered more transcription errors 
that I have fixed and a line that was inaudible. This line resulted in a "division by 0" error while counting average word
length, but I solved this issue by making that cell a word length of 1 and a sentence length of 1. 

I will be re-analyzing the data to see how my conclusions have changed. 

## 12/04/17
### Presentation:
My Presentation is about ready, including a lot of Gender Analyses. I plan to keep my analyses in this new sheet, and to have data compilation
in my process-art-corpus.ipynb, because new script, analysis.ipynb, has an organized analysis, and it will 
be easier to navigate.

Removed from my presentation and replaced with bullets:

Across the corpus, the three speaker types have about the same number of total turns. 
Individual Presenters have on average the most number of turns, while Callers have the fewest.  
So even though there are more callers speaking fewer lines and fewer presenters speaking more lines, 
the corpus is equally represented in regards to the number of turns by speaker type.

Experts have the longest sentences.

## 12/04/17
### Preparing for the Presentation:
I am adding gender to art_df and bk_df so that I can see how gender affects back channels. I would like to have some of this 
for my analysis in the presentation tomorrow. I would like to compare back channels of Presenters by gender.

I discovered a connection today between average sentence length and number of back channels: Experts have the longest sentences,
and the most back channels are uttered while they are speaking. This leads me to believe that longer speech results in more back channels.

I also discovered an error in my code, so some of my back channels were incorrect or missing. The error is now fixed, and my analysis
was unaffected.

### Further Analysis Plans:

- Where do back channels usually go? 
	- How far into the utterance? 
	- after what POS? 
		- stanford parser 
		- lexical items 
			- add columns with preceding and following words
			- put tokenized sentences from art_df or maybe raw texts into standford parser 
			- bigrams before and after what grammatical environment?
- compare lines with back channels and lines without
	- need both to see what differences there are between sentences that include back channels and sentences that don't.
	- **Prediction:** maybe longer lines have back channels and short ones don't
- **More Gender Analysis:** 
	- Look into Language Log: research on interruption times of men vs women
	- Compare back channels of Presenters by gender

## 12/03/17
### Back Channel Analysis:
I have begun my Back Channel Analysis. Callers utter the most back channels, and Experts have the most back 
channels uttered while they are speaking. I was surprised to note that Presenters utter the least number of back channels.
I would expect them to utter more because they are around the entire show. However, because there are so many callers all 
coming into the show at a new point, it also makes sense that they utter many back channels.

To know what these mean, I believe I need to normalize these raw scores in some way. My first attempt was to compare 
the number of back channels of each speaker type to the number of utterances for each speaker type. 

Because each speaker type has about the same number of total turns (~1500), I believe the raw count is acceptable for an analysis.

I had previously missed this in my analysis when looking at number of average turns per speaker type. **Across the corpus, 
the three speaker types have about the same number of total turns. So even though there are more callers speaking fewer lines 
and fewer presenters speaking more lines, the corpus is equally represented in regards to the number of turns by speaker type.**

## 12/01/17
### Back Channel Data Frame:
I have successfully built my back channel data frame, which is called bk_df! I had to split back channels that were uttered by 
2 people at once into separate back channels. These double-speaker back channels were almost always indicating laughter.

## 11/30/17
### Graphs
I am now adding graphs the analyses I have done so far for visualization.

## 11/28/17
### Gender:
I also created data frames for males and females, and discovered that there are 100 females and 60 males.
There are twice as many Female Callers vs Male Callers, but twice as many Male Experts and Presenters vs. Female Experts and Presenters.
This leads me to believe that a gender analysis on word length and sentence length would be too affected by the role of the speakers and 
that I cannot compare males and females in this way. However, seeing that the professionals on the show are mostly male and the callers mostly 
female leads to a conversation about gender equality.


## 11/27/17
The data frame art_df of each line of text now includes word tokens, number of words, average word length, sentences, and number of sentences. 
I added a speaker's role column, *role*, to art_df so that the lines could be grouped by role for my analysis.

### Average Word and Sentence Length:
I analyzed average word length and average sentence length. I found that average word length is not indicative of role, but that sentence length is.
Experts have the longest sentences, and Callers have the shortest sentences.

## 11/26/17
### MIT License:
I chose the MIT License, because it makes my code very open and accessible for future discourse analyses.

### Back Channels:
I also began working with the back channels in < >. I am attempting to locate all back channels using regular expressions.
I also need to create a list of the speaker, which can be the same as the line's speaker or another person in the conversation.

## 11/25/17
### Thinking About Licenses:
I am able to license my code but not any of the data. I would like my code to be open source. It is very helpful for other people who 
decide to analyze the Australian Radio Talkback Corpus, because it fixes transcription errors and organizes the data by line and by speaker.
In considering licenses, I have come across the MIT License and the Mozilla Public License 2.0 (MPL-2.0). I believe the MIT License is potentially 
too vague, and that I will prefer the MPL-2.0, but I will continue reading about the licenses to come to a final, informed decision.


## 11/25/17
### Number of Utterances for Presenters, Callers, and Experts:

*Note: The script described below is also part of process-art-corpus.ipynb*

For my first analysis, I looked at the number of utterances per speaker.
Before I could do this analysis, I needed to calculate each speaker's utterances.
To do this, I created a dictionary of utterances, utt_dict, by using *.groupby* on 
the speaker column in art_df, the data frame of each line of text: 

*utt_dict=dict(art_df.groupby("Speaker").size())*

I then created utt_df from the dictionary, with the index being the sorted keys from utt_dict. This ensures
that utt_df and speaker_df have the same indices. To combine my utterance data frame, utt_df, with my 
speaker data frame, speaker_df, I referenced [Kyle Landin's project](https://github.com/Data-Science-for-Linguists/project_KyleLandin.git) 
for his use of pd.merge to create the following code:

*speaker_df=pd.merge(speaker_df,utt_df,right_index=True,left_index=True)*

Thus, I added the column *Number_of_Utterances* to my speaker_df and could begin an analysis
using speaker_df.
I used *.loc* to split speaker_df into 3 separate data frames by role: P_df (the Presenter data frame),
C_df (the Caller data frame), and E_df (the Expert data frame).

Using *.info*, I discovered that there were 12 Presenters, 134 Callers, and 16 Experts.
I then used the *.describe()* method to compile information about each of the above data frames:

Presenters: 
- 12 people
- average of 122.5 turns per person
- std: 129.38

Callers: 
- 134 people
- average of 11.23 turns per person
- std: 7.97

Experts:
- 16 people
- average of 91.5 turns per person
- std: 86.82


## 11/22/17
### How I created process-art-corpus.ipynb:
The script process-art-corpus.ipynb is now working and does all that reformatting-data.ipynb was attempting to do. 
First I used glob to get all of the filenames. I then created a dictionary of the text for each filename.
Next, I modified the dictionary by splitting NAT4-raw.txt into NAT4-raw.txt and NAT5-raw.txt. (NAT4-raw.txt was 
mistakingly created to contain 2 separate transcriptions, resulting in duplicate unique speaker identities.)

Next, I began working on splitting the texts by line. However, due to many errors in the transcription, I needed
to fix the errors before I could accurately split the lines. I created a cell to fix all errors, adding
errors to the cell as I found them.  I found all lines that did not contain ']', which indicates the end of a 
speaker's line of text, and printed those lines. The cell that fixes errors is placed before the loop that I used to
find many of the errors.

After fixing the errors, I created the function 'get_speaker' to create unique speaker ids.
With the unique speaker ids, I was then able to create a speaker dictionary, speaker_dict. For speaker_dict,
the keys were the unique speaker IDs, and the values included segment (ex: ABCE1, ABCE2, etc..), role (P/C/E), 
gender (M/F), and name (ex: Simon Marnie). 
From speaker_dict I created the data frame speaker_df for visualization.

Later in my script, after creating a data frame containing each line of text, I added the column Number_of_Utterances
to speaker_df.

Next, I split the texts by line. I created the list art_list which contains 
the unique speaker ID of the line (ex: ABCE1-P1), the utterance number of the file, the segment (ex: ABCE1),
and the line of text. I created this list in order to create the data frame art_df for visualization.
However, I needed to transform the list into a numpy array (art_array) before creating the data frame.
I used the unique speaker ID and utterance number of the file as a double index, so that 
each line of text had a unique index.


## 11/19/17
Today I will begin working on a new analysis file called process-art-corpus.ipynb. I realized that making lists of my data was unreliable and causing multiple 
errors; this previous attempt relied on the erroneous assumption that I could create lists of equal lengths and add them to a data frame. 
I need to look at the text through a dictionary. This can be done by creating a dictionary from the raw text with the keys being the file names, 
linked to the text of the individual file. 
There were many errors/fluxuations in transcription, so I will have a cell that accounts for each of these differences.

## 11/13/17
I found the duplicate unique_speaker issue!! Simon Marnie spoke twice, but the other speakers were mislabeled true unique speakers. 
In NAT4-raw.txt, the second half of the file is actually NAT5-raw.txt. It is a new program with new speakers, but starts over with Presenter 1, 
Caller 1, etc. There were 6 new speakers from NAT5-raw.txt. I first adjusted my unique_speaker loop to account for this, and then I adjusted my 
loop from the very beginning of my data re-formatting to change all lines after the new Presenter 1 to list the fileid as NAT5-raw.txt instead of 
NAT4-raw.txt.
Even though that issue is fixed, ABCE1-P1 is still taking lines that are not his. For example, lines that are for NAT8-raw.txt are listed as 
ABCE1-P1's lines. I will look into my loop that calculates utterance numbers in the future to fix this issue.
I also plan to add more markdown cells to explain my code. I've been using a lot of comments, but I will add Markdown cells once I have fixed the
errors in my current code.

## 11/5/17
My project repo is now called "Discourse-Analysis-ART-Corpus."

## 11/2/17
As an organization member, I am not allowed to delete the new repo I created yesterday, so it is currently still on GitHub.
Upon attempting again to create a new repo today, I added my files after my correct .gitignore was in the repo, but it still uploaded my files. 
Therefore, Project-Alicia is still the correct repo and both of my new repos need to be delted.

Along the way I also messed up my Project-Alicia repo and it wouldn't allow me to push, but I fixed that issue.

## 11/1/17
I've found multiple issues in my code that I've been working on fixing. I had changed C33b to Caller 33b, but I put that in the wrong line.
I fixed my loop that creates the unique_speaker lists. I realized using my lists speaker_type and speaker_num wasn't going to work.
By adding regular expressions, I was able to find the real speaker number, and by taking the first letter of each speaker info (C,P,E), 
my loop now runs smoothly.
However, there are more duplicates that I need to find. len(set(unique_speaker)) is 421, but unique_speaker is 428. 
I will have to delve more into my speaker_info to figure out who is listed twice.
I also think that I want to remove the file COME6-raw.txt because it's format is very confusing.
There is a P1a and a P1b that seem to be the same person, but they talk over each other, so I expect that there is an error in the transcription.

I tried to create a new repo because I previously uploaded my files, but this didn't work either so I am still working in Project Alicia.
The problem was that I specified the AustralianRadioTalkback folder within my data_files folder instead of just ignoring everything in the data_files folder.


## 10/29/17
I created multiple dictionaries and lists to store my variables. 
I have the label instead of the full info listed in my DataFrame right now.
I am working on figuring out how to get gender into my DataFrame. I made 3 dictionaries to try and figure out how to do it,
but I am doing all of the restructuring by first creating lists and dictionaries in for loops or list/dictionary comprehension,
so I don't know if this is okay or not. 

## 10/27/2017
I'm updating my Project Plan

## 10/24/2017
Lauren visted our class and helped us look at our data. My data is closed, meaning that I cannot put it online or relicense it.
I began writing my license_notes.md file, and with the discovery above, I cannot write a LICENSE.md file. However, I still have one 
as a place holder that will state who the data is owned by.

I need to restart my repo, because I put my data up before my .gitignore, which is why it always appeared there.
For now I will keep the repo as private and then make a new repo later.

## 10/17/17
The last couple of days I have been:
- reading about discourse analysis
- thinking of ways to organize the data

I think I can look at the following in this corpus:
- back channels
- vocabulary size by speaker role and gender
- topic boundaries <-- this seems a little complicated

Issues:
- are the genders equally distributed?
- some roles have less lines than others
	- presenters talk the whole time
	- callers are only in the conversation for a limited amount of time

Terms of the Corpus:
 "We also grant You permission to download one copy only of a reasonable number of single Items for use by You alone off-line in conjunction with research and study only. This licence does NOT otherwise include the right to copy or reproduce the Material and IN NO CIRCUMSTANCES does it include the right to modify, adapt, distribute, display, transmit, perform or broadcast any Material, or otherwise cause it to be shown or heard in public or its use for any commercial purpose (including commercially exploiting the Material). This permission constitutes a limited licence and may not be, sub-licensed, transferred, assigned, charged or otherwise encumbered by You. Again, you will not have access to Sensitive Material unless You are a Trusted User."	
- This makes it sound like I am not allowed to annotate the corpus?? Hopefully this is not the case but I will discuss this further with NaRae
- I also need to make sure that my .gitignore is working	
	
## 10/16/17
### More Detail on What Led to My Project Plan Change:
I previously did not discuss in these reports all of the work I took to realize that my plan would not work. Here's what happened:
- I worked with the BNC_Baby, Australian Radio Talkback corpus, the australian and uk corpora of 10k written sentences, and the twitter API
- The data was not matched, and I was spread out in too many directions.
- The BNC_Baby corpus was a lot bigger than the ART corpus, and I had very few tweets
Summary of issue: I had a lot of mismatched data that would have made for a poor analysis, so I needed to change project goals

## 10/11/17
I realized that my project plan was not going to work with the data that I was able to attain.
I discussed my concerns with Na-Rae today, and after looking further into the Australian Radio Talkback Corpus, and I will look into discourse analysis in this corpus. 
I haven't previously learned about discourse analysis, so I will begin reading about discourse markers and how to code for discourse markers

### What is included in the Australian Radio Talkback Corpus?
- speaker information and markers
	- in each file, speakers' lines have an individual marker
	- types of speakers:
		- presenters [Presenter 1: Simon Marnie, M] = [P1]
		- experts [Expert 1: Angus Stewart, M] = [E1]
		- callers [Caller 1: Suzanne, F] = [C1]
- transcript corrections following typos {}
- non verbal cues and laughter < > 

### Analysis Ideas
- discourse markers:
	- back-channel
	- questions 
	- non-verbal markers (head nods)
- discourse by gender
- discourse by type of speaker

After reading more about discourse markers, I will have more definied ideas of what to analyze and how to organize my data

## 10/02/17

I have found multiple data sets, including news articles and transcripts from a radio show. 
I also completed my Project Plan today and can begin to move forward with this project.

One big concern I have with this project is whether or not the corpora I have found will be effective for my project.
I do not have pronunciation data, and the oral data I'm looking at is now in the form of transcripts. 

I also want to continue searching for corpora like Twitter corpora which is a very relaxed source of language data that could show more dialectal variation.