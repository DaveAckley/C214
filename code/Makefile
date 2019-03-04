SPLATTR:=/home/ackley/PART4/code/D/SPLAT/blib/script/splattr
MFZRUN:=/home/ackley/PART4/code/D/MFM/bin/mfzrun
MFZGEOMETRY:={{1H1}}
MFZBIGGEOMETRY:={{2H1}}
MFZARGS:=$(MFZGEOMETRY) -n
MFZARGS_MOVIE_FIXEDAER:=$(MFZGEOMETRY) -n -a 0 -p 30 -e 10
MFZARGS_MOVIE_ACC:=$(MFZBIGGEOMETRY) -n -a 0 -p 30 -e 0 --accelerate 150 --warpfactor 1
DIR:=$(shell pwd)
DEMO:=$(shell basename "$(DIR)")
TIMESTAMP:=$(shell date +%Y%m%d-%H%M%S)
DEV:=$(shell whoami)
ISHNAME:=ISH-$(TIMESTAMP)-$(DEV)
THIS_DIR:=$(strip $(notdir $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))))
SPLAT_FILES:=$(wildcard *.splat)
ULAM_FILES:=$(wildcard *.ulam)

$(DEMO).mfz:	$(SPLAT_FILES) $(ULAM_FILES) | Makefile* 
	$(SPLATTR) $^ $@

run:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS)

movie:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS_MOVIE_FIXEDAER)

movie2:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS_MOVIE_ACC)

clean:	FORCE
	rm -rf .gen .splatgen *~ .*~ ../*~

realclean:	clean
	rm -f *.mfz

ishtar:	FORCE
	@make realclean
	@make >ISH-BUILD-STDOUT.txt 2>ISH-BUILD-STDERR.txt || true
	@cd ..;tar czf $(ISHNAME).tgz $(THIS_DIR) --transform s/^$(THIS_DIR)/$(ISHNAME)/
	@echo Made ../$(ISHNAME).tgz

.PHONY:	FORCE
