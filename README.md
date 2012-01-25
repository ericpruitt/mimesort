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


Usage
-----

The scripts usage is pretty simple:

    mimesort.py [OPTIONS] [DIRECTORY... [DESTINATION]]

When no directory is supplied, mimesort works on the current working directory
but prompts the user before proceeding. When multiple directories are supplied
as arguments, the last folder is used as the destination for the sorted
contents of the preceding folders.


Example
-------

    ~/Downloads$ mimesort -d 0.6 | tail -n15
    ./shellinabox_2.10-1_amd64.deb                     debian-package
    ./Bat Euthanasia.pdf                               pdf
    ./AmazonMP3-1309433311.amz                         plain
    ./cruisecontrol-bin-2.8.4                    1.566 mixed
    ./WebShell-0.9.6                             1.476 mixed
    ./kien-ctrlp.vim-e50970f.tar.gz                    tar
    ./531 Manual.pdf                                   pdf
    ./xflux.tgz                                        tar
    ./mHXiz.png                                        image
    ./Full ...otherhood 1-64 (Eng Dub)           0.000 video
    ./Sunflower-0.1a-26.tgz                            tar
    ./ipmansubs.zip                                    zip
    ./Pokemans.mp3                                     audio
    ./Windo...it-English-Developer.iso                 iso9660-image
    ./amazonmp3                                  0.000 debian-package

    ~/Downloads$ ls
    audio           iso9660-image   pdf                     shellscript
    csv             java-archive    plain                   tar
    debian-package  java-jnlp-file  postscript              unknown
    document        message         redhat-package-manager  video
    executable      mixed           ruby                    xml
    image           msdos-program   sh                      zip


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
