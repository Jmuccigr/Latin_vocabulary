# Latin Vocabulary
This is a plain-text dump of the data from my FileMaker Pro relational database of Latin vocabulary and stems. I created it in the early 2000s, starting on FMP 3 and moving up to FMP 6. I used it a lot when I was teaching elementary Latin, and the formal product of it was an article: [Frequent Vocabulary in Latin Instruction, *Classical World* 97(4), 409–433](http://www.jstor.org/stable/4352875).

## The Conversion
Getting the data out of FMP and into this flat format required a few steps. First was updating the files. I already had FMP3 versions along with the FMP6 version I had done most of the work in. (Thatʻs .fp3 and .fp5 for the file extensions.) Sadly FMP12, which is what Iʻm now using, doesnʻt directly read the .fp5 format at all, and FMP6 is a Classic app, which OS X 9 (Mavericks) canʻt run directly. So hereʻs what I did:

  1. Create a virtual OS X 10.6 (Snow Leopard) box on my Mavericks system. Snow Leopard was the last OS X version to be able to run the Apple Classic emulator, Rosetta. That took a little doing, since I updated the various sytem pieces as needed. Not that this version can be super secure, but I just wanted it as close as possible.
  1. Convert the old .fp5 files to .fp7 with FMP 8 (I keep a few versions of FMP around).
  1. Archive the old .fp5 files as a zip file.
  1. Switch back to Mavericks.
  1. Archive the old .fp7 files. I realized that the conversion process forced me to rename the originals, and zipping left them there, so I cold skip the step of restoring the old filenames.
  1. Convert the .fp7 to .fmp12.
  1. Export the FMP files as text. Iʻm using UTF-16 for this, because the database uses diarheses for long vowels (äëïöü). Since this is gong from relational to flat files, I had to decide which data to include in the exports.
  1. Convert the diarheses to macrons (āēīōū). I did this using BBEdit.
  1. Import the new stems with macrons back into FMP. I did it this way because search and replace on BBEdit is faster than in FMP.
  1. Put the text files here.
  
## File Details
The various files have different data fields, of course, but all of them include an arbitrary ID field which was used as the key in the relational database. Below I'll comment only on fields which would seem to need it.

### Stems.tab - Latin stems
  * Type - nearly all of these are stem (basically the root vs. prefix or suffix of a word) morphemes. I intended to add more of the others, but didn't get around to it.
  * Count - a count of all the times the stem was attached to a vocabulary item in my database. Again, I never systematically finished attaching all the stems to all the items, but I think I did a fairly good job, so that the higher this number, the more common the stem is. If anyone forks this file, they can ignore this field.

### Vocab.tab - the vocabulary items
This is fairly self-explanatory. The columns in which 1 appears as an entry (except for the ID) use Booleans and I didn't include 0, where applicable (which is most of the time). I think I was pretty good about identifying morphological groups (*e.g.*, abstract nouns in -tas), but not so good about sense groups (*e.g.*, family terms).

### Readings.tab - the "readings"
This file contains all the sources I used for the vocabulary, which I called readings, even if they were simply chapters from textbooks or excerpts from longer readings. This is another place where the relational database came in handy, as I could link vocab items to readings, but here in the flat file I included a list of all the vocab items for each reading.

  * Name - the identity of the reading, often a textbook chapter.
  * Author - the author of the work I took the readings from, not necessarily an ancient author.
  * Title - again, the title of the work I got the vocab lists from.
  * Citation - a very abbreviated version.
  * VocabCount - the number of vocab items **I** counted, which is not necessarily the same number of items in the original. For example, the original might have broken down the first-person proun into separate entries for separate cases, but I didn't.
  * VocabID - this is the same ID that appears in the Vocab.tab file, so you could recreate the relationships, if you wanted.
  * VocabItem - my own form of the Latin part of the vocab item. This should be enough to dis-ambiguate the item.
