Alicia Sigmon

als333@pitt.edu

11/02/2017

# Discourse Analysis of the Australian Radio Talkback 

The Australian Radio Talkback Corpus is owned by Macquarie University and can be downloaded at this website: 
https://www.ausnc.org.au/corpora/art

## Project Summary: 

This project is a discourse analysis of the raw text files in the Australian Radio Talkback Corpus.
These files include speaker information within [], such as the speaker's role (presenter, caller, or expert), their name, and their gender.
They also include back channels and laughter, indicated by <> and spelling corrections and program breaks, indicated by {}.

For this project, I compared did analyses by speaker type and by gender. I looked at the number of turns, number of sentences and words, 
and sentence and word lengths. I also looked at backchannels to see how the speaker's role and gender affect this aspect of conversation.

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
		- contains the unique speaker ID, utterance number within the file, the filename, speaker type, speaker gender, the line of text, word tokens,
		number of words, average word length, sentences, and number of sentences
	- bk_df
		- contains speaker, speaker type, speaker gender, the lines with back channels, the line speaker, the segment utterance number, 
		the filename, the line speaker type, and the line speaker gender
		
## Project Directoryd
- [.gitignore](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/.gitignore)
- [README.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/README.md)
- [LICENSE.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/LICENSE.md)
- [analysis.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.ipynb)
- [license_notes.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/license_notes.md)
- [process-art-corpus.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/process-art-corpus.ipynb)
- [progress_report.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/progress_report.md)
- [project_plan.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/project_plan.md)
- [old_work](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/tree/master/old_work)
	- [Australia_Tweets.csv](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/Australia_Tweets.csv)
	- [reformatting_raw_files.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/reformatting_raw_files.ipynb)
	- [twitter.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/twitter.ipynb)
	- [working_on_data.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/working_on_data.ipynb)
	



Please visit my [visitor's log](https://github.com/Data-Science-for-Linguists/Shared-Repo/blob/master/todo10_visitors_log/visitors_log_Alicia.md)
to see others' comments on my project.
