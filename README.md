# Tools

A collection of tools for modding Victoria 2.

## Usage

Add `tools` as a remote to the repository

`git remote add tools https://github.com/napoleons-legacy/tools.git `

This adds the repository as a remote to fetch changes from. To get the latest change:

```sh
git fetch tools
git checkout -p tools/master [files to take here]
```

`util.py` is a file that is used in all other programs and is required as a result.

Files that can be deleted after the first fetch for general use:

* Pipfile and Pipfile.lock
* requirements.txt if `pip install -r requirements.txt` has already been run.

## Programs

### util.py

This program has no direct usage, but is instead used to find the mod directory agnostic of project. To minimize issues, have a correct `.mod` file definition and store only one `.mod` file in the directory.

### install.py

`python install.py`

This installs the mod into the game directory.
This removes the need to:

* Have the working directory be inside the `Victoria 2/mod` folder.
* Copy over the project to the `Victoria 2/mod` folder for testing.

### cleanup.py

`python cleanup.py`

This cleans up the entire project style.
This program:

* Changes all tabs to four spaces since tabs are platform dependant. Some applications render tabs as two, four, or eight spaces. This keeps it consistent.
* Change all line endings to the UNIX line ending `\n` over the Windows line ending `\r\n`. This improves compatibility with Git.
* Adjusts all files so that there are no line endings at the start of the file and that there is always one line ending at the end of the file. This avoids the issue of `history/provinces` consuming the last character of the file leading to issues such as `life_rating` issues. This also removes the message from Git indicating there is no line ending at the end of the file.
* Remove all trailing spaces at each line. These spaces have no function so this reduces file size.

### localization.py

`pip install -r requirements.txt` For first time use.

`python localization.py`

This deduplicates localization entries and normalizes the .csv file.

* Allows for the manual review of duplicate localization entries. The chosen entry number will be the only remaining instance left afterwards.
* `<CTRL+C>` Allows for progress to be saved at any point in the program.
* By default, the indicated duplicates show a prompt to have their files opened in whatever is designated as the editor for .csv files.
* A confirmation prompt is shown indicating what keys have been removed and in what file.
* On export, a proper header is added to the file. Semi-colon quantity is adjusted such that there will always be 14 of them, matching the game localization spec defined on the modding wiki.
* Entries that are similar to `x,,,`; contain only the character's `x` and `,` are removed since they have no actual functionality.

`python localization.py --help` For usage information.
