#convenient Makefile
#
#targets:
#  make            - builds the text and images
#  make text	   - builds the text only
#  make refcheck   - check \label{} and \ref{} and friends for consistency
#                    Result is in "latex_refs.log"
#  make clean      - removed Latex' auxiliary files and finalpix
#  make cleanpics  - remove created pics from subdirs
#  make pics	   - create pics
#  make ps         - create PS file
#  make pdf        - create PDF file
#  make html       - create HTML file
#  make updateicon - update png icons from QGIS source
#  make changelog  - creates ChangeLog

# Name of latex main file to compile
FILE=gis_introduction

all: 
	make pics
	latex $(FILE)
	#bibtex $(FILE)
	bibtex $(FILE)1
	bibtex $(FILE)2
	#now loop over Latex files, until stable:
	echo Rerun > $(FILE).log
	while grep Rerun $(FILE).log >/dev/null 2>&1 ; do latex $(FILE).tex ; done
	makeindex $(FILE)

text:
	latex $(FILE)
	bibtex $(FILE)
	#now loop over Latex files, until stable:
	echo Rerun > $(FILE).log
	while grep Rerun $(FILE).log >/dev/null 2>&1 ; do latex $(FILE).tex ; done

#check references:
refcheck:
	@rm -f all
	make | grep "Reference\|Rerun" | sed 's/LaTeX\ Warning:\ Reference\ //' | tr '`' "'" > latex_refs.log
	@rm -f all
	make | grep Citation >> latex_refs.log ; true
	@rm -f all
	make | grep Label | grep multiply >> latex_refs.log ; true
	@echo "Check latex_refs.log:"
	@echo "-------------" ; cat latex_refs.log | sort -u | grep -v Rerun


# check FIXMEs in document
fixme:
	grep -C 2 -n "FIXME" *.tex

#make PostScript:
ps:
	make all
	dvips $(FILE).dvi -o $(FILE).ps

#make PDF:
pdf:
	make all
	dvipdf  $(FILE).dvi

# make pics
pics:
	(cd ./images && make)
	(cd ./gisintro_images && make)
	(cd ./vectordata_images && make)	
	(cd ./attributedata_images && make)
	(cd ./datacapture_images && make)
	(cd ./rasterdata_images && make)
	(cd ./topology_images && make)
	(cd ./crs_images && make)
	(cd ./mapproduction_images && make)
	(cd ./vectoranalysis_images && make)
	(cd ./rasteranalysis_images && make)

# make html
# requires: latex2html oder tex4ht
# http://www.cse.ohio-state.edu/~gurari/TeX4ht/mn.html
html:
	make all
	if [ ! -d $(FILE) ]; then mkdir $(FILE); fi
	latex2html -init_file l2h.conf  -split=+2 -dir $(FILE) -address "\
	&copy; 2009 Chief Directorate: Spatial Planning \& Information,
        Department of Land Affairs, Eastern Cape. \
	<br>Last modified: `/bin/date +%d-%m-%Y`" $(FILE)

clean:
	rm -f *.log *.aux $(FILE).dvi *.bbl *.tip *.lox *.blg *.ind \
	*.ilg *.toc *.tof *.lof *.lot *.pdf *.ps *.idx *.brf *.out *~
	rm -rf $(FILE)
	rm -rf ./finalpix
	(cd ./appendices && rm -f *.aux)
	make cleanpics

cleanpics:
	(cd ./images && make clean)
	(cd ./gisintro_images && make clean)
	(cd ./vectordata_images && make clean)
	(cd ./attributedata_images && make clean)
	(cd ./datacapture_images && make clean)
	(cd ./rasterdata_images && make clean)
	(cd ./topology_images && make clean)
	(cd ./crs_images && make clean)
	(cd ./mapproduction_images && make clean)
	(cd ./vectoranalysis_images && make clean)
	(cd ./rasteranalysis_images && make clean)


