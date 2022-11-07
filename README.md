See IAM-Reference-Architecture.md for purpose

The main document is IAM-Reference-Architecture.md
It incorporates the png versions of the graphic model

The graphic model is built using the drawio tool. It is layered. 

The the prepare_figures script generates the png files, but requires manual intervention to select the correct layers from the model. The script refers to figures.txt for the list of figures.

Resources folder holds output from the graphic model and the reference doc for pandoc to create the word version.

The make_word script simply converts the markdown to MS word and puts the result in the output file.

If a collaborator provides edits in Word, save that as work.docx.  Complete the review, accepting, rejecting editing etc in work.docx.  Then run ./word2md.  This will create a work.md document you can inspect.  Once satisfied, copy that over the IAM-Reference-Architecture.md file.
