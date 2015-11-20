###Model Change

+---------+ i,I,a,A,o,O,r,R,s,S +----------+
| Normal +---------->------------+ Insert |
| mode |                           | mode |
| +----------<------------+ |
+-+---+---+ <Esc> +----------+
                    | |
                    | |
                    | |
                    | |
                    | |
                    v,V V ^ <Esc>
                    | |
                    | |
                    | |
                    | |
            +---+---+----+
            | Visual     |
            | mode       |
            +------------+




googleAppId  :  goagent-test-1097



Command Action
i insert text just before the cursor
I insert text at the start of the line
a append text just after the cursor
A append text at the end of the line
o open a new line below
O open a new line above
s substitute(替换) the current character
S substitute the current line
r replace the current character
R replace continuous characters（替换接下来的）



##Vim en:Typing Skills
#####

the fingers of your left hand are on the ``ASDF`` keys and the fingers of your right hand are on  the `JKL;`



##Vim en:Moving Around
#####

`w `   move to next word  
`}`    move to to the next paragraph  
`3fd`  move to 3rd  occurrence of the letter 'h'  
`35j`  move 35 lines downwards?   `k`   
`35L`  move to 35 lines  downwards(必须为大写)  `H`  
`3l`   move to 3 letters forwords in the line   `h`   
`ctrl-o`   jump back to the previous location 
`ctrl-i`  jump forward to the next location again.  
`ctrl-f`   move one screen `f`orward  
`50G`   move to 50th lines  
`1G`  or  `H`  move to first line  
`G`  or `L`  move to end line
`M`   move to the middle of the text

###Words, sentences, paragraphs

`^`  first
`w`  word   (前面可以带数字，直接跳过几个单词)
`e`  end of a word  
`b`   go back by a word  
See `:help word-motions` for more details. 

`(`  句子  
`)`  
`{`  段落  
`}`   
See `:help cursor-motions` for more details.  

Make your mark(自定义标签) 

`m`  means  mark  
with  `ma`  means  create  a mark named 'a';  tag can be named from "a-zA-Z"



###Parts of the text
`~`  change the  capitalization of letters


See :help object-motions and :help text-objects for more details.

`ap`  and  `aw`  是在视图模式下的命令，表示一个段落，一个word
`ab`   mens all thing between   parentheses

vim 中通过  `ctrl+]` 进行跳转位置


To make saving easier, add the following line to your vimrc file:
To save, ctrl-s.
nmap <c-s> :w<CR>
imap <c-s> <Esc>:w<CR>a


cop  paste  and  delete

|desktop world|            vim world  |           operation| 
|:---:|--:|--:| 
|cut                        |  delete               |    d  |
|copy                       |  yank                |     y  |
|paste                       | paste              |      p  |


`dw`     delete a word   quickly.  


`p` (lower case) paste after current cursor position  
`P` (upper case) paste before current cursor position  




####undo  redo 命令

`u`   and   `ctrl +r`
:earlier 4m

:later 45s

:undo 5

:undo 5

`/word`   查询命令



vim的正则表达式搜索如何进行！！！！！



vim大法

1. 将环境换成Linux
2. 熟悉试用vim基本命令
3. 接下来才是进行vim配置

***********************************************************
分割线
***********************************************************


###Basic Editing

1.  move  : `h j k l`
2.  delete : `x`

> 智能补全快捷键 ctrl + N  ctrl + P

3. other commands：
	- dd:delete the line.
	- o(open): open a new line 
	- a(append): insert after the cursor.

Interactive  Tutorial:  `:help tutor`  in unix: `$vimtutor`


###Editing a little faster
1. 区域move   ：
    - word：`w`
    - back with a word:`b`
    - end :`$` ex: `4$`
    - start : `^`  `0`  has the same function.
    - find: `f`  ex:`fx` find the first "x" in the line.
    - Find: `F`  ex:`Fx` find "x" in the line to the left 
    - G:  `1G`:top `10G`:the 10th line of the file `G`:end of the file
    - %: `10%`: locate the 10% of the file.
    - 翻页：`ctrl+U` `Ctrl+D`  backward(upward)/toward(downward)
2.delete text:
  first:  v Change to Visual mode ,then `b` or `w` choose a word. then `d` delete the word.
  delete text without Visual Model.
       1. d
       2. motion commands
  ex:`dw`  `d3l`  `d3h`      
  > 注意：it can only delete in a line.


`3dw` and `d3w`:
    `3dw`：delete one word 3times.
    `d3w`: delete 3 words once.

###Changing text
replace &&  change:
  1. `r`：repalce a character.
  2. `c`: replace a word or a block of a line.(most like `dmotion` command)
  just as delete text and change to insert mode.
  `C`(Capital大写的)  and `c$` the same mean.


