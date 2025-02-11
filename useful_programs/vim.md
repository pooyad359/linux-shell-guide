# Vim

## Operators
- `y`: Yank (copy)
- `d`: Delete and save to register
- `c`: Delete and save to register and start insert mode
- `p`: Paste yanked text after cursor
- `P`: Paste yanked text before cursor
- `dd`, `cc`, `yy`: delete/copy the entire current line

### Other operators
- `<`: Indent Left
- `>`: Indent right
- `=`: Auto indent
  - `=`, `<`, `>` can be used twice to apply to the current line (`==`) or with number to apply to multiple lines (`3<<` for three lines)
- `!! <command>`: Will replace the current line with the output of shell command
  - `!! tr _ -`: To replace `_` with `-` in the current line
  - `date`: To insert current timestamp to the current line
- `:! <command>`: Passes the current lines to the shell command and replaces them with the output. Use with visual mode (`Ctrl-V`) to select multilines
  - `:! sort`: Sort the selected lines
  - `:! grep <keyword>`: Only keep the lines that contain `keyword`
- `gU`: Convert to uppercase. E.g., `gUiw` to convert the current word to uppercase
- `gu`: Convert to lowercase.
- `g~`: Swap case

### Combine with motion
Operators can be combined with a motion to specify what they should act on. Examples:
- `yw`: yank from cursor to the end of the word
- `d}`: delete from cursor to the end of paragraph
- `c$`: delete from cursor to the end of line
- `d2w`: delete the next two words (from cursor)
- `d2j`: delete the current line and the next two lines

### Text Objects
You can apply the operators to a text objects, such as parantheses, brackets, quotes, etc.
- `i`: For inner object
- `a`: For outer object

Examples:
- `di(`: Delete the text in the parentheses
- `da(`: Delete the paratheses including the text inside

Objects:
- `w`: current word. Example: `diw` to remove the entire word under the cursor
- `p`: current paragraph
- `s`: current sentence
- `(`, `)`, `{`, `}`, `<`, `>`, `[`, `]`, `"`, `'`, or `` ` ``: for current pair

### Undo/Redo
You can undo changes by pressing `u`. To redo the undone changes press `Ctrl-R`. Both can be combined with a number to repeat the action, e.g., `3u` to undo the last three changes.


## Navigation
### Basic Navigation
- `h`: left
- `j`: down
- `k`: up
- `l`: right
- `<n><MOVE>`: apply the move multiple times. Example: 5j -> move down 5 times

  ### Word Navigation
  word: a sequence of letters/numbers/underscore
  WORD: a sequence of any characters except white space

  - `w`: Move forward to beginning of next word
  - `e`: Move forward to end of next word
  - `b`: Move backward to the beginning of previous word
  - `ge`: Move backward to end of previous word
  - `W`, `E`, `B`, `gE`: same as above but applies to WORD
 
  ### Line Navigation
  - `0`: Go to the beginning of the line
  - `^`: Go to the first non-blank character in the line
  - `g_`: Go to the last non-black character
  - `$`: Go to end of the line
  - `<n>|`: Go nth column in the line
  - `f<char>`: Takes you to the first occurance of `<char>` in the line
  - `t<char>`: Takes you to the character before the first occurance of `<char>` in the line
    - `;`: After using `f` or `t`, it can be used to go to the next occurrence in the line
    - `,`: After using `f` or `t`, it can be used to go to the previous occurrence in the line
    - `F`/`T`: Same as `f`/`t` but search backwards (before the cursor) in the line
 
  ### Sentence/Paragraph Navigation
  Sentence: a sentence is defined as ending at a ., !, or ? followed by either the end of a line, or by a space or a tab.
  Paragraph: any block of text separated by empty lines (before and after)

  - `(`: Go to previous sentence
  - `)`: Go to next sentence
  - `{`: Go to previous paragraph
  - `}`: Go to next paragraph
 
  ### Match Navigation
  You can move between matching brackets, parentheses, etc., using `%`.

  ### Line Number Navigation
  - `gg`: Go to first line
  - `G`: Go to last line
  - `<n>G`: Go to line `n`
  - `<n>%`: Go to n% in the file. Example: `50%` moves to the middle of the file.
 
  ### Scrolling
  - Ctrl-E: Scroll down one line
  - Ctrl-Y: Scroll up one line
  - Ctrl-D: Scroll down half a screen
  - Ctrl-U: Scroll up half a screen
  - Ctrl-F: Scroll down one screen
  - Ctrl-B: Scroll up one screen
 
  ### Search Navigation

  - `/<PHRASE>`: To search forward for `<PHRASE>`
  - `?<PHRASE>`: To search backward for `<PHRASE>`
  - `n`: Repeat the search forward (next match)
  - `N`: Repeat the search backward (previous match)
  - `*`: Go to next occurrence of the word under the cursor (strictly the same word)
  - `#`: Got to previous occurrence of the word under the cursor (strictly the same word)
  - `g*`: Got to the next occurrence of the word under the cursor (could be a substring)
  - `g#`: Got to the previous occurrence of the word under the cursor (could be a substring)

  ### Bookmarks
  - `m<char>`: Assign `char` as a bookmark to the current position
  - `` `<char> ``: Go to line and column of bookmark `<char>`
  - `'<char>`: Go to line of bookmark `<char>`

## Find and Replace
  To find and replace, vim uses a similar syntax to `sed`
  - `:s/old/new/` - Replace first occurrence of "old" with "new"
  - `:s/old/new/g` - Replace all occurrences of "old" with "new" in the current line For the entire file:
  - `:%s/old/new/g` - Replace all occurrences of "old" with "new" in the whole file
  - `:%s/old/new/gc` - Replace all occurrences with confirmation (it will ask you for each replacement)
 
  Some useful flags you can add:

  - `i` for case insensitive search (e.g., `:%s/old/new/gi`)
  - `c` for confirmation
  - `g` for global (all occurrences in the line)

  Some common special characters that can be used with this command:
  - `\r` - newline
  - `\t` - tab
  - `\s` - whitespace (space or tab)
  - `\S` - non-whitespace character
  - `\d` - digit (0-9)
  - `\D` - non-digit
  - `\w` - word character (letter, digit, underscore)
  - `\W` - non-word character
  - `\a` - alphabetic character

## Configuring vim
The `:set` command in Vim is used to configure various options. Here are some commonly used settings:

Line Numbers and Display:
- `:set number` (or `nu`) - Show line numbers
- `:set relativenumber` (or `rnu`) - Show relative line numbers
- `:set wrap` / `:set nowrap` - Enable/disable line wrapping
- `:set cursorline` - Highlight current line
- `:set list` - Show hidden characters (tabs, trailing spaces)

Indentation and Formatting:
- `:set autoindent` - Copy indent from current line when starting new line
- `:set expandtab` - Convert tabs to spaces
- `:set tabstop=4` - Set tab width to 4 spaces
- `:set shiftwidth=4` - Set indentation width
- `:set smartindent` - Smart autoindenting when starting a new line

Search Settings:
- `:set ignorecase` - Case insensitive search
- `:set smartcase` - Override ignorecase if search pattern has uppercase
- `:set incsearch` - Show partial matches while typing search
- `:set hlsearch` - Highlight all search matches

Useful Combinations:
- `:set number relativenumber` - Show both absolute and relative numbers
- `:set expandtab tabstop=2 shiftwidth=2` - Common setup for 2-space indentation

To make settings permanent:
1. Edit your `~/.vimrc` file
2. Add the settings without the colon (e.g., `set number`)

You can also:
- Use `:set all` to see all settings
- Add `no` prefix to disable (e.g., `:set noignorecase`)
- Add `?` to check current value (e.g., `:set tabstop?`)

## Edit Modes
- `i`: Insert mode
- `o`: Add new line below and insert
- `O`: Add new line above and insert
- `C`: Delete until end of line and insert
- `a` Append (start insert after the current position)
- `A`: Append to end of line (start inserting at the end of line)
- `S`: Delete current line and insert
