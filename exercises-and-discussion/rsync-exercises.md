# Try out Rsync for yourself!

If you don't already have Rysnc installed, follow the instructions at the top of the [Rsync guide](https://github.com/andreakb/parallel-lines-workshop/blob/master/tools/rsync.md)

If you need a corpus of files to play with for these exercises, use our set of files from one of our born-digital accessions, E4 that we made available [here](https://github.com/andreakb/parallel-lines-workshop/tree/master/corpus). You can find and access all these files in our holdings in [Archway](https://archway.archives.govt.nz/CallSeriesAdvancedSearch.do) by doing an advancded search for series code 7505.

A note about modification dates: They are tricky beasts to maintain  over web platforms! The modification dates you'll see after downloading the files from github reflect the date the files were uploaded to github, not the actual modification dates.

1. Use Rsync to transfer the corpus files (and just the corpus files under the Peter Dunne -E4 folder ) from the parallel-lines-workshop folder to your home directory in a folder called  "Peter Dunne -E4"

  * Try doing this a couple times by deleting the new "Peter Dunne -E4" directory and re-running Rsync with different options to compare and contrast how the options work. You can also see what will happen by using the `-n` (trial run) option. Try transferring files to other locations besides your home directory.

  * During a transfer process, have Rsync create a csv file containing modification dates, checksums and filenames.

2. Using the heroes.txt and the rogues.txt files in the corpus directory, create two new directories on your home directory, one with the files listed in the heroes.txt and one with just the files listed in rogues.txt.

3. Change something in one or more of the files on one of the new directories on your home directory. For example, actually open up one of the doc files in office ,and edit some of the text and save it. Then use `--inplace` to restore the file(s) to it's original state.

4. Delete some of the files in of the directories in your home directory. Try using the `--inplace` option again to restore the file(s) to their original state.
