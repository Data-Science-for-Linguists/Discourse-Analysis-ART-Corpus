Alicia Sigmon

als333@pitt.edu

# Discourse Analysis of the Australian Radio Talkback Corpus

## 11/25/17
### First Analysis:
For my first analysis, I first looked at the number of utterances per speaker.
Before I could do this analysis, I needed to calculate each speaker's utterances.
To do this, I created a dictionary of utterances, utt_dict, by using groupy on 
the speaker column in art_df, the data frame of each line of text: 

utt_dict=dict(art_df.groupby("Speaker").size())

I then created utt_df from the dictionary, with the index being the sorted keys from utt_dict. This ensures
that utt_df and speaker_df have the same indices. To combine my utterance data frame, utt_df, with my 
speaker data frame, speaker_df, I referenced Kyle Landin's project for his use of pd.merge to create the following code:

speaker_df=pd.merge(speaker_df,utt_df,right_index=True,left_index=True)

Thus, I added the column Number_of_Utterances to my speaker_df.


## 11/22/17
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