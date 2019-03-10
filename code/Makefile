SPLATTR:=/data/ackley/PART4/code/D/SPLAT/blib/script/splattr
MFZRUN:=/data/ackley/PART4/code/D/MFM/bin/mfzrun
MFZGEOMETRY:={{2H2}}
MFZBIGGEOMETRY:={{1H1}}
MFZBIG1GEOMETRY:={{1G1}}
MFZARGS:=$(MFZGEOMETRY) -n
MFZARGS_MOVIE_FIXEDAER:=$(MFZGEOMETRY) -n -a 0 -p 30 -e 10
MFZARGS_MOVIE_ACC:=$(MFZBIGGEOMETRY) -n -a 0 -p 30 -e 0 --accelerate 150 --warpfactor 1
MFZARGS_TILES_MOVIE_ACC:=$(MFZGEOMETRY) -n -a 0 -p 30 -e 0 --accelerate 150 --warpfactor 1
MFZARGS_TILES_MOVIE_SURGE:=$(MFZGEOMETRY) -n -a 0 -p 30 -e 0 --accelerate 150 --surge 300 --warpfactor 1
MFZARGS_BIGMOVIE:=$(MFZBIG1GEOMETRY) -n -a 0 -p 30 -e 5
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

tilemovie:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS_TILES_MOVIE_ACC)

tilemoviesurge:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS_TILES_MOVIE_ACC)

big1movie:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS_BIGMOVIE)

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
