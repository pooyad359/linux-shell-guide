# Vim

## Operators
- `y`: Yank (copy)
- `d`: Delete and save to register
- `c`: Delete and save to register and start insert mode
- `p`: Paste yanked text after cursor
- `P`: Paste yanked text before cursor
- `dd`, `cc`, `yy`: delete/copy the entire current line


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
 
