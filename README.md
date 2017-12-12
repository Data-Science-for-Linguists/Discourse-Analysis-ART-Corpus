Alicia Sigmon

als333@pitt.edu

11/02/2017

# Discourse Analysis of the Australian Radio Talkback 

The Australian Radio Talkback Corpus is owned by Macquarie University and can be downloaded [here](https://www.ausnc.org.au/corpora/art).

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
		
## Project Directory
- [.gitignore](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/.gitignore): A file that ignores the folder data_files, which contains the Australian Radio Talkback Corpus files and csv files for my data frames.
- [README.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/README.md): A summary of the project, and a directory of all files.
- [LICENSE.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/LICENSE.md): MIT License
- [analysis.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.ipynb): The analysis of my data frames.
- [final_report.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md): My final report, summarizing my analyses.
- [license_notes.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/license_notes.md): How I chose the MIT License for my code.
- [process-art-corpus.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/process-art-corpus.ipynb): Creating data frames for the Australian Radio Talkback Corpus.
- [progress_report.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/progress_report.md): Progress reports from throughout the course of my project.
- [project_plan.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/project_plan.md): The plan for the Discourse Analysis.
- [images](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/tree/master/images): A folder of all plots used for analysis.
	- [back_channels_line_speaker_types.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/back_channel_line_speaker_types.png): A plot of the number of back channels uttered while presenters, callers, and experts were talking.
	- [back_channel_speaker_genders.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/back_channel_speaker_genders.png): A ploto of the number of back channels uttered by males and females.
	- [back_channel_speaker_types.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/back_channel_speaker_types.png): A plot of the number of back channels spoken presenters, callers, and experts.
	- [caller_genders.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/caller_genders.png): A plot of Caller males and females.
	- [expert_genders.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/expert_genders.png): A plot of Expert males and females.
	- [gender_totals.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/gender_totals.png): A plot of all males and females in the corpus.
	- [presenter_genders.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/presenter_genders.png): A plot of Presenter males and females.
	- [role_totals.png](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/role_totals.png): A plot of all speakers per speaker type.
	- [top_20_back_channels](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/images/top_20_back_channels.png): A plot of the top 20 most common back channels in the corpus.

- [old_work](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/tree/master/old_work): A folder of Jupyter Notebook files and csv files that were discarded from this project. Originally I looked at tweets, the Australian Radio Talkback Corpus, and BNC Baby:
	- [Australia_Tweets.csv](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/Australia_Tweets.csv): Example Tweets
	- [reformatting_raw_files.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/reformatting_raw_files.ipynb): My first attempt at creating Data Frames for the Australian Radio Talkback Corpus for the Discourse Analysis.
	- [twitter.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/twitter.ipynb): Finding Tweets
	- [working_on_data.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/old_work/working_on_data.ipynb): My first attempt at looking at BNC Baby and the Australian Radio Talkback Corpus.
	

Please visit my [visitor's log](https://github.com/Data-Science-for-Linguists/Shared-Repo/blob/master/todo10_visitors_log/visitors_log_Alicia.md)
to see others' comments on my project.
