# siPhon
## Read and extract files from an iPod or other similar music storage without resorting to iTunes

### What is it?

This is a simple utility that will take a directory full of badly named MP3 or M4A (or maybe a couple other things) files in basically random order, and compile a database which you can then use to determine which music is actually there.  You can list songs, artists, albums.  You can copy them back out into files with something like appropriate filenames in a structure that is less anoying than what you had to start out.

### Why?

iTunes handles the storage of audio on Apple players poorly.  It splits the set of audio files on the device into about 50 different directories in the music folder, and just fills those directories up with files given meaningless, four-character names.  The iTunes database knows where the music is, but looking at the device, you won't.  If you want to pull some music back off of your iPod, say, to load it locally onto a machine and play it there, or whatever, it's not an easy thing to do.  This software fixes that.  You could, in fact, do something similar with a few different MP3 tag management applications, but none of those were quite as simple to configure and reconnfigure as I wanted.

## How?

We scan the whole disk (or at least the directory you specify, inefficiently; it takes a few minutes on the average iPod), reading the tags in the media files and compiling a database of information on your music.  This database is similar to the one iTunes itself builds, but separate from it.  It will not be automatically maintained, so you may need to rebuild it after you make changes.  It stores this database on the device in a directory called *siPhon-db*, so you'll need write access to the filesystem for this to work.  If you're just trying to pull data out and, for example, you've got a Mac format iPod on a Linux system without writable HFSPlus, you can specify a different database directory on a writable filesystem using the *--db* option.  The database will be created (or loaded from) there.
Once the scan is done, you can list out your albums, artists, or songs.  You can also copy them out to another place, automatically renaming them in transit.

### Installation

There really is none to speak of.  Put it somewhere from which you can run it.

#### Prerequisite Python libraries

   * Mutagen, for ID3 tags and so on.
   * python-magic, for recognition of files by magic number (yes, in theory, we don't even need good file extensions.

### Usage

First, mount your device somewhere, scan it and build the database:

```$ siPhon -i /mnt/IPOD scan ```

Now, dig through your music collection, for example:
```
$ siPhon -i /mnt/IPOD ls -a Kansas
Artist: Kansas / Album: Point Of Know Return
Name: Nobody's Home / File: ./iPod_Control/Music/F00/BMXG.mp3
--------
Artist: Kansas / Album: Kansas
Name: Wheels / File: ./iPod_Control/Music/F00/PLWZ.mp3
--------
Artist: Kansas / Album: In The Spirit Of Things
Name: Ghosts / File: ./iPod_Control/Music/F03/VVWA.mp3
--------
Artist: Kansas / Album: In The Spirit Of Things
Name: T.O. Witcher / File: ./iPod_Control/Music/F03/ENIL.mp3
--------
Artist: Kansas / Album: Point Of Know Return
Name: Point Of Know Return / File: ./iPod_Control/Music/F03/WAIL.mp3
--------
Artist: Kansas / Album: Power
Name: Secret Service / File: ./iPod_Control/Music/F03/TYTH.mp3

```

To pull music out, do something like:

```
$ siPhon -i /mnt/ipod get -a Kansas -A Power -o Music/extracted
```

See ```$ siPhon -h ``` for more.

