Alicia Sigmon; als333@pitt.edu; 10/01/2017
Project Plan:

# Discourse Analysis of the Australian Radio Talkback Corpus

## Data
Australian Radio Talkback Corpus: https://www.ausnc.org.au/corpora/art

	- 27 transcribed recordings of samples of national, regional and commercial Australian talkback radio from 2004 to 2006.
		- text: does not contain speaker information
		- raw
			- speaker information [Position+Number: Name, Gender]: 
				- position
					- presenter
					- expert
					- caller
				- number
					- order in which speakers appear in the file
					- presenters, callers, and experts each get their own series of numbers
						- ex: Presenter 1, Expert 1, Presenter 2, Caller 1, etc...
				- name
				- gender
			- laughter <>
			- overlapping speach (back channels) <>
			- commas <,>
			- spelling corrections {}
			- program advertisements, breaks, and music {}
	- closed data - cannot create a new license or distribute the data
 
## Project Goals:	

I would like to look at the following:

	- vocabulary size by speaker role and gender *(if genders are distributed evenly across roles)*
	- number of turns by speaker role and gender *(if genders are distributed evenly across roles)*
	- back channels
	- supervised machine learning?
		- can the computer guess if a sentence was uttered by a presenter, caller, or expert?

## Analysis:

These analyses will be divided by gender and then also speaker type (P, C, or E)

	- number of utterances (turns) 
	- number of sentences and words
	- vocabulary size
		- avg word length
		- TTR
	- number of backchannels or signs of paying attention
		- "Yeah" 
		- "Uh hu" 
		- laughter

### Questions and Hypotheses:

	- who takes most number of turns? 
		- hypothesis: Presenter
	- who talks the most?	
		- hypothesis: Presenter
	- who uses the most advanced vocabulary? 
		- hypothesis: Expert
	- Who is the funniest?
		- hypothesis: Presenter
 
### Methods:

	- create 3 pandas data frame
		- one with the texts
		- one with the speaker information
		- one with backchannels
	- reference the speaker information dataframe when analayzing the text by gender or role
	- nltk.word_tokenize and nltk.sent_tokenize
	- regular expressions to extract information from the text, like speaker number and backchannels
	
## Presentation:

	- DataFrames:
		- speaker information, organized by filename-speaker_role+speaker_number
		- texts, organized by speaker and utterance number within each file
		- graphs to display the results of my analysis