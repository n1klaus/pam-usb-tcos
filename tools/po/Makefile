LANGUAGES=es pt_BR
PACKAGE=pamusb-conf-gui

all: gmo


clean:
	@echo " **CLEAN**"
	@rm -rf *.mo *~ tmp/
	@for lang in $(LANGUAGES); do \
		echo " **CLEANDIR** $$lang"; \
		rm -rf $$lang;\
	done

files:
	find ../ -name "*.py" -o -name "*.glade"  > FILES
pot:
#	xgettext --add-comments -o $(PACKAGE).pot --files-from=FILES
	xgettext  -o $(PACKAGE).pot --files-from=FILES

po:
	@for lang in $(LANGUAGES); do \
		echo " **PO** $$lang"; \
		if [ ! -f $$lang.po ]; then \
			msginit --input $(PACKAGE).pot -o $$lang-old.po;\
		else \
			mv $$lang.po $$lang-old.po; \
		fi ; \
		msgmerge -o $$lang.po $$lang-old.po $(PACKAGE).pot; \
		rm -f $$lang-old.po; \
	done

gmo:
	@echo " **COMPILING** languages: $(LANGUAGES)"
	@for lang in $(LANGUAGES); do \
		echo " **COMPILEMO** $$lang" ; \
		mkdir -p $$lang/LC_MESSAGES/; \
		msgfmt --verbose -o $$lang/LC_MESSAGES/$(PACKAGE).mo $$lang.po; \
	done
	
install:
	@echo " **INSTALL** languages: $(LANGUAGES)"
	@for lang in $(LANGUAGES); do \
		echo " **INSTALLMO** $$lang" ; \
		mkdir -p $(DESTDIR)/usr/share/locale/$$lang/LC_MESSAGES/; \
		msgfmt -o $(DESTDIR)/usr/share/locale/$$lang/LC_MESSAGES/$(PACKAGE).mo $$lang.po; \
	done
	
