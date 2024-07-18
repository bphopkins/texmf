# texmf

This document provides instructions to change the TEXMFHOME location to the bph-work usb device.


Find where your texmf.cnf file is
	find /usr -type f -exec grep -il 'TEXMFHOME' {} \;

	sudo nano <output>
		On Pop_OS it was: /usr/share/texlive/texmf-dist/web2c/texmf.cnf
		Same in Fedora

	
Change ~/texmf to:
	Ubuntu (Pop):  /media/bph/bph-work/texmf
	Fedora:  /run/media/bph/bph-work/texmf

To update hash (only if texmf files have been modified)
	Ubuntu:  texhash /media/bph/bph-work/texmf
	Fedora:  texhash /run/media/bph/bph-work/texmf
