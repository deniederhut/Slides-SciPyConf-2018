ALL=index.html

.PHONY: all clean server web upload

all: $(ALL)

reveal.js:
	git clone https://github.com/hakimel/reveal.js

index.html: slides.md
	pandoc $< --output=$@ --mathjax --standalone --write=revealjs --css=slides.css --highlight-style=espresso

online:
	pandoc $< --output=$@ --mathjax --standalone --write=revealjs --css=slides.css --highlight-style=espresso --variable revealjs-url=http://lab.hakim.se/reveal-js

serve:
	python3 -m http.server 8080

clean:
	-rm $(ALL)
