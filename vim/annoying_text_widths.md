## Annoying Text Widths

Obviously in Vim the lines can go as long as possible, but for something like a
markdown file, I'm tired of constanly reformatting.  Added this snippet to my
.vimrc for local text widths for certain types of files.

```
au BufRead,BufNewFile *.md setlocal textwidth=80
```

Also, when you highlight a bunch of text `gq` will reformat it correctly.
