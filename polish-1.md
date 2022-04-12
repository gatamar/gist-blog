So I bought a book of Witold Shablovsky.
That book was in Polish. I don't speak Polish, I understand about 80%, and what's the most painful, I don't read it (YET).
I know that after reading a lot my English became very good with a one small flaw: wild accent.
So when choosing btw knowing all the words, feeling the context, quickly getting all the information... and the wild accent a one can develop when only reading, so the brain unconsciously repeats its version of the word, I choose both. :D

So I bought that book and got stuck at the very first page with some dedication or so. That word was `chochlą`. Now, before we proceed with the story, I want to say that I'm having online Polish lessons with some teacher from Ukraine, and we are doing Krok Po Kroku, and my brain is sometimes screaming of these grammar rules and a wild similarity of some words which sound the same e.g. `iść`/`jeść`/`jest`.
But what I found while reading a few pages of this Shablovsky book is that I love written Polish because of two reasons:
1. It has latin alphabet, so it's learnable :D
2. All these `ś`, `ć`, and `ą` are just perfect, because we can make the sound soft, or change the grammar form of the word, without increasing the number of letters, and without changing the suffixes dramatically like in Ukrainian/russian. Returning to "chochla"->"chochlą", it far easier to guess the initial form, than in the Ukrainian version "черпак"->"черпаком" (well, it's a bad example, I meant smth like "черпачна"->"черпачною", but this word doesn't exist :D).
So the written Polish is very ergonomic and UX-y (but I say nothing about the spoken Polish).

So, let's return to the book. As you may know, I've been writing a small iOS app for already 2.5 years, and it's still not finished, but the great result of doing it is that I can navigate in the Readium code. So when I got this ePub at https://www.taniaksiazka.pl/, waited for more that 10 min until an electronic version was _generated_, downloaded that ePub on my iPhone, I was asked to choose the app in which to read - of course I chosed a dev version of the Readium app (for which I'm doing some PR currently). 

Then when this "chochlą" word happened, the only this I knew is that it's realated to the cooking accessories and that the main form of the word is `chochla`. I selected the word, tapped "Translate" in the context menu and WAIT... WAIT... WAIT... iOS said that Polish sucks just as well as Ukrainian. :(

polish-1-1.jpeg

So I googled how to add that Polish to the dictionary, and didn't found how to do that, and there was an app called "Dictionary Appender", but then Apple wiped it out from the AppStore.

I decided to modify the Readium source code to add some custom Polish dictionary. Going forward (as the coffee ended and I'm tired of writing this), it took me 2.5 hours = 1 hour for modifying the code + 1.5 hour of searching for ANY Polish Glossary.

Most of the dictionaries I found on Github/ in some blog posts - were `*spell` dictionaries. Which means they didn't contain neither translation nor explanation, just the correct spelling form. Btw, I used this `*spell` stuff in my bachelor diploma, which while being miserable was a fun (and the only stuff which was left after it is this SO Q: https://stackoverflow.com/questions/24098658/morphological-text-analysis-with-python-using-dic-aff).

The only dictionary I found in 1.5 hours was this one: https://github.com/djstrong/PL-Wiktionary-To-Dictionary/blob/master/dictionaries/polish_english.txt.      

I embedded it into the iOS app, loading it into the memory when the book is opened, and making the requests when the book is opened.
It has 2 significant flaws:
1. there're only 16K words, I don't know if it's enough, but suppose not
2. it. doesnt. care. about. grammar. forms. So if I want to get the translation for "chochlą", it's not that smart, I don't want to spend a half of life to link some suffix dictionaries, somehow apply some formula to get the initial word form. Even if there're were handy libs for this, I guess Polish would suck because even Apple doesn't support it (btw, I hate that Siri didn't speak Ukrainian the last time I checked it, but the male voice with Australian accent was cool :D). 

So for any unknown word I substract the last 2 or 3 letters, and search for them in my "dictionary" (this is how O(logN) become 0(N) again :D). I've heard some "suffix tree" can be build, some "fuzzy seach" can be performed, but again, 1 hour of coding is better than 40 hours of research + coding. 
The current version of the app looks like this:

polish-1-2.jpeg

It's far from perfect, it doesn't know about 60% of the words I ask it, some part of that words would be known if some suffix correction was made, I want to improve this but I don't want to improve this.

So my two main goals of this braindump were achieved:
1. I wrote this stuff, so I won't think of it again and again this week
2. I added the screenshots, so I can show how easy it's to modify Readium to meet your needs

Btw, if someone will read it, and you know some simple way to add Polish-English or Polish-Ukrainian or Polish-russian dictionary to iOS, please ping me e.g. my opening an issue in this repo. 
