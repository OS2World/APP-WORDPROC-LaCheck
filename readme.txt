This archive contains OS/2 and DOS versions of LaCheck, a "lint"
for LaTeX (see below). New files:

 ./ 
  lacheck.exe     OS/2 1.x--2.x and DOS executable
  lacheck-32.exe  OS/2 2.x executable
  lacheck.1       man-page (see text version below)
 src/
  makefile.os2    makefile for EMX/gcc 0.8g and MSC 6.00A
  lacheck.def     linker-definition file
  lacheck-32.def

The 32-bit OS/2 executable will need the DLLs from the EMX distribution.
These are currently available as 
  ftp-os2.cdrom.com:pub/os2/2_x/unix/gnu/emx08g/emxrt.zip

--
Darrel Hankerson hankedr@mail.auburn.edu
8 August 1993

=================== LaCheck 1.8 Announcement ===============================
Newsgroups: comp.text.tex
From: abraham@research.att.com (Per Abrahamsen)
Subject: LaCheck 1.8 available for anonymous ftp
Content-Type: text/plain; charset=iso-8859-1
Message-ID: <ABRAHAM.93Aug8171213@steinhaus.iesd.auc.dk>
Sender: news@iesd.auc.dk (UseNet News)
Reply-To: auc-tex_mgr@iesd.auc.dk
Content-Transfer-Encoding: 8bit
Organization: AT&T Bell Laboratories, Murray Hill
Date: 08 Aug 1993 15:12:13 GMT


LaCheck is a tool for finding potential errors in LaTeX documents.
LaCheck catches many errors LaTeX will ignore, and LaCheck generally
gives better error messages.  Think of it as lint for LaTeX.  However,
it may also give warning for correct documents.

LaCheck should work on any Unix system that `flex' has been ported
to.  It may also work on other systems, I wouldn't know.  In
particular, no DOS binary of this version is currently available, and
I cannot create one.  LaCheck is available for anonymous ftp from:

host: ftp.iesd.auc.dk
file: /pub/TeX/LaTeX/lacheck.tar.gz

New in this version is check for italic correction:

alpha% cat test.tex
{\it Say {\sl goodbye {\em evil, cruel\/} world\/}\/}.
alpha% lacheck test.tex
"test.tex", line 1: you may need a \/ before "evil"
"test.tex", line 1: \/ not needed after non-italic text " cruel"
"test.tex", line 1: \/ not needed before italic text "world"
"test.tex", line 1: double \/ found "\/"
"test.tex", line 1: do not use \/ before "."

Also line numbers should be more correct in this version.

Man page follows:

LaCheck(1)               USER COMMANDS                 LaCheck(1)

NAME
     LaCheck - A consistency checker for LaTeX documents.

SYNOPSIS
     lacheck filename [ .tex ]

DESCRIPTION
     LaCheck is a general purpose consistency checker  for  LaTeX
     documents.   It  reads a LaTeX document and displays warning
     messages, if it finds bad sequences.  It  should  be  noted,
     that the badness is very subjective.  LaCheck is designed to
     help find common mistakes  in  LaTeX  documents,  especially
     those made by beginners.

     The things checked are:

     Mismatched groups (braces), environments and math mode  del-
     imiters.   When  a  mismatch is found, line numbers for both
     start and end of the mismatch is given. The  error  messages
     comes in pairs, one for the end match and one for the begin-
     ning, marked with `<-' and `->' respectively.

     Bad spacing including missing a `\ ' after an  abbreviation,
     missing  an  `\@'  before  a punctuation mark in a paragraph
     that is ended by an capital letter, double spaces like ` ~',
     bad  usage of ellipsis (like using ... instead of \ldots, or
     using \ldots where \cdots should be used), missing ~  before
     a  \cite  or  \ref  commands, space before footnotes, italic
     corrections before comma,  point,  or  italic  text,  italic
     correction after normal text, missing italic correction when
     switching from italic to  normal  text,  and  double  italic
     correction.

     Badly placed punctuation marks around end of math mode  del-
     imiters.  This  is,  pucktuators  placed right after display
     math end or punctuators placed right before text  math  end.
     Sequences  of  whitespace  followed by punctuation marks are
     also caught.

     Bad  use  of  quotation  characters,  i.e.  constructs  like
     "'word"  or  "word`"  are  warned  about,  tabs  in verbatim
     environments are caught, certain TeX primitives are  frowned
     upon,  attempts  to  give  font specifiers arguments such as
     \em{text} are noted, and  use  of  @  in  LaTeX  macros  are
     reported.

     LaCheck will read files  that  are  input  using  \input  or
     \include.   Files  with  suffix  `.sty' are omitted, as they
     probably will cause LaCheck to crash.

     LaCheck may be invoked from within Emacs(1) using compile:

     To run: M-x compile RET lacheck RET ,  and  then  C-x  `  to
     parse the messages

OUTPUT
     The output is UNIX-error  like,  and  may  be  parsed  using
     Emacs(1) compile mode. Here is a sample:

     lacheck compiler
     "/usr/mef/compiler.tex", line 34: missing `\ ' after "etc."
     "/usr/mef/compiler.tex", line 179: double space at " ~"
     "/usr/mef/compiler.tex", line 186: <- unmatched "}"
     "/usr/mef/compiler.tex", line 181: -> unmatched "$$"

     A control space `\ ' should  be  inserted  at  line  34,  to
     prevent  an  end-of-sentence  space.  Also, at line 179, the
     first space of the sequence " ~" should probably be deleted.
     The  last  two lines is an example, where the user mistyped,
     and probably inserted an extra "}" somewhere.

DIAGNOSTICS
     Some special cases should be explained.  In  cases  where  a
     sentence  ends  with  something  that  LaCheck  thinks is an
     abbreviation an missing `\ ' error may also  occur,  if  the
     following sentence begins with a lowercase letter.

     A mismatch error may cause more to follow, due to the chosen
     algorithm.  In  such  cases just correct the first error and
     run LaCheck again

     Braces, environments and math mode must be balanced within a
     file.

     LaCheck may be confused by  unmatched  stuff  placed  inside
     verbatim-like   environments   called  something  else  than
     exactly `verbatim'.

FILES
     /usr/local/bin/lacheck

SEE ALSO
     tex(1), emacs(1), latex(1)

BUGS
     LaCheck gets confused by advanced macros, is fooled by  sim-
     ple  macros,  can't figure out if you use a non-standard way
     to switch italic on or off, does not like TeX at  all,  does
     not  provide  any options to turn off specific warnings, and
     is at best a crude approximation.

     Ideas for improvements and bug  reports  are  very  welcome.
     Such  should  be  directed  to  the maintainers, their email
     address is <auc-tex_mgr@iesd.auc.dk>.

AUTHOR
     Kresten Krab Thorup with modifications by Per Abrahamsen.

Release 1.8           Last change: 08/05/93                     3
