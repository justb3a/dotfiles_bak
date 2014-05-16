SHELL=/bin/bash

#---------------------------------------------------------------------
# executables
#---------------------------------------------------------------------
MKDIR_P = mkdir -p
MV = mv
RM = rm -R
PTB = ${ptb}
.PHONY: directories

#---------------------------------------------------------------------
# rules
#---------------------------------------------------------------------
help:
	@echo "Please use \`make <target>\`  where <target> is one of"
	@echo ""
	@echo " - flexpaper  * DESC:  to convert a standalone PDF file to pdf, javascript, png and swf to use it for flexpaper"
	@echo "              * USAGE: please use \`make flexpaper name=<name>\` where <name> is the name of the pdf without file extension"
	@echo "              * ERROR HANDLING: use \`ptb=1\` if error \"FATAL Internal error: badly balanced softmasks/transparency groups\" occurs, use with care: QUALITY SUFFERS"

flexpaper: directories pdf js png

directories:
	if (test -d ${name}); then ${MV} ${name}/${name}.pdf ${name}.pdf && ${RM} ${name}; fi
	${MKDIR_P} ${name}
	${MV} ${name}.pdf ${name}

pdf:
	if [[ "${PTB}" == 1 ]]; then pdf2swf -f -T 9 -t -s storeallcharacters -s poly2bitmap ${name}/${name}.pdf -o ${name}/${name}.pdf.swf; else pdf2swf -f -T 9 -t -s storeallcharacters ${name}/${name}.pdf -o ${name}/${name}.pdf.swf; fi

js:
	pdf2json ${name}/${name}.pdf -enc UTF-8 -compress ${name}/${name}.pdf.js

png:
	mudraw -r100 -o ${name}/${name}.pdf_%d.png ${name}/${name}.pdf
