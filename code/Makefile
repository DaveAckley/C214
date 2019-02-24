SPLATTR:=/data/ackley/PART4/code/D/SPLAT/blib/script/splattr
MFZRUN:=/data/ackley/PART4/code/D/MFM/bin/mfzrun
MFZGEOMETRY:={{2H1}}
MFZARGS:=$(MFZGEOMETRY)
DIR:=$(shell pwd)
DEMO:=$(shell basename "$(DIR)")
TIMESTAMP:=$(shell date +%Y%m%d-%H%M%S)
DEV:=$(shell whoami)
ISHNAME:=$(TIMESTAMP)-$(DEV)
THIS_DIR:=$(strip $(notdir $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))))

$(DEMO).mfz:	*.splat Makefile* 
	$(SPLATTR) *.splat $@

run:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS)

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
