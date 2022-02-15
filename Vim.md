# Basics -
#### Exiting Vim - 
- To exit vim ***without making any changes*** :  `ESC+q`
- To exit vim ***forcefully without any changes*** : `ESC+q!`
- To ***save changes to a file*** -:`ESC+w`
- To ***save changes to a file and quit***: `ESC+wq`
#### Insert Mode - 
- Press `i` to go into ***insert*** mode.
- Press `a` to go into ***append*** mode.
- Press `I` to ***go to the beginning of the line*** in insert mode.
- Press `A` to ***go to the end of the line*** in insert mode.

#### Navigation -
While in `Normal` Mode,
 - Press `gg` to ***go to the starting of the file***.
 - Press `G` to ***go to the end of the file.***
 - Press `:15` to ***go to line 15***.
 - Press `$` to ***go to end of the line***.
 - Press `0` to ***go to the beginning of the line***.
- Press `w` to ***jump to the next word.***
	
	- Press `5w` to ***jump 5 words forward***(5 can be any number.) 

- Press `b` to ***jump to the previous word.*** 
	
	- Press `5b` to ***jump 5 words. backward***(5 can be any number.)
- Press `5j` to ***go down by 5 lines.***
- Press `5k` to ***go up by 5 lines.***
 
 #### Copy & Paste - 
 > ***Note -*** You can enter ***Visual Mode*** by pressing ***v*** and use ***arrow keys*** to select.

1. ##### In Visual Mode - 
- Press `d` to ***delete***.
- Press `c` to ***change***.
- Press `y` to ***yank i.e copy***.

2. ##### In Normal Mode -
- Press `yy` to ***yank(copy) the whole line***.
   - Press `5yy` to ***yank(copy) next 5 lines***.
- Press `y5w` to ***yank(copy) 5 words.***
- Press `yiw` to ***yank(copy) inner word.***
- Press `yi)` to ***yank(copy) everything inside bracket.***
- Press `p` to ***paste after.***
	- Press `9p` to ***paste 9 times.***
- Press `P` to ***paste before.***

 #### Deleting and Replacing -
 1. ##### Deleting - 
 	
	- Press `dw` to ***delete a word.***
	- Press `D` to ***delete rest of the line.***
 	- Press `d4w` to ***delete 4 words.***
 	- Press `C` to ***delete rest of the line and enter insert mode.***
 	- Press `dd` to ***delete the whole line.***
 	- Press `4dd`to ***delete 4 lines***
 
2. ##### Replacing - 
 - Press `r` to  ***replace a letter.***
 - Press `R` to ***use REPLACE MODE.***
 - Press `cw` to ***edit/replace a word either from starting of the word or from the middle***.
 - Press `cc` to ***replace the whole line.***
 - Press `7cc` to ***replace the next 7 lines(basically deletes the next 7 lines and puts you into insert mode.)***	
 
 #### Undo & Redo - 
 - Press `u` to ***undo a change.***
 	
	- Press `5u` to ***undo last 5 changes.*** 
 
 - Press `CTRL+R` to ***redo a change.***
 	
	- Press `7 CTRL+R` to ***redo last 7 things.***

#### Commands - 
While in `Normal` Mode,
- Press `:/word` to ***search for a word(replace 'word' with the word you want to search for).***
	- Press `n` to ***search for the `next` occurence of the word.***
	- Press `N` to ***search for the `previous` occurence of the word.***
- Press `:%s/old/new/g` to ***replace something globally in the whole file.***
	- Press `:s/old/new/g` to ***replace something globally but only in that line.***
- Press `:set number` to ***show line numbers.***
- Press `:set relativenumber` to ***show relative numbers.***
- Press `:colorscheme <colorscheme>` to set a colourscheme
#### Visual Mode - 
- Press `SHIFT+v` to ***select lines.***
- Press `CTRL+v` to ***select blocks.***
 

 ---
# Advanced Editing -

- Press `ciw` to ***change inner word.***
	> Eg: `This is a test.`
	> Suppose your cursor is at `e` in `test` and u want to edit the whole word, `ciw` will let u ***edit*** the whole word.
- Press `diw` to ***delete inner word.*** 
	> Eg: `This is a test.`
	> Suppose your cursor is at `e` in `test` and u want to edit the whole word, `diw` will let u ***delete*** the whole word.

	> ***Note:*** You can use `ciw` and `diw` with other stuff like - 
	**ci) - Change Inner Parentheses
	cil - Change Inner Parentheses
	ci[ Change Inner Brackets
	ci]
	Change Inner Brackets
	ci} Change Inner Brackets
	ci{ Change Inner Brackets**

- Press `%` to ***Jump to start of bracket to end of bracket***.
- Press `c%` to ***Change from bracket start until Bracket end.***.
- Press `d%` to ***Delete from bracket start until Bracket end***.
- Press `.` to *** do last operation***.
- Press `zz` to ***center ur line(center ur screen).***
- Press `gg=G` to ***indent the whole file.***
- Press`ggdG` to ***delete the whole file.***