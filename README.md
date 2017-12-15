Alicia Sigmon

als333@pitt.edu

11/02/2017

# Discourse Analysis of the Australian Radio Talkback 

The Australian Radio Talkback Corpus is owned by Macquarie University and can be downloaded [here](https://www.ausnc.org.au/corpora/art).

## Project Summary: 

This project is a discourse analysis of the 27 raw text files in the Australian Radio Talkback Corpus.
These files include speaker information within [], such as the speaker's role (presenter, caller, or expert), their name, and their gender.
They also include back channels and laughter, indicated by <> and spelling corrections and program breaks, indicated by {}.

For this project, I analyzed the texts by speaker type and gender. I looked at the number of turns, number of sentences and words, 
and sentence and word lengths. I also looked at backchannels to see how the speaker's role and gender affect collaboration in conversations.

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
		- contains speaker, speaker type, speaker gender, back channels, the line speaker, the segment utterance number, 
		the filename, the line speaker type, and the line speaker gender
		
## Project Directory
- [.gitignore](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/.gitignore): A file that ignores the folder data_files, which contains all data for this project.
- [README.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/README.md): A summary of the project, and a directory of all files.
- [LICENSE.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/LICENSE.md): MIT License
- [analysis.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.ipynb): The code containing analysis of my data frames.
- [analysis.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/analysis.md): The markdown version of my code for analyzying data frames.
- [final_report.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/final_report.md): My final report, summarizing my analyses.
- [license_notes.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/license_notes.md): How I chose the MIT License for my code.
- [process-art-corpus.ipynb](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/process-art-corpus.ipynb): Creating data frames for the Australian Radio Talkback Corpus.
- [process-art-corpus.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/process-art-corpus.md): The markdown version of my code to create data frames. 
- [progress_report.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/progress_report.md): Progress reports from throughout the course of my project.
- [project_plan.md](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/blob/master/project_plan.md): The plan for the Discourse Analysis.
- [images](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/tree/master/images): A folder of all plots used for analysis.
- [previous_code](https://github.com/Data-Science-for-Linguists/Discourse-Analysis-ART-Corpus/tree/master/previous_code): A folder of code and a csv file that were discarded from this project.
- data_files: This folder contains the data for this project but is hidden due to the [terms of use](https://www.ausnc.org.au/about-1/terms-of-use) 
of the Australian Radio Talkback Corpus.

Please visit my [visitor's log](https://github.com/Data-Science-for-Linguists/Shared-Repo/blob/master/todo10_visitors_log/visitors_log_Alicia.md)
to see others' comments on my project.
