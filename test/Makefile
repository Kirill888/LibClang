LLVM_CFG=../build/out/bin/llvm-config
CC=gcc
CFLAGS=-std=gnu99 
LLVM_CFLAGS=$(shell $(LLVM_CFG) --cflags)
LDFLAGS=$(shell $(LLVM_CFG) --ldflags)
LIBS=-ldl -pthread -Wl,-rpath -Wl,$(shell $(LLVM_CFG) --libdir) $(shell $(LLVM_CFG) --libs core) -lclang

all: Test_Diagnostics_c Test_Diagnostics_hs Test_InclusionVisitor_c Test_InclusionVisitor_hs Test_ChildVisitor_c Test_ChildVisitor_hs

test: all
	@echo "########### TESTING ##############"
	@./runTest.sh Test_Diagnostics Test_Diagnostics.c
	@./runTest.sh Test_InclusionVisitor Test_InclusionVisitor.c
	@./runTest.sh Test_ChildVisitor Test_ChildVisitor.c

%_c : %.c
	$(CC) $(CFLAGS) $(LLVM_CFLAGS) -o $@ $< $(LDFLAGS) $(LIBS)

%_hs : %.hs
	ghc -o $@ $<

clean:
	rm *_c *_hs *.o *.hi

.PHONY = all clean test
