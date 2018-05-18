## 800 Extra Dependencies

Some Rails applications require extra dependencies that need to be installed for certain portions of the application to run correctly. These dependencies can be installed once per server even with multiple Rails application running on the same machine. While these dependencies are not required for the Rails applications to run, they may be needed to allow certain components of the Rails application to behave correctly.

### 810 LaTeX

**NOTE: Required for Slice and CHAT Publications**

While the Ruby gem PDFKit allows a Rails application to quickly generate PDF documents directly from HTML, these often lack the quality that can be provided by compiling a PDF directly from LaTeX. Our first application using LaTeX PDF rendering using Embedded Ruby (ERB) is Slice. The Rails application will require the location of the pdflatex binary that is installed so that it can use this to render PDFs. Please note that this location is different depending on the operating system. Also note that TeX uses an [interesting versioning numbering system](http://en.wikipedia.org/wiki/Software_versioning#TeX) that progressively approaches the Greek letter pi.

#### Download and Install LaTeX (CentOS 6/7)

Original url, however doesn't work with wget: http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz

```
sudo yum -y install perl-Digest-MD5

cd ~/code/source
curl -L http://mirrors.ibiblio.org/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz | tar xvz
cd install-tl-*
sudo ./install-tl

Actions:
 <I> start installation to hard disk
 <H> help
 <Q> quit

Enter command: O
Enter command: D
Enter command: R
Enter command: I
```

Check that pdflatex was installed

```
/usr/local/texlive/2018/bin/x86_64-linux/pdflatex --version
```

```console
pdfTeX 3.14159265-2.6-1.40.19 (TeX Live 2018)
```

Finally, make sure to modify `[sleepdata.org|tryslice.io]/config/application.yml` to point to the correct pdflatex binary

```yml
latex_location:       "/usr/local/texlive/2017/bin/x86_64-linux/pdflatex"
```

#### Download and Install LaTeX (macOS)

Download and install MacTeX pkg (recommended)  (~3.14 Gb)

  http://www.tug.org/mactex/

Verify LaTeX is installed

```
which pdflatex
```

```console
/Library/TeX/texbin/pdflatex
```

```
pdflatex --version
```

```console
pdfTeX 3.14159265-2.6-1.40.18 (TeX Live 2017)
```

#### Download and Install LaTeX (Windows)

Download and install MiKTeX (recommended) (~153 Mb)

  http://miktex.org/download
