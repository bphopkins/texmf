# Global Custom LaTeX Macro Files, *Locally*

This document provides [instructions](#instructions) to change the TEXMFHOME location to the bph-work USB device. These instructions are generalizable to other locations.

It's kind of an annoying setup, but it can be worth it.


### Why would you want to do this?

It's a special kind of problem for people who write in LaTeX, **locally**, and have very long preambles. 
(As of 2024, Overleaf does not support global custom macro files. This is precisely why I do not use Overleaf.)

For example, I am a logician, and working in LaTeX can be a bit cumbersome when the default names of the symbols I use often have little in common with the meaning they have in my writing. So one redefines the symbols with a bit of flavor: for example, in my case, `\Vdash` gets redefined as `\trues`. Eventually there is a long list of these in the preamble of every document, which has to be copied over into each new document -- so one just offloads it all into a file, for example `logic.sty`. But eventually you have as many different `logic.sty` files as you have documents, each of which has some special command defined in it and only it.

This is where these instructions come in handy: they give you a way to have your custom LaTeX macro files stored in one place, so that you never go to use a command that's only defined in God-knows-which of your documents, for it not to compile.


## Instructions

1. Create a folder called `texmf` where you would like your custom macro files to be stored (mine is in the home directory of my USB stick). **The location of this folder cannot be changed without having to go through these steps again.** 
    - Inside `texmf`, create a folder called `tex`.
    - Inside `tex`, create a folder called `latex`.
    - Inside `latex`, create a folder for each of your macros, which has the same exact name as the primary file that will go in each folder, i.e., the exact name of the macro you intend to invoke in your preambles.
        - For example, if you have two macro files, they might be placed something like this:
            ```
            -texmf
                -tex
                    -latex
                        -logic
                            logic.sty
                        -tufte-compact
                            tufte-compact.cls
                            tufte-common.def
            ```


2. Find where your texmf.cnf file is. For example, you might search for "TEXMFHOME" in your filesystem:
    ```bash
    sudo find / -type f -exec grep -H 'TEXMFHOME' {} \;
    ```
    Running this command may take some time! In both Fedora and Ubuntu (Pop) it's at: 
    `/usr/share/texlive/texmf-dist/web2c/texmf.cnf`
    
    You might rather search for the `texmf.cnf` file, but as I recall not all systems (maybe I have Windows or Mac in mind) do not have the TEXMFHOME location information stored in a file with this name.

3. In your preferred editor, search for the line that contains `TEXMFHOME` (circa line 84) and change the default location `~/texmf` to your desired location (you might need to be root):
    - Ubuntu (Pop):  `/media/bph/bph-work/texmf`
	- Fedora:  `/run/media/bph/bph-work/texmf`

4. Update hash:
	- Ubuntu:  
        ```bash
        texhash /media/bph/bph-work/texmf
        ```
	- Fedora:
        ```bash
        texhash /run/media/bph/bph-work/texmf
        ```
    This will create a file inside the `texmf` folder called `ls-R` which directs the compiler to your custom macros.
