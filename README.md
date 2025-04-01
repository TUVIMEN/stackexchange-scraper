# Archive

Any further development has been transfered to [forumscraper](https://github.com/TUVIMEN/forumscraper).

# stackexchange-scraper

A bash script for scraping stackexchange forums in json.

## Requirements

 - [reliq](https://github.com/TUVIMEN/reliq)
 - [jq](https://github.com/stedolan/jq)

## Installation

    install -m 755 stackexchange-scraper /usr/bin

## Supported sites

All supported sites can be found [here](https://stackexchange.com/sites)

## Supported links formats

    https://example.stackexchange.com
    https://stackoverflow.com
    https://example.stackexchange.com/questions
    https://example.stackexchange.com/tags
    https://example.stackexchange.com/questions/tagged/some-tag
    https://example.stackexchange.com/questions/19924
    https://example.stackexchange.com/questions/19924/issue-title

## Json format

Here's [json](example.json) from one of the most popular issues on [stackoverflow](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)

## Usage

    stackexchange-scraper directory [URLS...]

All options should be specified before the directory.

The script writes every question to file in the directory (without overwriting them) and names of the files is the ids of questions.

Size of the page is 50 questions.

Since ids of the questions overlap with different websites it is recommended to download them into separate directories.

Download all tags to directory x with delay of 0.2 second and randomness of 3 seconds

    stackexchange-scraper -d 0.2 -r 3 x 'https://stackoverflow.com/tags'

Download all questions tagged python to directory x while using 5 processes

    stackexchange-scraper -p 5 x 'https://stackoverflow.com/questions/tagged/python'

Download all questions starting from 50th page to 75th page to directory x

    stackexchange-scraper -f 50 -l 75 x 'https://stackoverflow.com'

Download some questions to directory x

    stackexchange-scraper x 'https://stackoverflow.com/questions/3737139/reference-what-does-this-symbol-mean-in-php' 'https://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php' 'https://stackoverflow.com/questions/391005/how-can-i-add-html-and-css-into-pdf'

Get some help

    stackexchange-scraper -h

## Issues

### Too Many Requests

Be warned that you should limit your requests to all of the websites from stackexchange family as the protection counts requests for all of them.

### Large directory feature is not enabled on this filesystem

Storing a lot of files in a single directory (around 7 milion) will cause bash to show errors of lack of space (even when there is space and free inodes).

Dmesg will show you something like this:

    [979260.318526] EXT4-fs warning (device sda1): ext4_dx_add_entry:2516: Directory (ino: 89391105) index full, reach max htree level :2
    [979260.318528] EXT4-fs warning (device sda1): ext4_dx_add_entry:2520: Large directory feature is not enabled on this filesystem
