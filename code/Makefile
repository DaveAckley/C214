SPLATTR:=/data/ackley/PART4/code/D/SPLAT/blib/script/splattr
MFZRUN:=/data/ackley/PART4/code/D/MFM/bin/mfzrun
MFZGEOMETRY:={{2H1}}
MFZARGS:=$(MFZGEOMETRY) -n
MFZARGS_MOVIE_150AER:=$(MFZGEOMETRY) -n -a 0 -p 30 -e 5
MFZARGS_MOVIE_ACC:=$(MFZGEOMETRY) -n -a 0 -p 30 -e 0 --accelerate 180 --surge 360
DIR:=$(shell pwd)
DEMO:=$(shell basename "$(DIR)")
TIMESTAMP:=$(shell date +%Y%m%d-%H%M%S)
DEV:=$(shell whoami)
ISHNAME:=ISH-$(TIMESTAMP)-$(DEV)
THIS_DIR:=$(strip $(notdir $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))))

$(DEMO).mfz:	*.splat *.ulam | Makefile* 
	$(SPLATTR) $^ $@

run:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS)

movie:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS_MOVIE_150AER)

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
