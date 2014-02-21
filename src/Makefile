
prefix = /usr/local

bindir = $(prefix)/bin
mandir = $(prefix)/man/man1

INSTALL = install -c
INSTALL_PROGRAM = $(INSTALL)
INSTALL_DATA = $(INSTALL) -m 0444

# Remember to change when lacheck is updated.
REV = 1.8

# 
FTPDIR = /pack/ftp/pub/TeX/LaTeX

# Use `cc -bsd' on a next
CC = gcc -traditional

#
CFLAGS = -O # -DNEED_STRSTR 
LEX = flex -8 lacheck.lex

lacheck:	lacheck.o
	$(CC) $(CFLAGS) -o $@ lacheck.o -ll

lacheck.c:	lacheck.lex  
	$(LEX) 
	mv lex.yy.c $@

lacheck.1: 	lacheck.man  
	sed -e "s!%%LACHECKREV%%!Release $(REV)!" lacheck.man |\
	sed -e "s!%%LACHECKDATE%%!`date +%D`!" |\
	sed -e "s!%%LACHECKPATH%%!$(bindir)/lacheck!" > lacheck.1

install: 	lacheck lacheck.1
	$(INSTALL_PROGRAM) lacheck $(bindir)
	$(INSTALL_DATA) lacheck.1 $(mandir)

clean:
	rm -f lacheck lacheck.c *.o *.1 *.gz dist

dist:	lacheck.c lacheck.1 Makefile
	tar -cf lacheck.$(REV).tar lacheck.lex lacheck.man Makefile
	gzip -fv lacheck.$(REV).tar
	touch dist

ftp:	
	cp lacheck.$(REV).tar.gz $(FTPDIR) 
	cd $(FTPDIR) ; \
	rm -f lacheck.tar.gz ; \
	ln -s lacheck.$(REV).tar.gz lacheck.tar.gz

