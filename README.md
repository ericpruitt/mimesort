mimesort
========

Mimesort is used to sort files and folders into labeled folders based on MIME
types. When deciding what MIME classification to use for a folder, mimesort
checks the MIME type of every file within the folder and will classify a folder
based on the most commonly occurring type. By default, if the MIME types that
occur in a folder are not all the same, the folder is classified as "mixed."
This can be changed by adjusting the diversity threshold. The diversity of a
folder is determined by the [Shannon
index](http://en.wikipedia.org/wiki/Diversity_index#Shannon_index) of the MIME
types of its contents.

I have a nightly entry in my crontab that I use to sort my downloads directory:

    mimesort.py  -d .6  ~/Downloads

A Shannon index threshold of 0.6 does a good job of classifying folders to my
liking, but I recommend doing some dry-runs to see works best for you.


Options
-------

### -h ###

Displays a brief overview of the command line arguments accepted by mimesort.

### -d _NUMBER_ ###

Defines the threshold for determining whether or not a folder is classified as
"mixed" instead of the most commonly occurring MIME type. The default threshold
is 0.0.

### -i ###

Tells the script not to try to sort folders that, based on the folder names,
appears to already be sorted.

### -n ####

Displays a list of files, folders, their Shannon index values and
classifications but does not actually move anything around. This is essentially
a dry-run.

### -m ###

Do not use magic file libraries even if they are available. This is useful for
categorizing large quantities of files since the magic file libraries read data
from the file to determine its type, but the classifications will generally be
less accurate.

### -y ###

When mimesort is called without any arguments, it will attempt to sort the
current working directory but prompts the user before doing so. This argument
eliminates the prompt and will sort the current working directory immediately.


Usage
-----

The scripts usage is pretty simple:

    mimesort.py [OPTIONS] [DIRECTORY... [DESTINATION]]

When no directory is supplied, mimesort works on the current working directory
but prompts the user before proceeding. When multiple directories are supplied
as arguments, the last folder is used as the destination for the sorted
contents of the preceding folders.
