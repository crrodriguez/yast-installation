#
# Makefile.am 
#
#
SUBDIRS = examples

htmldir = $(docdir)/control-doc
xml_files =  $(wildcard *.xml) 

html_DATA = $(wildcard html/*.html) \
	    html/yast2docs.css

all-local: html/index.html

pdf: control-doc.pdf

html/index.html: $(xml_files)
	XML_CATALOG_FILES=@XML_CATALOG@ \
	@XSLTPROC@ @XSLTPROC_FLAGS@ --xinclude \
	@STYLESHEET_HTML@ $<

control-doc.fo: control-doc.xml
	XML_CATALOG_FILES=@XML_CATALOG@ \
	@XSLTPROC@ @XSLTPROC_FLAGS@ --xinclude \
	-o $@ @STYLESHEET_PDF@  $<

control-doc.pdf: control-doc.fo
	fop -q $< $@


html/yast2docs.css: html/index.html
	cp @STYLESHEET_CSS@ html
	cp -a `pkg-config --variable=yast2dir yast2-devtools`/data/docbook/images html


EXTRA_DIST = $(xml_files)

CLEANFILES =  $(html_DATA)

clean-local:
	rm -rf html

install-data-local:
	mkdir -p $(DESTDIR)$(htmldir)
	cp -a $(srcdir)/html/images $(DESTDIR)$(htmldir)
