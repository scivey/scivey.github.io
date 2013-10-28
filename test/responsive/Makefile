SERVEDIR = ./serve
SCSS = ./scss
STYLESERVE=$(SERVEDIR)/css/stylish.css
STYLESERVE_MOBILE=$(SERVEDIR)/css/stylish-mobile.css
SASSMAIN = $(SCSS)/stylish.scss
SASSMAIN_MOBILE = $(SCSS)/stylish.mobile.scss
SASSALL = $(wildcard $(SCSS)/*.scss)

SRC = src/
JADEALL = $(wildcard $(SRC)/*.jade)
PAGE = ./serve/index.html
JADEPAGE = ./src/index.jade

SYNCDIR = C:\scott\proj\ghTest\scivey.github.io\test\responsive

.SUFFIXES: .jade .html

main: $(STYLESERVE) $(STYLESERVE_MOBILE) $(PAGE) sync

$(PAGE): $(JADEPAGE)
	jade --pretty $(JADEPAGE) --out $(SERVEDIR)

$(JADEPAGE): $(JADEALL)
	touch $(JADEPAGE)

$(STYLESERVE): $(SASSMAIN)
	sass $(SASSMAIN) > $(STYLESERVE)

$(STYLESERVE_MOBILE): $(SASSMAIN_MOBILE)
	sass $(SASSMAIN_MOBILE) > $(STYLESERVE_MOBILE)

$(SASSMAIN): $(SASSALL)
	touch $(SASSMAIN)

$(SASSMAIN_MOBILE): $(SASSALL)
	touch $(SASSMAIN_MOBILE)

sync:
	cp $(SERVEDIR)/*.* $(SYNCDIR)

clean:
	rm $(SERVEDIR)/*.html