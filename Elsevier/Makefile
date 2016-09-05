FILE_NAME := paper

TEMP_FILES := \
	$(FILE_NAME).aux \
	$(FILE_NAME).spl \
	$(FILE_NAME).bbl \
	$(FILE_NAME).log \
	$(FILE_NAME).blg \
	$(FILE_NAME).brf \
	$(FILE_NAME).out

SECTION_FILES = \
	paper.tex 
	# sections/introduction.tex \
	# sections/background.tex \
	# sections/studydesign.tex \
	# sections/results.tex \
	# sections/threats.tex \
	# sections/RQ1.tex \
	# sections/RQ2.tex 

BIBTEX_FILES = \
	mybibfile.bib

GEN_FIGURES = \
	$(NULL)

# STATIC_FIGURES = \
# 	figure/overview.pdf 

DEBUG=no
ifneq '$(DEBUG)' 'yes'
LATEX_FLAGS="-interaction=batchmode"
endif

.DELETE_ON_ERROR:

################################################################################
# Main paper building
################################################################################
# $(STATIC_FIGURES)
$(FILE_NAME).pdf: $(SECTION_FILES) $(GEN_FIGURES) $(BIBTEX_FILES) 
	pdflatex $(LATEX_FLAGS) $(FILE_NAME)
	bibtex $(FILE_NAME)
	pdflatex $(LATEX_FLAGS) $(FILE_NAME)
	pdflatex $(LATEX_FLAGS) $(FILE_NAME)
	rm -f $(TEMP_FILES)
	open $(FILE_NAME).pdf
	# rm $(FILE_NAME).pdf


################################################################################
# Camera-Ready
################################################################################
.PHONY: camera
camera: 
	pdftops $(FILE_NAME).pdf
	ps2pdf14 -dPDFSETTINGS=/prepress $(FILE_NAME).pdf $(FILE_NAME)-new.pdf
	# pdffont $(FILE_NAME).pdf
	mv $(FILE_NAME)-new.pdf $(FILE_NAME).pdf
	open $(FILE_NAME).pdf
	# rm $(FILE_NAME).pdf
	
################################################################################
# Figures
################################################################################

#$(GEN_FIGURES): %.pdf: scripts/rms/analysis_figures.r scripts/rms/util.r
#	Rscript $<

################################################################################
# Clean
################################################################################
.PHONY: clean
clean:
	rm -f $(TEMP_FILES) $(GEN_FIGURES) $(FILE_NAME).pdf
