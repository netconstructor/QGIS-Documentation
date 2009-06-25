# makefile to convert figures into eps format for the book

# Comments from Michel Wurtz:
# You will notice that the list given is the list of targets.  "all" just
# refer to this list.  The most important rule is the next rule, that give
# the generic rule for transforming a .fig into a .eps file.  Note the use
# of % (define the couple target:source) and the use of
# $< (source postfix, here .fig) and $@ (target postfix, here .eps)

# with .eps extension:
# JPG=qgis_icon_new_verylarge.eps\

PNG=AngularLines1.eps\
    AngularLines2.eps\
    AngularLines.eps\
    linegeometry.eps\
    pointgeometry.eps\
    polygongeometry.eps\
    Scale-1mil.eps\
    Scale-250k.eps\
    Scale-50k.eps\
    Scale-all.eps\
    Slivers1.eps\
    Slivers2.eps\
    Slivers.eps\
    Symbology-default.eps\
    Symbology-settings.eps\
    Symbology-updated.eps\
    Toposheet.eps\
    UndershootsOvershoots.eps\
    vector_diagram.eps\

JPG=LandscapeFeaturesHighlighted.eps\
    Landscape.eps\
 
##### TARGETS #####

all: $(PNG) $(JPG)
	if [ ! -d ../finalpix/ ]; then mkdir ../finalpix; fi
	#do not use move (mv):
	cp *.eps ../finalpix/

#$(EPS):	%.eps: %.fig
#	fig2dev -L eps $< > $@

#$(FIGPNG): %.png: %.fig
#	fig2dev -L png -m 2 $< > $@

$(PNG): %.eps: %.png
	# Workaround for PDF
	#convert -geometry 300x -depth 1 $< $@
	convert $< $@ 

$(JPG): %.eps: %.jpg
	# Workaround for PDF
	#convert -geometry 300x -depth 1 $< $@
	convert $< $@

clean:
	rm -f *.bak *~ *.pdf $(PNG) $(JPG)
