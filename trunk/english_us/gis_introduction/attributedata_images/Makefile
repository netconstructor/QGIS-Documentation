# makefile to convert figures into eps format for the book

# Comments from Michel Wurtz:
# You will notice that the list given is the list of targets.  "all" just
# refer to this list.  The most important rule is the next rule, that give
# the generic rule for transforming a .fig into a .eps file.  Note the use
# of % (define the couple target:source) and the use of
# $< (source postfix, here .fig) and $@ (target postfix, here .eps)

# with .eps extension:
# JPG=qgis_icon_new_verylarge.eps\

PNG=attribute_diagram.eps\
    AttributeTable.eps\
    continuous_colour_contours.eps\
    continuous_colour_dialog.eps\
    graduated_colour_dialog.eps\
    graduated_contours.eps\
    HousesByBalcony.eps\
    HousesByRoofColour.eps\
    HousesByBalconyRoof.eps\
    Houses.eps\
    HousesSearch.eps\
    RenderAsColour.eps\
    RenderAsComparison.eps\
    RenderAsGrey.eps\
    single_symbol_dialog_lines.eps\
    single_symbol_dialog_point.eps\
    unique_value_dialog.eps\
    unique_value_roads.eps\
    blueline.eps\
    blackline.eps\
    apricotline.eps\
    apricotdots.eps\
    colorange1.eps\
    colorange2.eps\
    colorange3.eps\
    colorange4.eps\
    colorange5.eps\
    colbrown1.eps\
    colbrown2.eps\
    colbrown3.eps\
    colbrown4.eps\

#JPG=

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
