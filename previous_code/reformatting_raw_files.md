
# NOTE:
**This file was my first attempt at data processing. I was able to create data frames, but I did not efficiently or effectively extract my data from the raw form. This attempt relied on the assumption that I could create lists of equal lengths and add them to a data frame. However, this resulted in errors such as the wrong speaker being listed for individual lines.**

**In my next file, process-art-corpus.ipynb, I will work with a dictionary from the raw text. This will have the file name attached to it's lines of texts. This method is much more effective and reliable.**

Alicia Sigmon

als333@pitt.edu

10/17/2017

Updated: 11/15/2017

# Discourse Analysis of the Australian Radio Talkback Courpus

#### About the Corpus
- The Australian Radio Talkback corpus contains raw text files of telephone conversations.
- These conversations include the speaker's role (presenter, expert, or caller), name, and gender.
- The conversations include other verbal cues such as laughter <laugh> and where a speaker says something during another speaker's turn <E1 yeah>. It also notes corrections to the transcription in squirrley brackets {}.

#### Discourse Analysis Goals
- commparing speakers by role and gender
- aspects to consider:
    - back channels (yeah, uhhu, that's great!)
    - vocabulary size (avg word length)
    - number of turns, sentences, and words


```python
%pprint
```

    Pretty printing has been turned OFF
    


```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
from nltk.corpus import PlaintextCorpusReader
import pandas as pd
import nltk
```


```python
# Getting the fileids for ART
# Using PlaintextCorpusReader
ART_corpus_root = r'C:\Users\sigmo\Documents\Data_Science\Project-Alicia\data_files\AustralianRadioTalkback\files\Raw'
ART_corpus = PlaintextCorpusReader(ART_corpus_root, '.*')

ART_fids=[x for x in ART_corpus.fileids()]
```

Each filename contains 3-4 letters followed by a number. They all end in -raw.txt.


```python
len(ART_fids)
ART_fids[:5]
ART_fids[-5:]
```




    26






    ['ABCE1-raw.txt', 'ABCE2-raw.txt', 'ABCE3-raw.txt', 'ABCE4-raw.txt', 'ABCNE1-raw.txt']






    ['NAT3-raw.txt', 'NAT4-raw.txt', 'NAT6-raw.txt', 'NAT7-raw.txt', 'NAT8-raw.txt']



## Mini Test


```python
ART_corpus.raw()[:1000]==ART_corpus.raw('ABCE1-raw.txt')[:1000]
ART_corpus.raw()[:1000]
# Each new line begins with the speaker in [] and ends with \n\n
```




    True






    "[Presenter 1: Simon Marnie, M] Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.\n\n[Expert 1: Angus Stewart, M] I guess yeah yeah <laughs>.\n\n[P1] He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twen"



**Original Speaker Data Format:**

All speaker information is contained within [].

Each first instance of a speaker is in the following order:
    - Speaker Type
        - Presenter, Caller, or Expert
    - Speaker Number
        - the first presenter in a file is Presenter 1, the second presenter is Presenter 2, etc..
    - The Speaker's Name
        - ex: Simon Marnie
    - The Speaker's gender:
        - M / F
    
For every other instance of a speaker's line, the speaker is indicated by P, C, or E followed by their number.
    - Ex: [Presenter 1: Simon Marnie, M] == [P1]


```python
dir(ART_corpus.raw()[:1000])

mini=ART_corpus.raw()[:1000]
# list split by speakers' lines
mini_art=mini.split('\n\n')
mini_art

# 1st attempt at word tokenizing
mini_words=nltk.word_tokenize(mini)
mini_words
    # this does not keep the information of the speaker within brackets as one token
    # how can I separate this information?
```




    ['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']






    ["[Presenter 1: Simon Marnie, M] Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.", '[Expert 1: Angus Stewart, M] I guess yeah yeah <laughs>.', "[P1] He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twen"]






    ['[', 'Presenter', '1', ':', 'Simon', 'Marnie', ',', 'M', ']', 'Thanks', 'for', 'that', 'John', 'Hall', 'now', 'John', 'Hall', 'will', 'be', 'listening', 'for', 'the', 'next', 'hour', "'cos", 'Angus', 'Stewart', 'is', 'here', 'to', 'take', 'your', 'calls', 'eight-triple-three-one-thousand', 'one-eight-hundred-eight-hundred-seven-oh-two', 'something', 'in', 'the', 'garden', 'that', "'s", 'causing', 'you', 'problems', 'give', 'us', 'a', 'call', 'right', 'now', 'and', 'Angus', 'can', 'I', 'mean', "y'know", 'he', 'is', 'known', 'in', 'the', 'trade', 'as', 'Mr', 'popergation', '{', 'propagation', '}', 'Mr', 'propagation', '.', 'He', "'s", 'also', 'known', 'for', 'his', 'passion', 'for', 'natives', 'and', 'his', 'love', 'of', 'o', 'orchids', 'am', 'I', 'right', 'so', 'far', '.', '[', 'Expert', '1', ':', 'Angus', 'Stewart', ',', 'M', ']', 'I', 'guess', 'yeah', 'yeah', '<', 'laughs', '>', '.', '[', 'P1', ']', 'He', "'s", 'also', 'known', '<', 'E1', 'sounds', 'reasonable', '>', 'for', 'his', 'ability', 'to', 'open', 'cosposting', '{', 'composting', '}', 'toilets', 'so', 'he', 'can', 'tell', 'you', 'anything', 'worm', 'farm', 'problems', 'certainly', 'helped', 'us', 'and', 'although', 'I', "'m", 'still', 'confused', 'about', 'dry', 'ingredients', 'we', 'might', 'talk', 'about', 'that', 'as', 'well', 'but', 'eight-triple-three-one-thousand', 'one-eight-hundred-eight-hundred-seven-oh-two', 'fine', 'sunny', 'day', 'today', 'top', 'temperatures', 'on', 'the', 'coast', 'of', 'twenty-seven', 'inland', 'thirty', 'degrees', 'Bowral', 'enjoying', 'twen']




```python
mini_art[0]
endbrack = mini_art[0].index(']')
print(mini_art[0][1:endbrack])
print(mini_art[0][endbrack+2:])
```




    "[Presenter 1: Simon Marnie, M] Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far."



    Presenter 1: Simon Marnie, M
    Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.
    

## Creating lists for data


```python
# splitting all lines
ART_lines=ART_corpus.raw().split("\n\n")
ART_lines[:6]
```




    ["[Presenter 1: Simon Marnie, M] Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.", '[Expert 1: Angus Stewart, M] I guess yeah yeah <laughs>.', "[P1] He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twenty-seven and Katoomba twenty-five degrees currently around town on the coast it's seventeen that's four below <,> r Richmond and Bankstown are fifteen degrees Penrith sixteen Katoomba thirteen and Gosford twelve. One of the jewels in the open garden scheme crown is opening today and this is just a garden to envy how would you like <,> to have <,> a beautiful sandstone cottage nestled underneath a waterfall with a little pond and then a creek that runs through with thousands of water dragons so tame they come up and just <,> kiss you. Would you like to live there.", '[E1] Okay.', "[P1] Jeanne Villani does and we'll find out the secret of her open garden and give you the address so that you can go along today and tomorrow to see Waterfall Cottage which is a part of the open garden scheme all this and more because it is Saturday.\r\n\r\n{program advert}", "[P1] Eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two Suzanne's on the line in McMahon's Point and."]




```python
for y in ART_fids[:2]:
    print(y)   
```

    ABCE1-raw.txt
    ABCE2-raw.txt
    


```python
# Taking the speaker information, text, and file name for each line
# and storing them in individual lists

# also counting the number of utterances per file to use as an index in art_df

speaker=[]
text=[]
line_fid=[]
utterance_num=[]

newname=""

for y in ART_fids:
    count=0
    
    for x in ART_corpus.raw(y).split("\n\n"):
        count+=1
        
        # For NAT4:
        if y == "NAT4-raw.txt":
            if x.startswith("[Presenter 1: John Cleary, M]"):
                newname="NAT5-raw.txt"
                
            if newname=="NAT5-raw.txt":
                if x.startswith("["):
                    endbrack = x.index(']')
                    line_fid.append(newname)
                    speaker.append(x[1:endbrack])
                    text.append(x[endbrack+2:])
                    utterance_num.append(count)
            else:
                if x.startswith("["):
                    endbrack = x.index(']')
                    line_fid.append(y)
                    speaker.append(x[1:endbrack])
                    text.append(x[endbrack+2:])
                    utterance_num.append(count)
    
    # For all files that are not NAT4:
        else:
            if x.startswith("["):
                endbrack = x.index(']')
                line_fid.append(y)
                speaker.append(x[1:endbrack])
                text.append(x[endbrack+2:])
                utterance_num.append(count)

# text[3093]   # this line is actually 2 lines!! E1 and C4!
# line_fid[3093] # COME3



# This was attempted inside the 2nd for loop above to fix the line with the index 3093
# in order to fix the line shown above because [C4]'s line is contianed within [E1]'s line
    # there will be a better way to do this

# if count == 3093:
#     sent = "[E1] That sounds exactly <C4 inaudible> what it is just because you've had a hernia operation uh any sort of operation gall bladder operation hernia operation <,> doesn't mean that you can't get other things wrong with you and you still do you still get tonsillitis you still <C4 yeah> get appendicitis and you can still get gastroenteritis which sounds like what you've got.\r\n\r\n[C4] Nah <E1 it ih thi> and because of the operation that's stirring the my tummy up."
#     sent.split("\r\n\r\n")
#     for item in new_split:
#         endbrack = x.index(']')
#         line_fid.append(y)
#         speaker.append(x[1:endbrack])
#         text.append(x[endbrack+2:])
#         utterance_num.append(count)
```


```python
# checking the lists: len = 9026

len(line_fid)
line_fid[:10]
line_fid[-10:]

len(speaker)
speaker[:10]

len(text)
text[:10]

len(utterance_num)
utterance_num[:1500]
```




    9026






    ['ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt']






    ['NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt']






    9026






    ['Presenter 1: Simon Marnie, M', 'Expert 1: Angus Stewart, M', 'P1', 'E1', 'P1', 'P1', 'Caller 1: Suzanne, F', 'P1', 'C1', 'P1']






    9026






    ["Thanks for that John Hall now John Hall will be listening for the next hour 'cos Angus Stewart is here to take your calls eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two something in the garden that's causing you problems give us a call right now and Angus can I mean y'know he is known in the trade as Mr popergation {propagation} Mr propagation. He's also known for his passion for natives and his love of o orchids am I right so far.", 'I guess yeah yeah <laughs>.', "He's also known <E1 sounds reasonable> for his ability to open cosposting {composting} toilets so he can tell you anything worm farm problems certainly helped us and although I'm still confused about dry ingredients we might talk about that as well but eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two fine sunny day today top temperatures on the coast of twenty-seven inland thirty degrees Bowral enjoying twenty-seven and Katoomba twenty-five degrees currently around town on the coast it's seventeen that's four below <,> r Richmond and Bankstown are fifteen degrees Penrith sixteen Katoomba thirteen and Gosford twelve. One of the jewels in the open garden scheme crown is opening today and this is just a garden to envy how would you like <,> to have <,> a beautiful sandstone cottage nestled underneath a waterfall with a little pond and then a creek that runs through with thousands of water dragons so tame they come up and just <,> kiss you. Would you like to live there.", 'Okay.', "Jeanne Villani does and we'll find out the secret of her open garden and give you the address so that you can go along today and tomorrow to see Waterfall Cottage which is a part of the open garden scheme all this and more because it is Saturday.\r\n\r\n{program advert}", "Eight-triple-three-one-thousand one-eight-hundred-eight-hundred-seven-oh-two Suzanne's on the line in McMahon's Point and.", 'Hello.', 'How are you.', "I'm good thank you.", "You've got a big fat <C1 laughs> Morton Bay fig."]






    9026






    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 123, 124, 125, 126, 127, 128, 129, 130, 131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143, 144, 145, 146, 147, 148, 149, 150, 151, 152, 153, 154, 155, 156, 157, 158, 159, 160, 161, 162, 163, 164, 165, 166, 167, 168, 169, 170, 171, 172, 173, 174, 175, 176, 177, 178, 179, 180, 181, 182, 183, 184, 185, 186, 187, 188, 189, 190, 191, 192, 193, 194, 195, 196, 197, 198, 199, 200, 201, 202, 203, 204, 205, 206, 207, 208, 209, 210, 211, 212, 213, 214, 215, 216, 217, 218, 219, 220, 221, 222, 223, 224, 225, 226, 227, 228, 229, 230, 231, 232, 233, 234, 235, 236, 237, 238, 239, 240, 241, 242, 243, 244, 245, 246, 247, 248, 249, 250, 251, 252, 253, 254, 255, 256, 257, 258, 259, 260, 261, 262, 263, 264, 265, 266, 267, 268, 269, 270, 271, 272, 273, 274, 275, 276, 277, 278, 279, 280, 281, 282, 283, 284, 285, 286, 287, 288, 289, 290, 291, 292, 293, 294, 295, 296, 297, 298, 299, 300, 301, 302, 303, 304, 305, 306, 307, 308, 309, 310, 311, 312, 313, 314, 315, 316, 317, 318, 319, 320, 321, 322, 323, 324, 325, 326, 327, 328, 329, 330, 331, 332, 333, 334, 335, 336, 337, 338, 339, 340, 341, 342, 343, 344, 345, 346, 347, 348, 349, 350, 351, 352, 353, 354, 355, 356, 357, 358, 359, 360, 361, 362, 363, 364, 365, 366, 367, 368, 369, 370, 371, 372, 373, 374, 375, 376, 377, 378, 379, 380, 381, 382, 383, 384, 385, 386, 387, 388, 389, 390, 391, 392, 393, 394, 395, 396, 397, 398, 399, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 418, 419, 420, 421, 422, 423, 424, 425, 426, 427, 428, 429, 430, 431, 432, 433, 434, 435, 436, 437, 438, 439, 440, 441, 442, 443, 444, 445, 446, 447, 448, 449, 450, 451, 452, 453, 454, 455, 456, 457, 458, 459, 460, 461, 462, 463, 464, 465, 466, 467, 468, 469, 470, 471, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 123, 124, 125, 126, 127, 128, 129, 130, 131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143, 144, 145, 146, 147, 148, 149, 150, 151, 152, 153, 154, 155, 156, 157, 158, 159, 160, 161, 162, 163, 164, 165, 166, 167, 168, 169, 170, 171, 172, 173, 174, 175, 176, 177, 178, 179, 180, 181, 182, 183, 184, 185, 186, 187, 188, 189, 190, 191, 192, 193, 194, 195, 196, 197, 198, 199, 200, 201, 202, 203, 204, 205, 206, 207, 208, 209, 210, 211, 212, 213, 214, 215, 216, 217, 218, 219, 220, 221, 222, 223, 224, 225, 226, 227, 228, 229, 230, 231, 232, 233, 234, 235, 236, 237, 238, 239, 240, 241, 242, 243, 244, 245, 246, 247, 248, 249, 250, 251, 252, 253, 254, 255, 256, 257, 258, 259, 260, 261, 262, 263, 264, 265, 266, 267, 268, 269, 270, 271, 272, 273, 274, 275, 276, 277, 278, 279, 280, 281, 282, 283, 284, 285, 286, 287, 288, 289, 290, 291, 292, 293, 294, 295, 296, 297, 298, 299, 300, 301, 302, 303, 304, 305, 306, 307, 308, 309, 310, 311, 312, 313, 314, 315, 316, 317, 318, 319, 320, 321, 322, 323, 324, 325, 326, 327, 328, 329, 330, 331, 332, 333, 334, 335, 336, 337, 338, 339, 340, 341, 342, 343, 344, 345, 346, 347, 348, 349, 350, 351, 352, 353, 354, 355, 356, 357, 358, 359, 360, 361, 362, 363, 364, 365, 366, 367, 368, 369, 370, 371, 372, 373, 374, 375, 376, 377, 378, 379, 380, 381, 382, 383, 384, 385, 386, 387, 388, 389, 390, 391, 392, 393, 394, 395, 396, 397, 398, 399, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 418, 419, 420, 421, 422, 423, 424, 425, 426, 427, 428, 429, 430, 431, 432, 433, 434, 435, 436, 437, 438, 439, 440, 441, 442, 443, 444, 445, 446, 447, 448, 449, 450, 451, 452, 453, 454, 455, 456, 457, 458, 459, 460, 461, 462, 463, 464, 465, 466, 467, 468, 469, 470, 471, 472, 473, 474, 475, 476, 477, 478, 479, 480, 481, 482, 483, 484, 485, 486, 487, 488, 489, 490, 491, 492, 493, 494, 495, 496, 497, 498, 499, 500, 501, 502, 503, 504, 505, 506, 507, 508, 509, 510, 511, 512, 513, 514, 515, 516, 517, 518, 519, 520, 521, 522, 523, 524, 525, 526, 527, 528, 529, 530, 531, 532, 533, 534, 535, 536, 537, 538, 539, 540, 541, 542, 543, 544, 545, 546, 547, 548, 549, 550, 551, 552, 553, 554, 555, 556, 557, 558, 559, 560, 561, 562, 563, 564, 565, 566, 567, 568, 569, 570, 571, 572, 573, 574, 575, 576, 577, 578, 579, 580, 581, 582, 583, 584, 585, 586, 587, 588, 589, 590, 591, 592, 593, 594, 595, 596, 597, 598, 599, 600, 601, 602, 603, 604, 605, 606, 607, 608, 609, 610, 611, 612, 613, 614, 615, 616, 617, 618, 619, 620, 621, 622, 623, 624, 625, 626, 627, 628, 629, 630, 631, 632, 633, 634, 635, 636, 637, 638, 639, 640, 641, 642, 643, 644, 645, 646, 647, 648, 649, 650, 651, 652, 653, 654, 655, 656, 657, 658, 659, 660, 661, 662, 663, 664, 665, 666, 667, 668, 669, 670, 671, 672, 673, 674, 675, 676, 677, 678, 679, 680, 681, 682, 683, 684, 685, 686, 687, 688, 689, 690, 691, 692, 693, 694, 695, 696, 697, 698, 699, 700, 701, 702, 703, 704, 705, 706, 707, 708, 709, 710, 711, 712, 713, 714, 715, 716, 717, 718, 719, 720, 721, 722, 723, 724, 725, 726, 727, 728, 729, 730, 731, 732, 733, 734, 735, 736, 737, 738, 739, 740, 741, 742, 743, 744, 745, 746, 747, 748, 749, 750, 751, 752, 753, 754, 755, 756, 757, 758, 759, 760, 761, 762, 763, 764, 765, 766, 767, 768, 769, 770, 771, 772, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 123, 124, 125, 126, 127, 128, 129, 130, 131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143, 144, 145, 146, 147, 148, 149, 150, 151, 152, 153, 154, 155, 156, 157, 158, 159, 160, 161, 162, 163, 164, 165, 166, 167, 168, 169, 170, 171, 172, 173, 174, 175, 176, 177, 178, 179, 180, 181, 182, 183, 184, 185, 186, 187, 188, 189, 190, 191, 192, 193, 194, 195, 196, 197, 198, 199, 200, 201, 202, 203, 204, 205, 206, 207, 208, 209, 210, 211, 212, 213, 214, 215, 216, 217, 218, 219, 220, 221, 222, 223, 224, 225, 226, 227, 228, 229, 230, 231, 232, 233, 234, 235, 236, 237, 238, 239, 240, 241, 242, 243, 244, 245, 246, 247, 248, 249, 250, 251, 252, 253, 254, 255, 256, 257]




```python
# successfully changed the list of each line's file designation to contain NAT5-raw.txt
count=0
for x in line_fid:
    if x.startswith("NAT5"):
        count+=1
        y=x
count # 150 lines in the new file, NAT5-raw.txt
print("New file name:",y)
```




    150



    New file name: NAT5-raw.txt
    


```python
# speaker information compiled
speaker_infos=[]
speaker_infos_fid=[]
count=0
for x in speaker:
    y=line_fid[count] # trying to fix duplicates
    count+=1
    if len(x)>5:
        speaker_infos.append(x)
        speaker_infos_fid.append(y)
```


```python
len(speaker_infos)
speaker_infos[:20]
speaker_infos[-20:]

len(speaker_infos_fid)
speaker_infos_fid[:20]
speaker_infos_fid[-20:]
```




    428






    ['Presenter 1: Simon Marnie, M', 'Expert 1: Angus Stewart, M', 'Caller 1: Suzanne, F', 'Caller 2: Lisa, F', 'Caller 3: Sally, F', 'Caller 4: Danny, M', 'Caller 5: Trevor, M', 'Caller 6: Gillian, F', 'Caller 7: Colleen, F', 'Caller 8: Bernie, M', 'Caller 9: William, M', 'Expert 2: Jeanne Villani, F', 'Caller 10: Beth, F', 'Caller 11: Lynne, F', 'Caller 12: Jack, M', 'Presenter 1: Simon Marnie, M', 'Expert 1: Les, M', 'Expert 2: Pete, M', 'Caller 1: Julie, F', 'Caller 2: Janelle, F']






    ['Caller 12, Brian, M', 'Caller 13: Louis, M', 'Caller 14: Sam, M', 'Presenter 1: Gaby Brown, F', 'Caller 1: Ben, M', 'Caller 2: Tony, M', 'Caller 3: Tim, M', 'Caller 4: Steven, M', 'Caller 5: Theo, M', 'Caller 6: Britney, F', 'Caller 8: Peter, M', 'Caller 9: Michael, M', 'Caller 10, Brett, M', 'Caller 11: Leah, F', 'Caller 12: Grant, M', 'Caller 13: Laurence, M', 'Caller 14: Ted, M', 'Caller 15: Britney, F', 'Caller 16: Jesse, M', 'Caller 17: Kieran, M']






    428






    ['ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE2-raw.txt', 'ABCE2-raw.txt', 'ABCE2-raw.txt', 'ABCE2-raw.txt', 'ABCE2-raw.txt']






    ['NAT7-raw.txt', 'NAT7-raw.txt', 'NAT7-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt']




```python
# simon marnie is presenter 1 for both files ABCE1 and ABCE2
count=0
for x in speaker_infos:
    if "Simon Marnie" in x:
        print(x) # he's only in those 2 files! 
        print(count)
    count+=1

speaker_infos_fid[0]
speaker_infos_fid[15] # shows he's in dif files <-- will work on fixing once all speaker info is in the same format!!
```

    Presenter 1: Simon Marnie, M
    0
    Presenter 1: Simon Marnie, M
    15
    




    'ABCE1-raw.txt'






    'ABCE2-raw.txt'




```python
# finding formats missing the :
for x in speaker_infos:
    if ":" not in x:
        x
        speaker_infos.index(x)
        speaker.index(x)

# what's happening with Paul?
```




    'Caller 11, Robyn, F'






    40






    1478






    'Caller 23, Maureen, F'






    98






    2699






    'Caller 9 Maureen, F'






    121






    3172






    'P1b Paul Murray, M'






    168






    4483






    'Caller 12, Brian, M'






    408






    8600






    'Caller 10, Brett, M'






    420






    8858




```python
# Examining file COME6-raw.txt
speaker.index('P1b Paul Murray, M') # 4483
speaker[4400:4500]

speaker.index('Presenter 1: Paul Murray, M') # 4436
line_fid[4436] #COME6-raw.txt

# after looking at this file, I think it needs to be removed!!
    # The document switches back and forth between P1a and P1b, and once P1a had an interruption in P1b
```




    4483






    ['C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P2', 'C24', 'P1', 'P2', 'C24', 'P1', 'C24', 'P2', 'C24', 'P2', 'P1', 'P2', 'P1', 'P2', 'P1', 'Presenter 1: Paul Murray, M', 'Caller 1: Ella, F', 'P1a', 'C1', 'P1a', 'C1', 'P1a', 'C1', 'P1a', 'Caller 2: TJ, M', 'P1a', 'C2', 'P1a', 'C2', 'P1a', 'Caller 3: Jo, F', 'P1a', 'C3', 'P1a', 'C3', 'P1a', 'C3', 'P1a', 'C3', 'P1a', 'Caller 4: Ruben, M', 'P1a', 'C4', 'P1a', 'C4', 'P1a', 'Caller 5: Johnny, M', 'P1a', 'C5', 'P1a', 'Caller 6: LJ, M', 'P1a', 'C6', 'P1a', 'C6', 'P1a', 'C6', 'P1a', 'C6', 'P1a', 'C6', 'P1a', 'P1b Paul Murray, M', 'Caller 7: Megan, F', 'P1b', 'C7', 'P1b', 'C7', 'P1b', 'C7', 'P1b', 'C7', 'P1b', 'C7', 'P1b', 'C7', 'P1b', 'C7', 'P1b']






    4436






    'COME6-raw.txt'




```python
# manually adding the colon for first time info 
speaker_infos[40]='Caller 11: Robyn, F'
speaker_infos[98]='Caller 23: Maureen, F'
speaker_infos[121]='Caller 9: Maureen, F'
speaker_infos[168]='Presenter 1b: Paul Murray, M' # probably deleting file
speaker_infos[408]='Caller 12: Brian, M'
speaker_infos[420]='Caller 10: Brett, M'

speaker[1478]='Caller 11: Robyn, F'
speaker[2699]='Caller 23: Maureen, F'
speaker[3172]='Caller 9: Maureen, F'
speaker[4483]='Presenter 1b: Paul Murray, M' # maybe delete this file
speaker[8600]='Caller 12: Brian, M'
speaker[8858]='Caller 10: Brett, M'
```


```python
for x in speaker_infos:
    if x[-1:] != "F" and x[-1:] != "M":
        print(x)
        print(speaker_infos.index(x))
        
# Graham's gender: "" -> "NaN"
# Chris's gender: "male" -> "M"
```

    Expert 1: Doctor Graham
    111
    Caller 33b: Chris, male
    359
    


```python
speaker.index("Expert 1: Doctor Graham")
speaker.index("Caller 33b: Chris, male")

speaker[2967]
speaker[7659]
```




    2967






    7659






    'Expert 1: Doctor Graham'






    'Caller 33b: Chris, male'




```python
speaker_infos[111] = "Expert 1: Doctor Graham, NAN"
speaker_infos[359] = "Caller 33b: Chris, M"

speaker[2967] = "Expert 1: Doctor Graham, NAN"
speaker[7659] = "Caller 33b: Chris, M"
```


```python
# necessary for gen: can get speaker_type from speaker_infos!!

# USE REGEX LATER TO MAKE THIS MORE EFFICIENT

# # using word_tokenize to separate out speaker info
speaker_toks=[]
for x in speaker:
    if len(x) > 5:
        speaker_toks.append(nltk.word_tokenize(x))
```


```python
# Works for speaker_type, but can probably use a better method:

# getting gender
len(speaker_toks)
speaker_toks[:5]
gen=[x[-1] for x in speaker_toks]
len(gen)

# getting type
speaker_type=[x[0] for x in speaker_infos]
len(speaker_type)
speaker_type[:20]
```




    428






    [['Presenter', '1', ':', 'Simon', 'Marnie', ',', 'M'], ['Expert', '1', ':', 'Angus', 'Stewart', ',', 'M'], ['Caller', '1', ':', 'Suzanne', ',', 'F'], ['Caller', '2', ':', 'Lisa', ',', 'F'], ['Caller', '3', ':', 'Sally', ',', 'F']]






    428






    428






    ['P', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'E', 'C', 'C', 'C', 'P', 'E', 'E', 'C', 'C']




```python
# Correctly adjusted the incorrect gender formats for Graham and Chris!!

speaker_infos[111]
speaker_infos[359]

speaker[2967]
speaker[7659]
```




    'Expert 1: Doctor Graham, NAN'






    'Caller 33b: Chris, M'






    'Expert 1: Doctor Graham, NAN'






    'Caller 33b: Chris, M'




```python
gen

# # fixing Graham
# speaker_infos[gen.index("Graham")] # does not list a gender
# gen[gen.index("Graham")]="NAN"

# # fixing "male" for gender IN speaker_infos AND speaker
# speaker_infos[gen.index("male")]
# speaker_infos[gen.index("male")]='Caller 33b: Chris, M'
# print("index of 'male':",str(gen.index("male")))

# # this claims chris is an Expert - WRONG 
# speaker[gen.index("male")]

# len(gen)
# len(speaker)
# len(speaker_infos)

# # CANNOT DO THIS BECAUSE SPEAKER'S INDEX IS NOT THE SAME AS GEN'S INDEX
# # speaker[gen.index("male")]='Caller 33b: Chris, M'       
#     # THIS IS WHY 33B WAS IN ABCE1!!!! 

# speaker[speaker.index('Caller 33b: Chris, male')]='Caller 33b: Chris, M'
# speaker_infos[gen.index("male")]

# gen[gen.index("male")]='M'
# gen
```




    ['M', 'M', 'F', 'F', 'F', 'M', 'M', 'F', 'F', 'M', 'M', 'F', 'F', 'F', 'M', 'M', 'M', 'M', 'F', 'F', 'M', 'M', 'M', 'F', 'F', 'M', 'F', 'M', 'F', 'F', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'M', 'F', 'M', 'M', 'F', 'F', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'F', 'M', 'F', 'M', 'M', 'F', 'M', 'F', 'F', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'F', 'F', 'M', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'NAN', 'F', 'F', 'F', 'F', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'F', 'F', 'M', 'F', 'M', 'F', 'M', 'M', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'F', 'M', 'F', 'F', 'M', 'F', 'F', 'F', 'M', 'F', 'F', 'F', 'F', 'M', 'F', 'F', 'M', 'F', 'F', 'F', 'F', 'M', 'F', 'M', 'F', 'M', 'M', 'M', 'M', 'F', 'M', 'F', 'F', 'M', 'F', 'M', 'M', 'F', 'M', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'F', 'M', 'M', 'M', 'M', 'F', 'F', 'M', 'M', 'F', 'M', 'F', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'F', 'M', 'F', 'M', 'M', 'M', 'F', 'F', 'M', 'M', 'F', 'M', 'M', 'F', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'F', 'F', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'M', 'F', 'F', 'M', 'F', 'M', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'F', 'F', 'F', 'M', 'M', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'F', 'M', 'M', 'F', 'M', 'F', 'F', 'M', 'M', 'F', 'F', 'F', 'M', 'M', 'M', 'M', 'F', 'M', 'F', 'M', 'F', 'F', 'M', 'F', 'F', 'M', 'M', 'F', 'M', 'M', 'F', 'F', 'M', 'M', 'M', 'F', 'M', 'M', 'F', 'F', 'M', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'F', 'F', 'M', 'M', 'M', 'F', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'M', 'M', 'F', 'M', 'M']




```python
# speaker_infos.index('Caller 33b: Chris, M') # 359
# speaker.index('Caller 33b: Chris, M') # 7659

# speaker_num

# line_fid[359]
# line_fid[7659]


# speaker_infos[:20]
# speaker_num[:20]

# # used to see a ":" as the number for Jenny, Caller 5
#     # ex: Jenny's first line is called "C5" instead of Caller 5
#     # see below for fixes
```


```python
# # which speaker_num items are wrong?
# count=0
# for x in speaker_num:
#     if x == ":":
#         print(x)
#         speaker_infos[count]
#         print(count)
#     count+=1
    
# # later rebuild speaker_num using regex
# # to find these where the 1st instance uses C,E,or P instead of Caller, Expert etc, can use .startswith
```


```python
# speakers whose type is not written out!

for x in speaker_infos:
    if x[2].isalpha()== False:
        print(x)
        print(speaker_infos.index(x))
```

    C5: Jenny, F
    105
    C14: Noelene, F
    244
    


```python
# fixing the above lines that labeled the number as a colon

# speaker_num[105] = '5'
# speaker_num[244] = '14'

# Fixing Jenny and Noelene!!
speaker_infos[105]='Caller 5: Jenny, F'
speaker_infos[244]='Caller 14: Noelene, F'

speaker.index('C5: Jenny, F') # 2834
speaker.index('C14: Noelene, F') # 6063

speaker[2834] = 'Caller 5: Jenny, F'
speaker[6063] = 'Caller 14: Noelene, F'
```




    2834






    6063




```python
# Jenny and Noelene are fixed!

speaker_infos[105]
speaker_infos[244]

speaker[2834]
speaker[6063]
```




    'Caller 5: Jenny, F'






    'Caller 14: Noelene, F'






    'Caller 5: Jenny, F'






    'Caller 14: Noelene, F'




```python
# # dictionary for gender of the speaker from speaker info
# gen_dict={x:x[-1] for x in speaker_infos}
```


```python
# gen_dict['Presenter 1: Simon Marnie, M']
```


```python
# # dictionary for filename from speaker info
# file_speaker_dict={x:line_fid[speaker.index(x)] for x in speaker_infos}
```


```python
# file_speaker_dict['Presenter 1: Simon Marnie, M']
# file_speaker_dict['Caller 12: Brian, M']
```


```python
# # dictionary for speaker's filename, gender, and shortcut label (ex: P1, C12, etc..)
# gen_file_speaker_dict={x:[line_fid[speaker.index(x)],x[-1],speaker_type[speaker_infos.index(x)]+speaker_num[speaker_infos.index(x)]] for x in speaker_infos}
```


```python
# gen_file_speaker_dict['Presenter 1: Simon Marnie, M']
# gen_file_speaker_dict['Caller 12: Brian, M']
```


```python
# Figuring out how to do the regular expression to find the speaker_number
# USE x IN THE BIG LOOP
import re

s="Presenter 1: Simon Marnie, M"
s="Caller 33b: Chris, M"

re.findall('\d+[a-z]*', s)[0]
```




    '33b'




```python
# using regular expressions to find the speaker num!
for x in speaker_infos:
    speaker_num=[re.findall('\d+[a-z]*', x)[0] for x in speaker_infos]
    
len(speaker_num)
```




    428




```python
# creating a lists for all speakers and unique speakers

new_speaker_list=[]    # a list of each line's speaker with the filename
all_speaker_type=[]    # a list of each line's speaker's P/C/E designation
unique_speaker=[]      # a list of each speaker's unique id (ex: ABCE1-P1)
unique_speaker_type=[] # a list of each unique speaker's type (P/C/E)
unique_speaker_fid=[]  # a list of which file contains each unique speaker

count = 0 
all_count=0

used_speaker=[]

# for x in speaker[:500]:
# for x in speaker[-50:]:
for x in speaker:

    x_loc=speaker.index(x)
#     print(line_fid[x_loc])
#     print(line_fid[x_loc].index("-"))
#     print(line_fid[x_loc][:dash+1])
    dash=line_fid[x_loc].index("-")
    
    
    # adjusts for people like Simon Marnie who show up in multiple files (ABCE1 and ABCE2)
    if x in used_speaker:
#         print(x)
        x_loc=all_count # getting rid of this line messes it up.... something is wrong in here!!
        dash=line_fid[all_count].index("-")
    
    if x in speaker_infos:
        
#         print(speaker_type[speaker_infos.index(x)])
#         print(speaker_num[speaker_infos.index(x)])
#         print(line_fid[x_loc][:dash+1])

        current_speaker=speaker_infos[count] # WRONG!!! 
#         if current_speaker in used_speaker:
#             print(current_speaker)
        new_speaker_list.append(line_fid[x_loc][:dash+1]+speaker_type[speaker_infos.index(x)]+speaker_num[speaker_infos.index(x)])
#         print(current_speaker) ## DOES NOT MATCH BELOW
#         print(line_fid[x_loc][:dash+1]+speaker_type[speaker_infos.index(x)]+speaker_num[speaker_infos.index(x)]) 
        all_speaker_type.append(speaker_type[speaker_infos.index(x)])
        
        # ONLY CHECK THESE IF YOU LIMIT THE RANGE OF speaker!
#         print(line_fid[x_loc][:dash+1]) # CORRECT
#         print(speaker_type[count]) # GIVES WRONG LETTER -- CANNOT USE COUNT FEATURE
#         print(x[0])
#         print(x+"\n") # correctly identifies Marnie's second occurance as being in ABCE2

        NUM=re.findall('\d+[a-z]*', x) # need regex to fix the number - get type from first letter of x instead of using speaker_type list
        
        
        # NAT4 Duplicate Loop:
            # CHECK FOR DUPLICATES: File NAT4 begins with a new Presenter 1, Caller1-6 at the end of the file!!
            # The second half of NAT4 will now be NAT5 because there is no NAT 5 file!
            
        if line_fid[x_loc][:dash+1]+x[0]+NUM[0] in unique_speaker:
            
            print(line_fid[x_loc][:dash+1]+x[0]+NUM[0])
         
            # NO LONGER NECESSARY AFTER FIXING line_fid
#             unique_speaker.append(line_fid[x_loc][:dash-1]+"5"+line_fid[x_loc][dash:dash+1]+x[0]+NUM[0])
#             unique_speaker_type.append(x[0])
#             unique_speaker_fid.append(line_fid[x_loc][:dash-1]+"5"+line_fid[x_loc][dash:dash])
            
#             print(line_fid[x_loc][:dash-1]+"5"+line_fid[x_loc][dash:dash+1]+x[0]+NUM[0])
#             print(x[0])
#             print(line_fid[x_loc][:dash-1]+"5"+line_fid[x_loc][dash:dash])
            
        else:
            unique_speaker.append(line_fid[x_loc][:dash+1]+x[0]+NUM[0])
            unique_speaker_type.append(x[0])
            unique_speaker_fid.append(line_fid[x_loc][:dash+1]) # refers to their first line to find the file id
        
#         unique_speaker.append(line_fid[x_loc][:dash+1]+x[0]+NUM[0])
#         unique_speaker_type.append(x[0])
#         unique_speaker_fid.append(line_fid[x_loc][:dash+1]) # refers to their first line to find the file id
        
        count+=1
        used_speaker.append(x)
    else:
        new_speaker_list.append(line_fid[x_loc][:dash+1]+x)
        all_speaker_type.append(x[0]) # only want the letter
    
    all_count+=1

    
# Same names in multiple files: 
    # Presenter 1: Simon Marnie, M
    # Caller 6: Alan, M
    # Presenter 1: Trevor Jackson, M
    # Caller 1: Graham, M
    # Presenter 1: Luke Bona, M
    # Caller 3: Cathy, F
    # Presenter 1: Luke Bona, M
    # Caller 1: Julie, F
    # Caller 7: Tony, M
    # Presenter 1: Harvey Deegan, M
    # Caller 2: Anne, F
    # Caller 3: John, M
    # Caller 8: Paul, M
    # Presenter 1: Sandy McCutcheon, M
    # Caller 8: Paul, M
    # Caller 11: Shirley, F
    # Caller 5: Judy, F
# why no dah after COMNEC8??
```


```python
# # A SECOND ATTEMPT AT GETTING UNIQUE SPEAKER INFO:
# # Taking the speaker information, text, and file name for each line
# # and storing them in individual lists

# # also counting the number of utterances per file to use as an index in art_df
# NEWALL=[]

# for y in ART_fids:
#     count=0
    
#     for x in ART_corpus.raw(y).split("\n\n"):
#         count+=1
        
#         # For NAT4:
#         if y == "NAT4-raw.txt":
#             if x.startswith("[Presenter 1: John Cleary, M]"):
#                 newname="NAT5-raw.txt"
                
#             if newname=="NAT5-raw.txt":
#                 if x.startswith("["):
#                     endbrack = x.index(']')
#                     dash=newname.index("-")
#                     z=x[1:endbrack] # speaker info?
#                     NUM=re.findall('\d+[a-z]*', z)
#                     NEWALL.append(newname[:dash+1]+x[1:2]+NUM)
#             else:
                
#                 if x.startswith("["):
#                     endbrack = x.index(']')
#                     dash=newname.index("-")
#                     z=x[1:endbrack] # speaker info?
#                     NUM=re.findall('\d+[a-z]*', z)
#                     NEWALL.append(newname[:dash+1]+x[1]+NUM)
    
#     # For all files that are not NAT4:
#         else:
#             if x.startswith("["):
#                 endbrack = x.index(']')
#                 dash=x.index("-")
#                 z=x[1:endbrack] # speaker info?
#                 NUM=re.findall('\d+[a-z]*', z)
#                 NEWALL.append(y[:dash+1]+x[1]+NUM)

```


```python
len(used_speaker)
len(unique_speaker) # 428

# After adding the NAT4 Duplicate Loop, every speaker has a unique ID:
# After fixing line_fid, the NAT4 Duplicate Loop is no longer necessary to give every speaker a unique ID
len(set(unique_speaker)) # 421 -> 428 
all_count
x_loc
```




    428






    428






    428






    9026






    2525




```python
# how many times is Simon Marnie the main presenter? Answer: twice!
count=0
for x in speaker:
    if x == "Presenter 1: Simon Marnie, M":
        count
    count+=1
print("First instance of Simon Marnie:",str(speaker[0]), ",", str(line_fid[0]))
print("Second instance of Simon Marnie:",str(speaker[471]), ",", str(line_fid[471]))

# line_fid WAS correctly built (at least where Simon Marnie is concnered)
    # Simon is in ABCE1 and ABCE2
```




    0






    471



    First instance of Simon Marnie: Presenter 1: Simon Marnie, M , ABCE1-raw.txt
    Second instance of Simon Marnie: Presenter 1: Simon Marnie, M , ABCE2-raw.txt
    


```python
# comparing new_speaker_list, speaker, and all_speaker_type to make sure they are the same

# 9026 lines
len(new_speaker_list)
len(speaker)
len(all_speaker_type)

print("Original list of speakers for each line:")
speaker[:100]
speaker[-100:]

print("New list of speakers for each line:")
new_speaker_list[:100]

# WHY ARE ABCE1-P1 AND OTHER FILENAMES SHOWINIG UP IN THE END? ERROR SOMEWHERE!!!!!
# !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
new_speaker_list[-100:]

print("List of the type of speaker for each line:")
all_speaker_type[:100]
all_speaker_type[-100:]

print("List of fileid for each line:")
line_fid[:100]
line_fid[-100:]
```




    9026






    9026






    9026



    Original list of speakers for each line:
    




    ['Presenter 1: Simon Marnie, M', 'Expert 1: Angus Stewart, M', 'P1', 'E1', 'P1', 'P1', 'Caller 1: Suzanne, F', 'P1', 'C1', 'P1', 'C1', 'P1', 'C1', 'P1', 'C1', 'P1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'E1', 'C1', 'P1', 'C1', 'P1', 'C1', 'P1', 'E1', 'P1', 'E1', 'P1', 'E1', 'P1', 'E1', 'P1', 'E1', 'P1', 'E1', 'P1', 'P1', 'Caller 2: Lisa, F', 'P1', 'C2', 'P1', 'C2', 'E1', 'C2', 'E1', 'P1', 'C2', 'P1', 'C2', 'P1', 'E1', 'C2', 'E1', 'C2', 'E1', 'C2', 'E1', 'P1', 'E1', 'C2', 'P1', 'C2', 'E1', 'P1', 'C2', 'P1', 'C2', 'P1', 'P1', 'Caller 3: Sally, F', 'P1', 'C3', 'P1', 'C3', 'P1', 'C3', 'E1', 'C3', 'P1', 'C3', 'P1', 'E1', 'P1']






    ['P1', 'C13', 'P1', 'C13', 'P1', 'C13', 'P1', 'C13', 'P1', 'C13', 'P1', 'C13', 'P1', 'C13', 'P1', 'C13', 'P1', 'Caller 14: Ted, M', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'C14', 'P1', 'P1', 'P1', 'Caller 15: Britney, F', 'P1', 'C15', 'P1', 'C15', 'P1', 'C15', 'P1', 'C15', 'P1', 'C15', 'P1', 'C15', 'P1', 'C15', 'P1', 'Caller 16: Jesse, M', 'P1', 'C16', 'P1', 'C16', 'P1', 'C16', 'P1', 'C16', 'P1', 'C16', 'P1', 'C16', 'P1', 'Caller 17: Kieran, M', 'P1', 'C17']



    New list of speakers for each line:
    




    ['ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-E1', 'ABCE1-C2', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-C2', 'ABCE1-E1', 'ABCE1-C2', 'ABCE1-E1', 'ABCE1-C2', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-C2', 'ABCE1-P1', 'ABCE1-P1', 'ABCE1-C3', 'ABCE1-P1', 'ABCE1-C3', 'ABCE1-P1', 'ABCE1-C3', 'ABCE1-P1', 'ABCE1-C3', 'ABCE1-E1', 'ABCE1-C3', 'ABCE1-P1', 'ABCE1-C3', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1']






    ['ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'COME1-C13', 'ABCE1-P1', 'NAT8-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'COME1-C14', 'ABCE1-P1', 'ABCE1-P1', 'ABCE1-P1', 'NAT8-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'COME1-C15', 'ABCE1-P1', 'NAT8-C16', 'ABCE1-P1', 'COME1-C16', 'ABCE1-P1', 'COME1-C16', 'ABCE1-P1', 'COME1-C16', 'ABCE1-P1', 'COME1-C16', 'ABCE1-P1', 'COME1-C16', 'ABCE1-P1', 'COME1-C16', 'ABCE1-P1', 'NAT8-C17', 'ABCE1-P1', 'COME1-C17']



    List of the type of speaker for each line:
    




    ['P', 'E', 'P', 'E', 'P', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'C', 'P', 'C', 'P', 'C', 'P', 'E', 'P', 'E', 'P', 'E', 'P', 'E', 'P', 'E', 'P', 'E', 'P', 'P', 'C', 'P', 'C', 'P', 'C', 'E', 'C', 'E', 'P', 'C', 'P', 'C', 'P', 'E', 'C', 'E', 'C', 'E', 'C', 'E', 'P', 'E', 'C', 'P', 'C', 'E', 'P', 'C', 'P', 'C', 'P', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'E', 'C', 'P', 'C', 'P', 'E', 'P']






    ['P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'P', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C', 'P', 'C']



    List of fileid for each line:
    




    ['ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt', 'ABCE1-raw.txt']






    ['NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt', 'NAT8-raw.txt']




```python
# checking unique_speaker, unique_speaker_type, and unique_speaker_fid

# 428 for each
len(speaker_infos)
len(unique_speaker)
len(unique_speaker_type)
len(unique_speaker_fid)

print("Speaker Infos:")
speaker_infos[:100]
speaker_infos[-100:]

print("Unique Speaker ID:")
unique_speaker[:100]
unique_speaker[-100:]

print("Unique Speaker Type:")
unique_speaker_type[:100] # Note: NOT made from speaker_type
unique_speaker_type[-100:]

print("Unique Speaker Fileid:")
unique_speaker_fid[:100]
unique_speaker_fid[-100:]
```




    428






    428






    428






    428



    Speaker Infos:
    




    ['Presenter 1: Simon Marnie, M', 'Expert 1: Angus Stewart, M', 'Caller 1: Suzanne, F', 'Caller 2: Lisa, F', 'Caller 3: Sally, F', 'Caller 4: Danny, M', 'Caller 5: Trevor, M', 'Caller 6: Gillian, F', 'Caller 7: Colleen, F', 'Caller 8: Bernie, M', 'Caller 9: William, M', 'Expert 2: Jeanne Villani, F', 'Caller 10: Beth, F', 'Caller 11: Lynne, F', 'Caller 12: Jack, M', 'Presenter 1: Simon Marnie, M', 'Expert 1: Les, M', 'Expert 2: Pete, M', 'Caller 1: Julie, F', 'Caller 2: Janelle, F', 'Caller 3: Geoff, M', 'Caller 4: Terry, M', 'Expert 3: John Hall, M', 'Caller 5: Judy, F', 'Caller 6: Dawn, F', 'Caller 7: Paul, M', 'Caller 8: Linda, F', 'Caller 9: Croydon, M', 'Caller 10: Joan, F', 'Presenter 1: Lynne Haultain, F', 'Presenter 2: Jurate Sasnaitis, F', 'Caller 1: Rick, M', 'Caller 2: Sarah, F', 'Caller 3: Liz, F', 'Caller 4: Cathy, F', 'Caller 6: Bullia, F', 'Caller 7: Juliet, F', 'Caller 8: Melanie, F', 'Caller 9: Margaret, F', 'Caller 10: Lisa, F', 'Caller 11: Robyn, F', 'Caller 12: Mary, F', 'Expert 1: Ric Nattrass, M', 'Presenter 1: Kelly Higgins-Devine, F', 'Caller 1: Graham, M', 'Caller 2: Len, M', 'Caller 3: Cathy, F', 'Caller 4: Margaret, F', 'Caller 5: Hayden, M', 'Caller 6: Alan, M', 'Caller 7: Sharon, F', 'Presenter 1: Trevor Jackson, M', 'Expert 1: Roly Sussex, M', 'Caller 1: Barry, M', 'Caller 2: Anne, F', 'Caller 3: Lance, M', 'Caller 4: Pauline, F', 'Caller 5: John, M', 'Caller 6: Alan, M', 'Caller 7: Colin, M', 'Caller 8: Roger, M', 'Caller 9: Jim, M', 'Presenter 1: Trevor Jackson, M', 'Expert 1: Greg Kerrin, M', 'Caller 1: Graham, M', 'Caller 2: Patricia, F', 'Caller 3: John, M', 'Caller 4: Iris, F', 'Caller 5: Peter, M', 'Caller 6: Kath, F', 'Caller 7: Leon, M', 'Caller 8: Bill, M', 'Caller 9: Iris, F', 'Presenter 1: Luke Bona, M', 'Expert 1: Linda Ross, F', 'Caller 1: Anne, F', 'Caller 2: Iris, F', 'Caller 3: Greg, M', 'Caller 4: Jenny, F', 'Caller 5: Mila, F', 'Caller 6: Pamela, F', 'Caller 7: Glad, F', 'Caller 8: Sally, F', 'Caller 9: John, M', 'Caller 10: Dorothy, F', 'Caller 11: Nora, F', 'Caller 12: Dorothy, F', 'Caller 13: Laurie, F', 'Caller 14: Nicky, F', 'Caller 15: Maurice, M', 'Caller 16: Robyn, F', 'Caller 17: Winifred, F', 'Expert 2: Rodian Booker, M', 'Caller 18: Noel, M', 'Caller 19: Nicky, F', 'Caller 20: Anita, F', 'Caller 21: Lorraine, F', 'Caller 22: Judy, F', 'Caller 23: Maureen, F', 'Presenter 1: Luke Bona, M']






    ['Caller 4: Joan, F', 'Caller 5: Judy, F', 'Caller 6: Lynne, F', 'Caller 7: Edith, F', 'Caller 8: Karen, F', 'Caller 9: Ruth, F', 'Caller 10: Wayne, M', 'Caller 11: David, M', 'Caller 12: Helen, F', 'Caller 13: Graham, M', 'Caller 14: Sue, F', 'Caller 15: Jennifer, F', 'Caller 16: Greg, M', 'Caller 17: Kevin, M', 'Caller 18: Glenys, F', 'Caller 19: June, F', 'Caller 20: Betty, F', 'Caller 21: Jeremiah, M', 'Caller 22: Michael, M', 'Caller 23: Ken, M', 'Caller 24: Jim, M', 'Caller 25: Debbie, F', 'Caller 26: Frank, M', 'Caller 27: Sonia, F', 'Caller 28: Sean, M', 'Caller 29: Anne, F', 'Caller 30: Lesley, F', 'Caller 31: Ron, M', 'Caller 32a: Sue, F', 'Caller 32b: Mary, F', 'Caller 33a: Gerrard, M', 'Caller 33b: Chris, M', 'Caller 34: Keira, F', 'Caller 35: Robin, M', 'Caller 36: Wayne, M', 'Caller 37: Sue, F', 'Caller 38: Jill, F', 'Caller 39: Peter, M', 'Caller 40: Rick, M', 'Caller 41: Jean Pierre, M', 'Caller 42: Magpie, F', 'Caller 43: Warren, M', 'Caller 44: Colin, M', 'Caller 45: Eve, F', 'Caller 46: Dawn, F', 'Caller 47: James, M', 'Caller 48: Steve, M', 'Caller 49: Greg, M', 'Caller 50: Tom, M', 'Caller 51: Ian, M', 'Presenter 1: John Cleary, M', 'Expert 2: Victoria Kearney, F', 'Expert 3: Paul Newsham, M', 'Caller 1: Damian, M', 'Caller 2: Bernard, M', 'Caller 3: Pam, F', 'Caller 4: Mark, M', 'Caller 5: Michael, M', 'Caller 6: Caleb, M', 'Presenter 1: Mel Bampton, F', 'Expert 1: Karl Kruselnicki, M', 'Caller 1: Naomi, F', 'Caller 2: Fiona, F', 'Caller 3: Scott, M', 'Caller 4: Jason, M', 'Caller 5: Ty, M', 'Caller 6: Priscilla, F', 'Caller 7: Gonk, M', 'Presenter 1: Rosie Beaton, F', 'Caller 1: Dan, M', 'Caller 3: Mark, M', 'Caller 4: Lotus, M', 'Caller 5: Nelson, M', 'Caller 6: Mark, M', 'Caller 7: Lindsay, M', 'Caller 8: Seamus, M', 'Caller 9: Tash, F', 'Expert 1: Robbie Buck, M', 'Caller 10: Clarence, M', 'Caller 11: Sarah, F', 'Caller 12: Brian, M', 'Caller 13: Louis, M', 'Caller 14: Sam, M', 'Presenter 1: Gaby Brown, F', 'Caller 1: Ben, M', 'Caller 2: Tony, M', 'Caller 3: Tim, M', 'Caller 4: Steven, M', 'Caller 5: Theo, M', 'Caller 6: Britney, F', 'Caller 8: Peter, M', 'Caller 9: Michael, M', 'Caller 10: Brett, M', 'Caller 11: Leah, F', 'Caller 12: Grant, M', 'Caller 13: Laurence, M', 'Caller 14: Ted, M', 'Caller 15: Britney, F', 'Caller 16: Jesse, M', 'Caller 17: Kieran, M']



    Unique Speaker ID:
    




    ['ABCE1-P1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-C2', 'ABCE1-C3', 'ABCE1-C4', 'ABCE1-C5', 'ABCE1-C6', 'ABCE1-C7', 'ABCE1-C8', 'ABCE1-C9', 'ABCE1-E2', 'ABCE1-C10', 'ABCE1-C11', 'ABCE1-C12', 'ABCE2-P1', 'ABCE2-E1', 'ABCE2-E2', 'ABCE2-C1', 'ABCE2-C2', 'ABCE2-C3', 'ABCE2-C4', 'ABCE2-E3', 'ABCE2-C5', 'ABCE2-C6', 'ABCE2-C7', 'ABCE2-C8', 'ABCE2-C9', 'ABCE2-C10', 'ABCE3-P1', 'ABCE3-P2', 'ABCE3-C1', 'ABCE3-C2', 'ABCE3-C3', 'ABCE3-C4', 'ABCE3-C6', 'ABCE3-C7', 'ABCE3-C8', 'ABCE3-C9', 'ABCE3-C10', 'ABCE3-C11', 'ABCE3-C12', 'ABCE4-E1', 'ABCE4-P1', 'ABCE4-C1', 'ABCE4-C2', 'ABCE4-C3', 'ABCE4-C4', 'ABCE4-C5', 'ABCE4-C6', 'ABCE4-C7', 'ABCNE1-P1', 'ABCNE1-E1', 'ABCNE1-C1', 'ABCNE1-C2', 'ABCNE1-C3', 'ABCNE1-C4', 'ABCNE1-C5', 'ABCNE1-C6', 'ABCNE1-C7', 'ABCNE1-C8', 'ABCNE1-C9', 'ABCNE2-P1', 'ABCNE2-E1', 'ABCNE2-C1', 'ABCNE2-C2', 'ABCNE2-C3', 'ABCNE2-C4', 'ABCNE2-C5', 'ABCNE2-C6', 'ABCNE2-C7', 'ABCNE2-C8', 'ABCNE2-C9', 'COME1-P1', 'COME1-E1', 'COME1-C1', 'COME1-C2', 'COME1-C3', 'COME1-C4', 'COME1-C5', 'COME1-C6', 'COME1-C7', 'COME1-C8', 'COME1-C9', 'COME1-C10', 'COME1-C11', 'COME1-C12', 'COME1-C13', 'COME1-C14', 'COME1-C15', 'COME1-C16', 'COME1-C17', 'COME1-E2', 'COME1-C18', 'COME1-C19', 'COME1-C20', 'COME1-C21', 'COME1-C22', 'COME1-C23', 'COME2-P1']






    ['NAT4-C4', 'NAT4-C5', 'NAT4-C6', 'NAT4-C7', 'NAT4-C8', 'NAT4-C9', 'NAT4-C10', 'NAT4-C11', 'NAT4-C12', 'NAT4-C13', 'NAT4-C14', 'NAT4-C15', 'NAT4-C16', 'NAT4-C17', 'NAT4-C18', 'NAT4-C19', 'NAT4-C20', 'NAT4-C21', 'NAT4-C22', 'NAT4-C23', 'NAT4-C24', 'NAT4-C25', 'NAT4-C26', 'NAT4-C27', 'NAT4-C28', 'NAT4-C29', 'NAT4-C30', 'NAT4-C31', 'NAT4-C32a', 'NAT4-C32b', 'NAT4-C33a', 'NAT4-C33b', 'NAT4-C34', 'NAT4-C35', 'NAT4-C36', 'NAT4-C37', 'NAT4-C38', 'NAT4-C39', 'NAT4-C40', 'NAT4-C41', 'NAT4-C42', 'NAT4-C43', 'NAT4-C44', 'NAT4-C45', 'NAT4-C46', 'NAT4-C47', 'NAT4-C48', 'NAT4-C49', 'NAT4-C50', 'NAT4-C51', 'NAT5-P1', 'NAT5-E2', 'NAT5-E3', 'NAT5-C1', 'NAT5-C2', 'NAT5-C3', 'NAT5-C4', 'NAT5-C5', 'NAT5-C6', 'NAT6-P1', 'NAT6-E1', 'NAT6-C1', 'NAT6-C2', 'NAT6-C3', 'NAT6-C4', 'NAT6-C5', 'NAT6-C6', 'NAT6-C7', 'NAT7-P1', 'NAT7-C1', 'NAT7-C3', 'NAT7-C4', 'NAT7-C5', 'NAT7-C6', 'NAT7-C7', 'NAT7-C8', 'NAT7-C9', 'NAT7-E1', 'NAT7-C10', 'NAT7-C11', 'NAT7-C12', 'NAT7-C13', 'NAT7-C14', 'NAT8-P1', 'NAT8-C1', 'NAT8-C2', 'NAT8-C3', 'NAT8-C4', 'NAT8-C5', 'NAT8-C6', 'NAT8-C8', 'NAT8-C9', 'NAT8-C10', 'NAT8-C11', 'NAT8-C12', 'NAT8-C13', 'NAT8-C14', 'NAT8-C15', 'NAT8-C16', 'NAT8-C17']



    Unique Speaker Type:
    




    ['P', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'E', 'C', 'C', 'C', 'P', 'E', 'E', 'C', 'C', 'C', 'C', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'P', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'E', 'P', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'P']






    ['C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'E', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'E', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'P', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'E', 'C', 'C', 'C', 'C', 'C', 'P', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C', 'C']



    Unique Speaker Fileid:
    




    ['ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE1-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE2-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE3-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCE4-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE1-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'ABCNE2-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME1-', 'COME2-']






    ['NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT4-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT5-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT6-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT7-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-', 'NAT8-']




```python
# Check Marnie in the new lists:

# marnie should be ABCE2
speaker_infos[15]
print("Marnie's 2ND file Unique ID:", str(unique_speaker[15]))
print("Marnie's speaker type:",str(unique_speaker_type[15]))
print("Marnie's fileid:",str(unique_speaker_fid[15]))
```




    'Presenter 1: Simon Marnie, M'



    Marnie's 2ND file Unique ID: ABCE2-P1
    Marnie's speaker type: P
    Marnie's fileid: ABCE2-
    


```python
# finding extra items in the text like laughter and interruptions

# THIS IS A WORK IN PROGRESS
# I will change my methods to use regular expressions in order to find backchannels instead of using all of these loops

# extras=[]
# all_sq_braqs=[]
# all_carrots=[]

# for line in text:
    
#     line_extras=[]
#     sq_bra_each_line=[]
#     car_each_line=[]
    
#     # skipping lines that are not speech 
#     if line.startswith("\r\n{")==False:
        
#         if "<" in line: # others' speech, laughter, "inaudible"
#             CARROTS_INDEX=[]
#             END_CARROTS_INDEX=[]
#             for y in line:
#                 if y == "<":
#                     CARROTS_INDEX.append(line.index(y))
#                 elif y == ">":
#                     END_CARROTS_INDEX.append(line.index(y))
#             for z in CARROTS_INDEX:
#                 car=line[z+1:END_CARROTS_INDEX[CARROTS_INDEX.index(z)]]
#                 car_each_line.append(car)

#         else:
#             car_each_line.append("Nan")
            
#         all_carrots.append(car_each_line)        
     
#         if "{" in line: # spelling corrections, interruptions to the program (I tried to remove previously)
#             BRAQ_INDEX=[]
#             END_SQ_BRAQ_INDEX=[]
#             for y in line:
#                 if y == "{":
#                     BRAQ_INDEX.append(line.index(y))
#                 elif y == "}":
#                     END_SQ_BRAQ_INDEX.append(line.index(y))
#             for z in BRAQ_INDEX:
#                 sq_bra=line[z+1:END_SQ_BRAQ_INDEX[BRAQ_INDEX.index(z)]]
#                 sq_bra_each_line.append(sq_bra)
                
#         else: 
#             sq_bra_each_line.append("Nan")
            
# #         print(sq_bra_each_line)
#         all_sq_braqs.append(sq_bra_each_line)
# #         print(all_sq_braqs)
        
# #         if "[" in line:
# #             bracket=line.index("[")
# #             if "]" not in line:         
# #                 print(line)
# #                 print(text.index(line))    # 3093
# #             end_bracket=line.index("]")
# #             bra=line[bracket:end_bracket]
# #             line_extras.append(bra)

# #         if "[" not in line and "{" not in line and "<" not in line:

```


```python
# all_sq_braqs[:10]
# text[:10]
```


```python
# double checking which lists are which for my next loop: finding the number of turns per speaker
len(line_fid)
len(utterance_num)
len(new_speaker_list)
len(unique_speaker)

# these 2 should not line up, just taking a peak at both
print("Unique Speaker List: length",str(len(unique_speaker)))
unique_speaker[:10]
print("New Speaker List for each line: length",str(len(new_speaker_list)))
new_speaker_list[:10]
```




    9026






    9026






    9026






    428



    Unique Speaker List: length 428
    




    ['ABCE1-P1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-C2', 'ABCE1-C3', 'ABCE1-C4', 'ABCE1-C5', 'ABCE1-C6', 'ABCE1-C7', 'ABCE1-C8']



    New Speaker List for each line: length 9026
    




    ['ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-E1', 'ABCE1-P1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1', 'ABCE1-C1', 'ABCE1-P1']




```python
'NAT4-C33b' in unique_speaker
# successfully got the letters to work!
```




    True




```python
# Finding number of turns per speaker
speaker_counts={}
speaker_counts_L=[]
for x in unique_speaker:
    count=0

    for y in new_speaker_list: # remember: new speaker list is the new speaker list for each line of the data
        if x==y:
            count+=1
    speaker_counts[x]=count
    speaker_counts_L.append(int(count))
```


```python
len(unique_speaker)

len(speaker_counts)  # no longer 6 short because I solved the NAT4 / NAT5 error
len(speaker_counts_L)

len(set(unique_speaker)) # 421 -> 428

print("A peak at individual speaker counts:")
speaker_counts_L[:100]
# Originally two people talked 2678 times, I fixed that issue
    # ABCE1-P1 Simon Marnie is showing up later in NAT files --- fix this!

len(speaker_infos)

unique_speaker[:100]

print("Simon Marnie:")
unique_speaker[0]
unique_speaker[15] # Simon Marnie is P1 for ABCE1 and ABCE2
speaker_infos[0]
speaker_infos[15] 
```




    428






    428






    428






    428



    A peak at individual speaker counts:
    




    [2677, 1955, 203, 212, 202, 184, 166, 165, 189, 149, 230, 342, 166, 113, 85, 1, 1, 1, 1, 1, 1, 1, 45, 1, 1, 1, 1, 1, 1, 1, 708, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 77, 85, 69, 79, 57, 1, 54, 34, 10, 13, 24, 45, 1]






    428






    ['ABCE1-P1', 'ABCE1-E1', 'ABCE1-C1', 'ABCE1-C2', 'ABCE1-C3', 'ABCE1-C4', 'ABCE1-C5', 'ABCE1-C6', 'ABCE1-C7', 'ABCE1-C8', 'ABCE1-C9', 'ABCE1-E2', 'ABCE1-C10', 'ABCE1-C11', 'ABCE1-C12', 'ABCE2-P1', 'ABCE2-E1', 'ABCE2-E2', 'ABCE2-C1', 'ABCE2-C2', 'ABCE2-C3', 'ABCE2-C4', 'ABCE2-E3', 'ABCE2-C5', 'ABCE2-C6', 'ABCE2-C7', 'ABCE2-C8', 'ABCE2-C9', 'ABCE2-C10', 'ABCE3-P1', 'ABCE3-P2', 'ABCE3-C1', 'ABCE3-C2', 'ABCE3-C3', 'ABCE3-C4', 'ABCE3-C6', 'ABCE3-C7', 'ABCE3-C8', 'ABCE3-C9', 'ABCE3-C10', 'ABCE3-C11', 'ABCE3-C12', 'ABCE4-E1', 'ABCE4-P1', 'ABCE4-C1', 'ABCE4-C2', 'ABCE4-C3', 'ABCE4-C4', 'ABCE4-C5', 'ABCE4-C6', 'ABCE4-C7', 'ABCNE1-P1', 'ABCNE1-E1', 'ABCNE1-C1', 'ABCNE1-C2', 'ABCNE1-C3', 'ABCNE1-C4', 'ABCNE1-C5', 'ABCNE1-C6', 'ABCNE1-C7', 'ABCNE1-C8', 'ABCNE1-C9', 'ABCNE2-P1', 'ABCNE2-E1', 'ABCNE2-C1', 'ABCNE2-C2', 'ABCNE2-C3', 'ABCNE2-C4', 'ABCNE2-C5', 'ABCNE2-C6', 'ABCNE2-C7', 'ABCNE2-C8', 'ABCNE2-C9', 'COME1-P1', 'COME1-E1', 'COME1-C1', 'COME1-C2', 'COME1-C3', 'COME1-C4', 'COME1-C5', 'COME1-C6', 'COME1-C7', 'COME1-C8', 'COME1-C9', 'COME1-C10', 'COME1-C11', 'COME1-C12', 'COME1-C13', 'COME1-C14', 'COME1-C15', 'COME1-C16', 'COME1-C17', 'COME1-E2', 'COME1-C18', 'COME1-C19', 'COME1-C20', 'COME1-C21', 'COME1-C22', 'COME1-C23', 'COME2-P1']



    Simon Marnie:
    




    'ABCE1-P1'






    'ABCE2-P1'






    'Presenter 1: Simon Marnie, M'






    'Presenter 1: Simon Marnie, M'




```python
speaker_counts_L[-100:]
# These are wrong -- Simon Marnie is taking some of their lines!!
```




    [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 4, 4, 1, 2, 4, 5, 4, 7, 4, 19, 2, 6, 6, 7, 1, 6, 4, 1, 3, 5, 8, 5, 3, 3, 4, 4, 5, 4, 4, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]



## Creating DataFrames
### Text DataFrame

The Data Frame art_df contains every line of text. The lines are organized by the unique speaker identifier and the utterance number of the file. The data frame also contains the filename (for searchability) and the line's text.


```python
# Text DataFrame
art_df = pd.DataFrame(new_speaker_list)
art_df.head()

art_df.columns = ["Speaker"]
art_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-P1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-E1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-P1</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-P1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-E1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-P1</td>
    </tr>
  </tbody>
</table>
</div>




```python
art_df["Utterance_Number"]=pd.DataFrame(utterance_num)
art_df["Filename"]=pd.DataFrame(line_fid)
art_df["Text"]=pd.DataFrame(text)
art_df.head()
art_df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th>Filename</th>
      <th>Text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
      <td>1</td>
      <td>ABCE1-raw.txt</td>
      <td>Thanks for that John Hall now John Hall will b...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
      <td>2</td>
      <td>ABCE1-raw.txt</td>
      <td>I guess yeah yeah &lt;laughs&gt;.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-P1</td>
      <td>3</td>
      <td>ABCE1-raw.txt</td>
      <td>He's also known &lt;E1 sounds reasonable&gt; for his...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-E1</td>
      <td>4</td>
      <td>ABCE1-raw.txt</td>
      <td>Okay.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-P1</td>
      <td>5</td>
      <td>ABCE1-raw.txt</td>
      <td>Jeanne Villani does and we'll find out the sec...</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th>Filename</th>
      <th>Text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9021</th>
      <td>COME1-C16</td>
      <td>359</td>
      <td>NAT8-raw.txt</td>
      <td>Thanks for that.</td>
    </tr>
    <tr>
      <th>9022</th>
      <td>ABCE1-P1</td>
      <td>360</td>
      <td>NAT8-raw.txt</td>
      <td>Uh let's see if we can just squeeze in one mor...</td>
    </tr>
    <tr>
      <th>9023</th>
      <td>NAT8-C17</td>
      <td>361</td>
      <td>NAT8-raw.txt</td>
      <td>Um okay yeah thanks for that Gaby.</td>
    </tr>
    <tr>
      <th>9024</th>
      <td>ABCE1-P1</td>
      <td>362</td>
      <td>NAT8-raw.txt</td>
      <td>That's alright.</td>
    </tr>
    <tr>
      <th>9025</th>
      <td>COME1-C17</td>
      <td>363</td>
      <td>NAT8-raw.txt</td>
      <td>Um and now that last caller I was just gunna s...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# how to do multi-level indexing
help(art_df.set_index)
```

    Help on method set_index in module pandas.core.frame:
    
    set_index(keys, drop=True, append=False, inplace=False, verify_integrity=False) method of pandas.core.frame.DataFrame instance
        Set the DataFrame index (row labels) using one or more existing
        columns. By default yields a new object.
        
        Parameters
        ----------
        keys : column label or list of column labels / arrays
        drop : boolean, default True
            Delete columns to be used as the new index
        append : boolean, default False
            Whether to append columns to existing index
        inplace : boolean, default False
            Modify the DataFrame in place (do not create a new object)
        verify_integrity : boolean, default False
            Check the new index for duplicates. Otherwise defer the check until
            necessary. Setting to False will improve the performance of this
            method
        
        Examples
        --------
        >>> df = pd.DataFrame({'month': [1, 4, 7, 10],
        ...                    'year': [2012, 2014, 2013, 2014],
        ...                    'sale':[55, 40, 84, 31]})
           month  sale  year
        0  1      55    2012
        1  4      40    2014
        2  7      84    2013
        3  10     31    2014
        
        Set the index to become the 'month' column:
        
        >>> df.set_index('month')
               sale  year
        month
        1      55    2012
        4      40    2014
        7      84    2013
        10     31    2014
        
        Create a multi-index using columns 'year' and 'month':
        
        >>> df.set_index(['year', 'month'])
                    sale
        year  month
        2012  1     55
        2014  4     40
        2013  7     84
        2014  10    31
        
        Create a multi-index using a set of values and a column:
        
        >>> df.set_index([[1, 2, 3, 4], 'year'])
                 month  sale
           year
        1  2012  1      55
        2  2014  4      40
        3  2013  7      84
        4  2014  10     31
        
        Returns
        -------
        dataframe : DataFrame
    
    

The speaker and utterance_number are the indices so that each index is unique.


```python
# Sets the index to the speaker and utterance number
art_df = art_df.set_index(keys=["Speaker","Utterance_Number"])
art_df.head()
art_df.tail() # note: speaker is wrong in the tail!! We know this because the unique_speaker code is not lining up with the filename.
    # The tail should only contain speakers from 1 file, but in this tail we see 3 different file speakers, even though all of these lines are uttered by people in 1 FILE!!
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Filename</th>
      <th>Text</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <th>1</th>
      <td>ABCE1-raw.txt</td>
      <td>Thanks for that John Hall now John Hall will b...</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>2</th>
      <td>ABCE1-raw.txt</td>
      <td>I guess yeah yeah &lt;laughs&gt;.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>3</th>
      <td>ABCE1-raw.txt</td>
      <td>He's also known &lt;E1 sounds reasonable&gt; for his...</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <th>4</th>
      <td>ABCE1-raw.txt</td>
      <td>Okay.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>5</th>
      <td>ABCE1-raw.txt</td>
      <td>Jeanne Villani does and we'll find out the sec...</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Filename</th>
      <th>Text</th>
    </tr>
    <tr>
      <th>Speaker</th>
      <th>Utterance_Number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>COME1-C16</th>
      <th>359</th>
      <td>NAT8-raw.txt</td>
      <td>Thanks for that.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>360</th>
      <td>NAT8-raw.txt</td>
      <td>Uh let's see if we can just squeeze in one mor...</td>
    </tr>
    <tr>
      <th>NAT8-C17</th>
      <th>361</th>
      <td>NAT8-raw.txt</td>
      <td>Um okay yeah thanks for that Gaby.</td>
    </tr>
    <tr>
      <th>ABCE1-P1</th>
      <th>362</th>
      <td>NAT8-raw.txt</td>
      <td>That's alright.</td>
    </tr>
    <tr>
      <th>COME1-C17</th>
      <th>363</th>
      <td>NAT8-raw.txt</td>
      <td>Um and now that last caller I was just gunna s...</td>
    </tr>
  </tbody>
</table>
</div>



### Speaker DataFrame

The Data Frame speaker_df lists each unique speaker's information, including their speaker type (P, C, or E) and their number of utterances.

**I will add their filename for searchability and their name since this is public data and anonimity is not necessary.**


```python
# Speaker DataFrame
speaker_df = pd.DataFrame(unique_speaker)
speaker_df.head()

speaker_df.columns = ["Filename_Speaker"]
speaker_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-C1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-C2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-C3</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Filename_Speaker</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-C1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-C2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-C3</td>
    </tr>
  </tbody>
</table>
</div>




```python
speaker_df["Speaker_Type"]=pd.DataFrame(unique_speaker_type) # is this right? investigate later
speaker_df["Gender"]=pd.DataFrame(gen)
speaker_df["Turns"] = pd.DataFrame(speaker_counts_L)
speaker_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Filename_Speaker</th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Turns</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABCE1-P1</td>
      <td>P</td>
      <td>M</td>
      <td>2677</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABCE1-E1</td>
      <td>E</td>
      <td>M</td>
      <td>1955</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABCE1-C1</td>
      <td>C</td>
      <td>F</td>
      <td>203</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABCE1-C2</td>
      <td>C</td>
      <td>F</td>
      <td>212</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCE1-C3</td>
      <td>C</td>
      <td>F</td>
      <td>202</td>
    </tr>
  </tbody>
</table>
</div>




```python
speaker_df = speaker_df.set_index("Filename_Speaker")
```


```python
speaker_df.head()

# I have filename_speaker, speaker type, and gender
# I added number of lines or "turns" <-- this might need editing
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Turns</th>
    </tr>
    <tr>
      <th>Filename_Speaker</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <td>P</td>
      <td>M</td>
      <td>2677</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <td>E</td>
      <td>M</td>
      <td>1955</td>
    </tr>
    <tr>
      <th>ABCE1-C1</th>
      <td>C</td>
      <td>F</td>
      <td>203</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>C</td>
      <td>F</td>
      <td>212</td>
    </tr>
    <tr>
      <th>ABCE1-C3</th>
      <td>C</td>
      <td>F</td>
      <td>202</td>
    </tr>
  </tbody>
</table>
</div>




```python
# help(speaker_df)
speaker_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 428 entries, ABCE1-P1 to NAT8-C17
    Data columns (total 3 columns):
    Speaker_Type    428 non-null object
    Gender          428 non-null object
    Turns           428 non-null int64
    dtypes: int64(1), object(2)
    memory usage: 8.4+ KB
    


```python
speaker_df.head(20)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Turns</th>
    </tr>
    <tr>
      <th>Filename_Speaker</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <td>P</td>
      <td>M</td>
      <td>2677</td>
    </tr>
    <tr>
      <th>ABCE1-E1</th>
      <td>E</td>
      <td>M</td>
      <td>1955</td>
    </tr>
    <tr>
      <th>ABCE1-C1</th>
      <td>C</td>
      <td>F</td>
      <td>203</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>C</td>
      <td>F</td>
      <td>212</td>
    </tr>
    <tr>
      <th>ABCE1-C3</th>
      <td>C</td>
      <td>F</td>
      <td>202</td>
    </tr>
    <tr>
      <th>ABCE1-C4</th>
      <td>C</td>
      <td>M</td>
      <td>184</td>
    </tr>
    <tr>
      <th>ABCE1-C5</th>
      <td>C</td>
      <td>M</td>
      <td>166</td>
    </tr>
    <tr>
      <th>ABCE1-C6</th>
      <td>C</td>
      <td>F</td>
      <td>165</td>
    </tr>
    <tr>
      <th>ABCE1-C7</th>
      <td>C</td>
      <td>F</td>
      <td>189</td>
    </tr>
    <tr>
      <th>ABCE1-C8</th>
      <td>C</td>
      <td>M</td>
      <td>149</td>
    </tr>
    <tr>
      <th>ABCE1-C9</th>
      <td>C</td>
      <td>M</td>
      <td>230</td>
    </tr>
    <tr>
      <th>ABCE1-E2</th>
      <td>E</td>
      <td>F</td>
      <td>342</td>
    </tr>
    <tr>
      <th>ABCE1-C10</th>
      <td>C</td>
      <td>F</td>
      <td>166</td>
    </tr>
    <tr>
      <th>ABCE1-C11</th>
      <td>C</td>
      <td>F</td>
      <td>113</td>
    </tr>
    <tr>
      <th>ABCE1-C12</th>
      <td>C</td>
      <td>M</td>
      <td>85</td>
    </tr>
    <tr>
      <th>ABCE2-P1</th>
      <td>P</td>
      <td>M</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE2-E1</th>
      <td>E</td>
      <td>M</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE2-E2</th>
      <td>E</td>
      <td>M</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE2-C1</th>
      <td>C</td>
      <td>F</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE2-C2</th>
      <td>C</td>
      <td>F</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
len(speaker_counts_L)
```




    428




```python
# dataframe of presenters
P_df=speaker_df.loc[speaker_df["Speaker_Type"]=='P',:]
P_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Turns</th>
    </tr>
    <tr>
      <th>Filename_Speaker</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-P1</th>
      <td>P</td>
      <td>M</td>
      <td>2677</td>
    </tr>
    <tr>
      <th>ABCE2-P1</th>
      <td>P</td>
      <td>M</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE3-P1</th>
      <td>P</td>
      <td>F</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE3-P2</th>
      <td>P</td>
      <td>F</td>
      <td>708</td>
    </tr>
    <tr>
      <th>ABCE4-P1</th>
      <td>P</td>
      <td>F</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# dataframe of callers
C_df=speaker_df.loc[speaker_df["Speaker_Type"]=='C',:]
C_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Turns</th>
    </tr>
    <tr>
      <th>Filename_Speaker</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-C1</th>
      <td>C</td>
      <td>F</td>
      <td>203</td>
    </tr>
    <tr>
      <th>ABCE1-C2</th>
      <td>C</td>
      <td>F</td>
      <td>212</td>
    </tr>
    <tr>
      <th>ABCE1-C3</th>
      <td>C</td>
      <td>F</td>
      <td>202</td>
    </tr>
    <tr>
      <th>ABCE1-C4</th>
      <td>C</td>
      <td>M</td>
      <td>184</td>
    </tr>
    <tr>
      <th>ABCE1-C5</th>
      <td>C</td>
      <td>M</td>
      <td>166</td>
    </tr>
  </tbody>
</table>
</div>




```python
# dataframe of experts
E_df=speaker_df.loc[speaker_df["Speaker_Type"]=='E',:]
E_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Speaker_Type</th>
      <th>Gender</th>
      <th>Turns</th>
    </tr>
    <tr>
      <th>Filename_Speaker</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ABCE1-E1</th>
      <td>E</td>
      <td>M</td>
      <td>1955</td>
    </tr>
    <tr>
      <th>ABCE1-E2</th>
      <td>E</td>
      <td>F</td>
      <td>342</td>
    </tr>
    <tr>
      <th>ABCE2-E1</th>
      <td>E</td>
      <td>M</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE2-E2</th>
      <td>E</td>
      <td>M</td>
      <td>1</td>
    </tr>
    <tr>
      <th>ABCE2-E3</th>
      <td>E</td>
      <td>M</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>




```python
P_df.info()
C_df.info()
E_df.info()

# There are a lot more Callers than there are Presenters and Experts, but there are about equal numbers of Presenters and Experts
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 32 entries, ABCE1-P1 to NAT8-P1
    Data columns (total 3 columns):
    Speaker_Type    32 non-null object
    Gender          32 non-null object
    Turns           32 non-null int64
    dtypes: int64(1), object(2)
    memory usage: 640.0+ bytes
    <class 'pandas.core.frame.DataFrame'>
    Index: 360 entries, ABCE1-C1 to NAT8-C17
    Data columns (total 3 columns):
    Speaker_Type    360 non-null object
    Gender          360 non-null object
    Turns           360 non-null int64
    dtypes: int64(1), object(2)
    memory usage: 7.0+ KB
    <class 'pandas.core.frame.DataFrame'>
    Index: 36 entries, ABCE1-E1 to NAT7-E1
    Data columns (total 3 columns):
    Speaker_Type    36 non-null object
    Gender          36 non-null object
    Turns           36 non-null int64
    dtypes: int64(1), object(2)
    memory usage: 720.0+ bytes
    


```python
# Looking at the Presenter DF
P_df.max() # 2677
P_df.min() # 1
P_df.sum() # 3490
# help(P_df["Turns"])
```




    Speaker_Type       P
    Gender             M
    Turns           2677
    dtype: object






    Speaker_Type    P
    Gender          F
    Turns           1
    dtype: object






    Speaker_Type    PPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPP
    Gender          MMFFFMMMMMMFMMMMMMMMMMFMMFFMMFFF
    Turns                                       3488
    dtype: object




```python
P_df.describe()
C_df.describe()
E_df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Turns</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>32.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>109.00000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>485.03096</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2677.00000</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Turns</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>360.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>8.669444</td>
    </tr>
    <tr>
      <th>std</th>
      <td>32.735271</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>230.000000</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Turns</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>36.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>65.972222</td>
    </tr>
    <tr>
      <th>std</th>
      <td>328.823138</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1955.000000</td>
    </tr>
  </tbody>
</table>
</div>



There are a lot more callers than there are presenters and experts.
This means that the presenters and experts are probably more comparable. However, this will depend on the number of words that are actually uttered by the presenters vs. experts.
On average, presenters take about 109.06 turns. However, there is a very high standard deviation of 485. I believe that this is
because Simon Marnie talks a lot and is in 2 files. Experts had on average 65.97 turns, but also had a high standard deviation of about 329. 
The max for presenters (Simon Marnie) was 2677 and for experts it was 1955. These are outliers and are skewing the data.
In radio show talks, callers typically are only on the air for a minute or two. This explains why there are so many callers
with such low numbers of turns. On average, callers had almost 9 turns. The standard deviation is much lower, partially due to the large number of callers. The max, 230, still seems very high for callers and this may also be an outlier. 


Based on this corpus, the presenters (the show's hosts) take the most number of turns throughout the show.


As for who actually talks the most, I will be looking into that in my next analsis, which will involve word and sentence tokens.


Similarly, I will do an analysis on vocabulary size and sentence length to compare across types of speakers
