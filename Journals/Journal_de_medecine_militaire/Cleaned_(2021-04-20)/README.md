# Data Map 
In this first stage of cleaning- I decided to isolate the individual pages of the journal and the titles of each journal article for easier navigation. The page numbers are now separated from the body of text by blank lines. The title of each article are now separated from the text of the previous article by several blanks lines and a marker which is simply the word “Title” floating two lines above the title itself. Note that the title of each article is not separated from its own text. Below is the process I used for this stage of cleaning.  
# Isolating Pages 
In the base text files, most pages are delimited by a single line that reads either # Journal on the even pages, or de de Medecine militaire # on the odd pages. To isolate these lines, I used the following regular expressions. 

Even pages: `\d+\d?\sJournal`. This looks for a number with any amount of digits followed by a white space followed by the word Journal. Added `\r\n\r\n$&\r\n\r\n` to put a new line in between each page. 

Odd pages: `de Médecine militaire(,|.)\s\d+\d`. This regular expression looked for the string of words de Médecine militaire, followed by a common or a period then a white space followed by a number with any amount of digits. 

After highlighting these lines, I replaced them using the following regular expression `\r\n\r\n$&\r\n\r\n`, which put a new line in between each page. Unfortunately, this method only worked in Volumes 2-7. Because volume one had a different header than the following volumes. Because of this, I only isolated the titles in volume one and note the pages.    
# Isolating Titles
Usually, the titles are spelled out with all capital letters. To Find these instances, I used the following regular expression: `(?=^[A-WYZÈ]{4,})`. This looked for the start of a line that contained a series of at least 4 capital letters. This brought me to the first lines of most titles to articles. I then inserted `\r\n\r\nTitle\r\n\r\n$&` to put lines above the title itself then inserted the word “title”. I could not use the find and replace all function, because this expression would sometime catch random capitalized words. So I have to select manually the instances where I wanted to use the replace function.  

