# cruzviz-vim

I use MacVim for web development (HTML/CSS/JavaScript) and Python coding. This is the .vimrc file I use to make it pretty and more IDE-like.

I'm really not a wizard with Vim and vi commands, I slowly learn new shortcuts here and there, and am nowhere near using them all. I still use all the standard Mac system commands like Command-z, Command-c, and Command-v for undo, copy, and paste inside Vim. This README documents what I do know and try to use. I am sharing the vimrc and this README for two reasons: 1) in case it helps anybody else, especially beginners, and 2) for my future self, because I forget how to do anything in vim if I stop using it for a few months, and I will surely have to install it on a new machine someday, which I need to remember how to do.

[Note to self:] My next to-do items to get more out of Vim: 1) figure out and actually use NERDtree to navigate my file system from inside Vim (it's installed but I don't use it, I just use the MacVim GUI, the Mac Finder, and/or terminal); and 2) start using split layouts and keeping Vim full screen (I currently keep each file in its own window, and I find myself clicking/dragging/resizing all my different Vim windows quite a bit when I work with on more complex projects). If I had both of these items figured out, I could use keyboard shortcuts within Vim to very quickly jump around between and open/close multiple files in various directories, and keep everything visually organized so I could see all my source files at once.

## Getting started with Vim - the super basic basics
Vim has 3 main "modes" - NORMAL, INSERT, and VISUAL.

1) When you first open Vim, it is in NORMAL mode, with a fat cursor that covers a whole character space. This is actually a command mode where you can skip your cursor around easily, save (write) the file, and generally perform various tricks. Hit `<esc>` (the Escape key) to enter NORMAL mode from any other mode, or to cancel any partially constructed NORMAL mode command.

2) INSERT mode is what some of us might consider "normal" word processing mode: there is a skinny cursor in between subsequent character spaces, and you type on the keyboard to add text to the file. From NORMAL mode, you can enter INSERT mode by typing `i` ('i'nsert) to place the skinny cursor just to the left of the NORMAL fat cursor, or `a` ('a'ppend) to place the skinny cursor to the right.

3) VISUAL mode is for selecting text. From NORMAL mode, type `v` ('v'isual) to enter VISUAL mode, with your current location as the starting point. Once you hit `v` and start moving the cursor around, you are highlighting everything in between the starting point and the cursor.

## Initial set-up
* Install a nice modern graphical version of vim. gVim for Windows, MacVim for Mac. I use MacVim, which is `mvim` from the terminal. I'm pretty sure gVim works the same way but is called `gvim` at the terminal.
  * `mvim {new filename}` entered at a terminal window opens a new file inside MacVim at the present working directory.
  * `mvim {existing filename}` opens an existing file for editing inside MacVim. More often I will just double-click the file in Finder, since I've set up most of my code file types (*.css, *.js, *.csv, *.txt, *.py) to use MacVim as the default program (using System Preferences). For HTML files, though, I have to right-click and 'Open with..' MacVim.
  * For example, `mvim .vimrc` from the directory containing .vimrc will open the .vimrc file inside MacVim. The terminal is necessary to use for hidden files, or directories that the Mac Finder won't let you see.
* Make sure the .vimrc file resides in your home directory so Vim can find it. This is usually the default directory when you open a new terminal. On my MacBook, it's the directory `/Users/<myusername>`, which contains Applications, Desktop, and Documents, among others. This directory isn't actually accessible through the Finder, you need to use a terminal to get here.
* Install all the Vundle plug-ins by typing `:PluginInstall<return>` in NORMAL mode (from inside any Vim buffer).
* I set the font Vim uses to be [Hack](http://sourcefoundry.org/hack/), so that font needs to be installed on your system. Feel free to change this to a different font if you want; it's the last line of .vimrc.
* Install any popular linters you might need for the type of coding you do (such as `pylint` for Python) and make sure they are accessible (i.e. in your $PATH). [Syntastic](https://github.com/scrooloose/syntastic) does syntax checking using external system-installed linters. Read the FAQ at the Syntastic GitHub site if you're having problems. If everything is working correctly, you should see some errors appear when you save (`:w`) a code file with improper syntax - for example, saving a *.py file which has some PEP8 violations - which then disappear after you fix the errors and re-save.

# CHEAT SHEET (stuff I actually use)

##NORMAL mode:

1) File commands: `:w` to save/write the file and find syntax errors; `:wq` to save and then quit (close the window), `:q!` to quit without saving changes. These only apply to the current window, not to all open files inside Vim.

2) `/{stuff}` searches the file for all instances of `{stuff}` and highlights them all. Once that is done, you can type `N` or `n` to jump around all these instances (backwards and forwards, respectively). To turn the highlighting off again, type `\ ` - that's backslash followed by the spacebar.

3) Jumping around:
  * `$` jumps to end of line, `0` jumps to beginning of line
  * `W`/`w` jumps to next word, `B`/`b` jumps 'b'ack to previous word
  * `{line number}G` jumps ('G'Os) to a specific line number, or `G` by itself goes to end of file

4) Delete a whole line with `dd` or 'd'elete multiple lines at once with `d{x}<return>` where {x} is the number of lines to delete.

5) `r{new character}` 'r'eplaces a single character. It overwrites the character underneath the cursor with the {new character}.

##VISUAL mode:

1) Use all the jumping around commands from NORMAL mode to quickly highlight what you need.

2) To de-indent or indent highlighted lines, `<` or `>` respectively.

3) You can access the system clipboard for cutting, copying, or pasting-over using the usual Command-x, Command-c, Command-v (on a Mac).

WARNING! To paste in a brand new chunk of text rather than overwriting existing text, it is better to enter INSERT mode to get the cursor placed correctly and then use Command-V. The Vim shortcut commands are `p` vs `P` for pasting before vs after the cursor, but I never remember which is which and it's a pain in the ass to have that one beginning or ending character end up in the wrong spot.

##EMMET

Emmet (aka Zen Coding) is a system for writing cumbersome chunks of HTML very efficiently. Emmet shortcuts can be used in any file with a *.html extension.

See the [Emmet cheatsheet](http://docs.emmet.io/cheat-sheet/).

To implement inside Vim:

1) Write out the Emmet shortcut (i.e. `html:5>table>th>td*6^tr*5>td*6`) in INSERT mode.

2) Then hit `<esc>`, the Escape key, to enter NORMAL mode.

3) Make sure the cursor is covering the last character of your Emmet shortcut. Then hit `<tab>`, the Tab key.

Done! If you don't like it, Command-z to undo it and try again.
