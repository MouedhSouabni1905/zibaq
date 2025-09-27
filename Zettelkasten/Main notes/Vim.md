**Tags:** [[Programming]] [[Sysadmin]]

- Prefixing movement commands with *g* makes it so that you move through the visual line not the actual line (because in vim the line doesn't go to a new line until you press enter).
- *gq* formats a block of text to return to the next line automatically
- *gu* lowercases text objects and *gU* uppercases them
- *gf* opens the file corresponding to the path your cursor is on (doesn't have to be selected)
- *J* joins lines, contrary to *gq*
- *cib* jumps to the first and outer-most bracket on the line you're on, deletes anything inside the brackets and enters insert mode
- *ciB* does the same for the curly braces (in this case it would be the code block not the line)
- Replacing *c* with *v* in both of these selects instead of deleting
- Fun fact: vim uses linked lists to represent characters in memory. Not very memory efficient, the technique used in other code editors is a [[Data structures|gap buffer]].
  