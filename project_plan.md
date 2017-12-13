Alicia Sigmon

als333@pitt.edu

10/01/2017

# Plan for Discourse Analysis:

## Data:

### [Australian Radio Talkback Corpus:](https://www.ausnc.org.au/corpora/art)

	- 27 transcribed recordings of samples of national, regional and commercial Australian talkback radio from 2004 to 2006.
		- text: does not contain speaker information
		- raw
			- Speaker Information [Type+Number: Name, Gender]: 
				- Speaker Type (Presenter, Caller, Expert)
				- Speaker Number
					- order in which speakers appear in the file
					- the first presenter in a file is Presenter 1, the second presenter is Presenter 2, etc..
				- Name
				- Gender (M/F)
			- laughter <>
			- overlapping speech (back channels) <>
			- commas <,>
			- spelling corrections {}
			- program advertisements, breaks, and music {}
	- closed data - cannot create a new license or distribute the data
 
## Project Goals:	

I would like to look at the following:

	- word and sentence length by speaker role and gender *(if genders are distributed evenly across roles)*
	- number of turns by speaker role and gender *(if genders are distributed evenly across roles)*
	- back channels
		- "Yeah
		- "Uh hu"
		- laughter

## Analysis:

These analyses will be divided by gender and speaker type

	- number of utterances (turns) 
	- average number of utterances (turns)
	- number of sentences and words
	- avg word length
	- avg sentence length
	- distrubtion of backchannels
		- speaker 
	- most common back channels

### Questions and Hypotheses:

	- who takes most number of turns? 
		- hypothesis: Presenter
	- who talks the most?	
		- hypothesis: Presenter
	- who uses the most advanced vocabulary? 
		- hypothesis: Expert
	- are men or women more likely to utter back channels while someone of the same gender is speaking?
		- hypotheses: women will utter more back channels while men are talking, and men will utter more back channels while men are talking.
 
### Methods:

	- create 3 pandas data frames
		- one with the texts
		- one with the speaker information
		- one with backchannels
	- nltk.word_tokenize and nltk.sent_tokenize
	- regular expressions to extract information from the text, like speaker number and backchannels
	
## Presentation:

	- DataFrames:
		- speaker information, organized by filename-speaker_role+speaker_number
		- texts, organized by speaker and utterance number within each file
		- graphs to display the results of my analysis
	- Bar Graphs