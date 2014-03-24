MANUSCRIPT=abstract

help:
	@echo "Rules:"
	@echo "  pdf     compile the manuscript plus a copy without references"
	@echo "  wc      count the words in the document (approximate)"
	@echo "  clean   remove generated files"

wc:
	@detex $(MANUSCRIPT).tex | wc -w

pdf: $(MANUSCRIPT).pdf

$(MANUSCRIPT).pdf: $(MANUSCRIPT).tex
	pdflatex $<
	bibtex $(MANUSCRIPT)
	pdflatex $<
	pdflatex $<
	pdflatex $(MANUSCRIPT)-norefs.tex

clean:
	rm -rf *.aux *.log *.bbl *.blg *.fff *.lof $(MANUSCRIPT).pdf \
		$(MANUSCRIPT)-norefs.pdf
