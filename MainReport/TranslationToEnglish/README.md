The numbered files above so each step of the translation process.

There are many steps, because human-translation is expensive, so I tried to use machine-translation (with manual grammatical refinement) where possible, to then be merged with the parts that required human translation.

This sentence-marking -> splitting -> sentence-matching -> merging process is a bit complex, hence all the steps.

# Helpers

### Steps to produce the "marked text only" files
```
1) Remove paragraphs without marked sections, using regex (in vscode): /\n\n([^`]+)\n\n/ -> "\n\n"
2) Remove non-marked text (before marked-text) in remaining paragraphs, using regex: /\n[^`#\n]+`([^#\n]+?)`/ -> "\n###`$1`"
3) Remove non-marked text (after marked-text) in remaining paragraphs, using regex: /(###|\n)`([^#\n]+?)`[^`#\n]+(`|\n)/ -> "$1`$2`###$3"
4) Manually replace the few remaining non-marked sections with "###". (there should only be a few)
5) Replace "###" with "...": "###" -> "..."
6) Remove backtick markers: "`" -> ""
7) Fix cases of quadruple ellipses: "...." -> "..."
8) Add spaces after non-start-of-line ellipses: /([^\s\[])\.\.\.([^\s\]])/ -> "$1... $2"
```