SPLATTR:=/data/ackley/PART4/code/D/SPLAT/splattr
MFZRUN:=/data/ackley/PART4/code/D/MFM/bin/mfzrun
MFZGEOMETRY:={{2H2}}
MFZARGS:=$(MFZGEOMETRY) --no-std
DIR:=$(shell pwd)
DEMO:=$(shell basename "$(DIR)")

run:	$(DEMO).mfz
	$(MFZRUN) $^ run $(MFZARGS)

$(DEMO).mfz:	*.splat Makefile* 
	$(SPLATTR) *.splat $@

clean:	FORCE
	rm -rf .gen .splatgen *~ ../*~

realclean:	clean
	rm -f *.mfz

.PHONY:	FORCE
