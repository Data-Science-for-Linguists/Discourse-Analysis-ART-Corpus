Alicia Sigmon

als333@pitt.edu

11/02/2017

# Discourse Analysis of the Australian Radio Talkback 

The Australian Radio Talkback Corpus is owned by Macquarie University and can be downloaded at this website: 
https://www.ausnc.org.au/corpora/art

## Summary: 

I will do a discourse analysis of the raw text files in the Australian Radio Talkback Corpus.
These files include speaker information within [], such as the speaker's role (presenter, caller, or expert), their name, and their gender.
They also include back channels and laughter, indicated by <> and spelling corrections and program breaks, indicated by {}.

For this project, I will compare the number of turns, vocabulary size, and number of sentences and words across speaker roles. I will
also look at the distribution of gender across roles to see if a similar analysis can be done based on gender.
I will also look at backchannels to see how the speaker's role and/or gender affect this aspect of conversation.

Please visit my [visitor's log](https://github.com/Data-Science-for-Linguists/Shared-Repo/blob/master/todo10_visitors_log/visitors_log_Alicia.md)
to see others' comments on my project.

### Importance of this script:
- My script fixes the following errors:
	- variation in how speakers' information is introduced.
		- Example format: [Presenter 1: Simon Marnie, M]
	- formatting:
		- NAT4-raw.txt contains NAT5-raw.txt
		- COME6-raw.txt marked Presenter 1 as both P1 and P1b.
- My script gives each speaker a unique identifier, so that speakers can be compared across text files.
- My script creates the following data frames:
	- speaker_df
		- contains speaker information, including thier unique identifier, filename, name, speaker type (P/C/E), gender, and number of utterances.
	- art_df
		- contains the unique speaker ID, utterance number within the file, the filename, and the line of text
	- bk_chnl_df
		- contains lines with back channels