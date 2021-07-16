###############################################################################
## Makefile for apertium-gle
###############################################################################

LANG1=gle
BASENAME=apertium-$(LANG1)

TARGETS_COMMON =			\
	$(LANG1).automorf.bin		\
	$(LANG1).automorf.att.gz	\
	$(LANG1).autogen.bin		\
	$(LANG1).autogen.att.gz		\
	$(LANG1).rlx.bin

# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Irish transducer
###############################################################################

$(LANG1).autogen.bin: $(BASENAME).$(LANG1).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(LANG1).automorf.bin: $(BASENAME).$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(LANG1).autogen.att.gz: $(LANG1).autogen.bin
	lt-print $< | gzip -9 -c -n > $@

$(LANG1).automorf.att.gz: $(LANG1).automorf.bin
	lt-print $< | gzip -9 -c -n > $@

###############################################################################
## Disambiguation rules
###############################################################################

$(LANG1).rlx.bin: $(BASENAME).$(LANG1).rlx
	cg-comp $< $@

###############################################################################
## Distribution
###############################################################################
EXTRA_DIST=$(BASENAME).$(LANG1).dix		\
		$(BASENAME).$(LANG1).rlx	\
		modes.xml

###############################################################################
## Installation stuff
###############################################################################
#
#   apertium_gle_dir: This is where the compiled binaries go
#   apertium_gle_srcdir: This is where the source files go

apertium_gledir=$(prefix)/share/apertium/$(BASENAME)/
apertium_gle_srcdir=$(prefix)/share/apertium/$(BASENAME)/

apertium_gle_DATA=$(TARGETS_COMMON)

pkgconfigdir = $(prefix)/share/pkgconfig
pkgconfig_DATA = $(BASENAME).pc

noinst_DATA=modes/$(LANG1)-morph.mode

install-data-local: install-modes
	$(INSTALL_DATA) $(BASENAME).$(LANG1).dix $(DESTDIR)$(apertium_gle_srcdir)
	$(INSTALL_DATA) $(BASENAME).$(LANG1).rlx $(DESTDIR)$(apertium_gle_srcdir)

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	apertium-regtest test
