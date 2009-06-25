# makefile to convert figures into eps format for the book

# Comments from Michel Wurtz:
# You will notice that the list given is the list of targets.  "all" just
# refer to this list.  The most important rule is the next rule, that give
# the generic rule for transforming a .fig into a .eps file.  Note the use
# of % (define the couple target:source) and the use of
# $< (source postfix, here .fig) and $@ (target postfix, here .eps)

# with .eps extension:
# JPG=qgis_icon_new_verylarge.eps\

PNG=ecape01.eps\
    polygonfeature.eps\
    polylinefeature.eps\
    topic1_adding_layers1.eps\
    topic1_adding_layers2.eps\
    topic1_adding_layers3.eps\
    topic1_adding_layers4.eps\
    topic1_after_legend_drag.eps\
    topic1_before_legend_drag.eps\
    topic1_changing_symbology.eps\
    topic1_menus.eps\
    topic1_raster_data_zoomed_in.eps\
    topic1_raster_data_zoomed_out.eps\
    topic1_toolbars.eps\
    topic1_vector_data.eps\
	 
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
