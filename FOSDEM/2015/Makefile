default: all

all: makedirs dirs README.txt STATUS.txt

makedirs: index.html
	for i in `grep 'href=".[^"]*/"' $< | cut -f 2 -d '"'`; do \
	  [ -e $$i ] || mkdir $$i; \
	  [ -h $$i/Makefile ] || \
	  [ $$i == ../ ] || \
	    ln -s ../Makefile.subdir $$i/Makefile; \
	done

PHONY = 

define DIR_template
$(1):
	make -C $(1)

PHONY += $(1)
endef

DIRS = $(patsubst %/Makefile,%,$(wildcard */Makefile))
$(info $(DIRS))

$(foreach dir,$(DIRS),$(eval $(call DIR_template, $(dir))))

dirs: $(DIRS)

BASE = https://video.fosdem.org/2015/

index.html:
	wget -O $@.new $(BASE)
	mv $@.new $@

README.txt:
	wget -O $@.new $(BASE)$@
	mv $@.new $@

STATUS.txt:
	wget -O $@.new $(BASE)$@
	mv $@.new $@

.PHONY: default all index.html README.txt STATUS.txt dirs $(PHONY)
