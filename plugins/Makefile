GCCFLAGS=-Wall -g
ROOTFLAGS=`root-config --cflags --libs`
ROOFITLIBS = -l RooFitCore -l RooFit -l RooStats

TOOLSFLAGS=$(GCCFLAGS) -I$(ROOTSYS)/include -c 
SELECTORFLAGS=$(GCCFLAGS) $(ROOTFLAGS) -lProof
FIGURESFLAGS=$(GCCFLAGS) $(ROOTFLAGS) 
FITFLAGS=$(GCCFLAGS) $(ROOTFLAGS) -lRooFit -lRooFitCore -lMinuit

all: sel fig fit  
	@echo "Full build successful."


tools.o: tools.cc tools.h 
	g++ $(TOOLSFLAGS)  $(ROOFITLIBS) $(ROOTFLAGS) $< 

sel: SingleBsToPhiMuMuSelector.cc 
	g++ $(SELECTORFLAGS) $< -o $@

fig: SingleBsToPhiMuMuFigures.cc tools.o 
	g++ $(FIGURESFLAGS) $^ -o $@

fit: SingleBsToPhiMuMuFitters.cc tools.o 
	g++ -g $(FITFLAGS) $^ -o $@	

sel2011: SingleBsToPhiMuMuSelector_xCheck2011.cc
	g++ ${SELECTORFLAGS} $< -o $@

test: testMinuitFitter.cc
	g++ ${FITFLAGS} $< -o $@


clean:
	rm -rf tools.o sel fig fit 
