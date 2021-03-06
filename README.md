cewe2pdf
========

A python script to turn cewe photobooks into pdf documents.
The CEWE pdf export is achieved by interpreting the mcf xml-files 
and compiling a pdf document which looks like the cewe photo book.

There are many unsupported options, so an exact conversion cannot be guaranteed. The script is mostly based on reverse-engineering and guessing. It is not meeting any official specifications. So don't be surprised if one or another feature doesn't work. However, improvements are always appreciated.

tags: mcf2pdf, mcf_to_pdf, CEWE Fotobuch als pdf speichern, Fotobuch nach pdf exportieren, cewe Fotobuch pdf, mcf in pdf umwandeln, aus CEW-Fotobuch ein pdf machen, cewe Fotobuch pdf


Install - Windows
-----------------
Download or clone this cewe2pdf repository into a folder of your choice.

The easiest way to start this Python script, is to install the latest pyhthon version.
Then from the start-menu open your pyhthon promt and install the dependencies
```
pip install lxml reportlab pillow
```

If you have installed the Anaconda Pyhton distribution, there is one catch:
Currently, there is a problem with the pillow image library in Anaconda, that prevents it from loading .webp images on Windows.
This will give the error:
`"image file could not be identified because WEBP support not installed"`.

To fix this, you can do the following steps.

Press Windows Start button and start the "Anaconda prompt"

Make sure you have all the dependencies installed by executing:
```
conda install lxml
conda uninstall reportlab pillow
pip install reportlab pillow
```

Install - Windows (continued)
-----------------------------
Go to the directory where cewe2pdf is installed and create a text file there with filname ``cewe_folder.txt``
and use a text editor to write the installation directory of the CEWE software into the text file.
Example
if you have the software branded for the company DM, called "dm-Fotowelt", then the file ``cewe_folder.txt`` should contain:
```
C:\Program Files\dm\dm-Fotowelt\dm-Fotowelt.exe
```
Save the file and close it.

Alternatively, you can move on to more extensive configuration by using ``cewe2pdf.ini`` instead of ``cewe_folder.txt``. The contents can, for example, be of the form:
```
[DEFAULT]
cewe_folder = C:\Program Files\Elkjop fotoservice_6.3\elkjop fotoservice
extraBackgroundFolders = C:/ProgramData/hps/5026/addons/447/backgrounds,C:/ProgramData/hps/5026/addons/448/backgrounds
```
In addition to specifying the location of the cewe folder, you may also provide a comma separated list of locations for additional background images.

Create another text file called ``additional_fonts.txt``, but leave it empty.

Install - Linux
---------------

Copy the script where your album is (`*.mcf` file)

Ensure the python dependancies are installed.

On Fedora :
```
sudo dnf install python2-lxml python2-reportlab
```

Define the CEWE path (the directory where your CEWE album software is installed. You can recognize it by the many `.so` files and some subdirs like `Resources`). Put this directory name into a file named `cewe_folder.txt`.

Example with my CEWE FOTOWELT is installed in /home/username/CEWE/CEWE FOTOWELT/ :
```
echo "/home/username/CEWE/CEWE FOTOWELT/" > cewe_folder.txt
```

Example with my CEWE software in /opt/CEWE :
```
echo "/opt/CEWE" > cewe_folder.txt
```

Define some additionnal fonts (`name = /path/to/file.ttf`) into a file named `additionnal_fonts.txt`

This will create an empty file :
```
touch additionnal_fonts.txt
```

You can edit additionnal_fonts.txt and add the fonts you want.

Install - continued
-------------------

At this point, you should have these files in your current directory :
* `cewe2pdf.py`
* `cewe_folder.txt`
* `additionnal_fonts.txt`
* your `*.mcf` file
* a directory named `<album>_mcf-Datein`

How to use
----------

Just run `cewe2pdf.py` and you will find a new pdf file to appear in your current directory.
Example:
```
   python cewe2pdf.py c:\path\to\my\files\my_nice_fotobook.mcf
```

Options
-------
currently cewe2pdf supports the following options. They are shown if you run

``` python cewe2pdf.py --help```
```
usage: cewe2pdf [-h] [--keepDoublePages] [inputFile]

Convert a foto-book from .mcf file format to .pdf

positional arguments:
  inputFile          the mcf input file. If not given, the first .mcf in the
                     current directory is used. (default: None)

optional arguments:
  -h, --help         show this help message and exit
  --keepDoublePages  Each page in the .pdf will be a double-sided page,
                     instead of a normal single page. (default: False)

Example:
   python cewe2pdf.py c:\path\to\my\files\my_nice_fotobook.mcf

```


Development
-----------
To create a stand-alone compiled package, you can use
```
pip install pyinstaller
pyinstaller cewe2pdf.py --onefile
```

To run the unit-test you also need to install
```
pip install pytest pdfrw
```
You can then call pytest from the working directory or use the runAllTests.py file.
