The numbered files above show the various steps of the translation process.

Part of the reason there are so many steps, is that human-translation is expensive, so I used machine-translation as the base for areas where the meaning was sufficiently clear (with grammar and phrasing refinements then added), which were then merged with the parts that required human translation.

This sentence-marking -> splitting -> sentence-matching -> merging process (along with refinements during the process) ended up requiring several steps; the incremental outputs of these steps are stored within the numbered files. (you can use a tool like [TortoiseGitMerge](https://github.com/Venryx/TortoiseGitMerge_Standalone) to easily compare the contents of any two files)

# Viewing

To view a PDF or HTML file in its "rendered" form, add its filename to the end of this url: `https://venryx.github.io/lalm-2010-analysis/MainReport/TranslationToEnglish/`

Using the above scheme, here are the links for viewing the original PDF, and the final translated PDF/HTML files:
* https://venryx.github.io/lalm-2010-analysis/MainReport/TranslationToEnglish/1.0%29%20Orig%20document.pdf
* https://venryx.github.io/lalm-2010-analysis/MainReport/TranslationToEnglish/Final.pdf
* https://venryx.github.io/lalm-2010-analysis/MainReport/TranslationToEnglish/Final.html

# Helpers

### Steps to extract "backtick-marked text" from a file (eg. deriving 7.1 from 7.0)
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

### Steps to produce the final pdf and html files

1) Open the "Final.<area>md" file in Visual Studio Code.
2) Install the "Markdown PDF" extension. (v1.4.4 at time of initial PDF generation)
3) Export to the Final.pdf file, by running the (just added) VSCode command: "Markdown PDF: Export (pdf)"  
4) Export to the Final.html file, by running the VSCode command: "Markdown PDF: Export (html)"

Optionally: (for setting the PDF document's title)  

5) Download/install exiftool: https://exiftool.org
6) For Windows: Open/extract the zip file, and move the "exiftool(-k).exe" file to a suitable location, renaming it to just `exiftool.exe`.
7) Run the following in a terminal: `"exiftool" -title="Lalm kindergarten: Overview and assessment of unusual events from 26 April to 15 June 2010" "Final.pdf" -overwrite_original` (if either `exiftool` or the pdf file cannot be located by the terminal, use their full paths in the command string)