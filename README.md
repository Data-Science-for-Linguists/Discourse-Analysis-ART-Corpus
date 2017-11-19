### Alicia Sigmon, als333@pitt.edu, 11/02/2017

# Discourse Analysis of the Australian Radio Talkback 

## Summary: 

I will do a discourse analysis of the raw text files in the Australian Radio Talkback Corpus.
These files include speaker information within [], such as the speaker's role (presenter, caller, or expert), their name, and their gender.
They also include back channels and laughter, indicated by <> and spelling corrections and program breaks, indicated by {}.

For this project, I will compare the number of turns, vocabulary size, and number of sentences and words across speaker roles and gender.
I will also look at backchannels, laughter, and interruptions to see how the speaker's role and/or gender affect these aspects of conversation.

### Importance of this script:
- My script fixes the following errors:
	- changes in how speakers' information is introduced.
		- Example format: [Presenter 1: Simon Marnie, M]
	- formatting:
		- NAT4-raw.txt contains NAT5-raw.txt
		- COME6-raw.txt marked Presenter 1 as both P1 and P1b.
- My script gives each speaker a unique identifier, so that speakers can be compared across text files.
- My script creates data frames to compile speaker information, including thier unique identifier, filename, name, speaker type (P/C/E), gender, and number of utterances.
	- I wiill also have a data frame for back channels.