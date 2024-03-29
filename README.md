# semantic-change-hansard


Author: Japleen Gulati 
Please reach me on japleengulati@gmail.com for any questions from here!

NOTE:
In each of the folders - BaselineModel, Retrofitting, VanillaModel, WeightedSimilarityExperiments,
the .py file contain amended code only meant for the generation of the master table called by masterTable.py
-they DO NOT contain the whole code

The other experiments conducted for a model and the larger picture is available in the python notebooks present in the folders

- x - x - x - x - x - x - x - x - x - x - x - x - x - x - x - x - x 

Retrofitting ReadME details (also inside the retrofitting folder)

RETROFITTING 

For working with Faruqui et al's retrofitting code, there is pre and post processing required which will be carried out using these 3 scripts:

1.	Synonyms' creation
2.	Input vectors' creation
3.	Drawing results from output-retrofitted vectors

I.	Synonym Creation Script

Requirements:
●	mpTimeDf.pkl

To run: 
1.	Import mpTimeDf.pkl, define its path in the variable picklePath
2.	In the main(), initiate synonymFactor as one of - ‘party’ or ‘party-time’ depending on if we want to make synonym pairs based on the same party 
alone or of MP records belonging to the same party and the same time interval. 
3.	In the main(), initiate synPicklePath and synTextPath in sync with the synonyms being created. E.g. ‘synonymsParty.pkl’
4.	Run and download the generated pickle and text files for the synonym pairs.

II.	Input Vectors’ Creation Script

Requirements:
●	24 aligned work2vec Mp-time models
●	Synonyms pickle file e.g. synonymsParty.pkl

To run: 
1.	Define synonymsPath and folderPath and import synonyms pickle file and 24 MP-time models
2.	In create_input_vectors() initiate vectorFileName as the input vectors file name required. E.g. 'vectorsPartyTime.txt'
3.	Run all and download the generated vectors text file to use as input for faruqui’s code

III.	Run Faruqui’s Python 3 modified code with input vectors file, synonyms file generated. 
Add synonyms.txt to lexicons folder, vectors.txt file to the main code folder.

The command would be something such as:

```python retrofit.py -i vectorsParty.txt -l lexicons/synonymsParty.txt -n 10 -o out_vecParty.txt```

 “where, 'n' is an integer which specifies the number of iterations for which the
optimization is to be performed.  Usually n = 10 gives reasonable results.”


IV.	Read Retrofitted vectors, find cosine similarity & run ML

Requirements:
●	24 aligned work2vec Mp-time models
●	Synonyms pickle file e.g. synonymsParty.pkl

To run: 
1.	Define synonymsPath and folderPath and import synonyms pickle file and 24 MP-time models
2.	Define retrofittingFactor as ‘party’ / ‘party-time’ etc
 

Although the 3 scripts have been modified to work for different basis for retrofitting,
such as retrofitting using the same party, or considering the same party and time, 
the result generation doesn’t generate the table for ALL factors automatically. 
The sci-kit learn to make these scores is somehow failing to run when provided with a different retrofittingBasis in the same execution. 
Once in many attempts, it worked, but mostly it’s not working and will probably have to be done once for a factor per notebook-session. 
The result can be exported as a pickle file and then the script can be run for a different retrofitting factor. 

 