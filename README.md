# PDFtoCSV
A script to take multiple PDF files as input and output their text in a CSV file

The guide below is copied from the Guide.ipynb Jupyter Notebooks file. Some formatting, instructions, and links might therefore not be accurate. For best results, open Guide.ipynb in Jupyter Notebooks

Guide for Installation and Use
Prerequisites
Anaconda & Jupyter Notebooks
We recommend using this program via the Anaconda Data Science Platform. This includes Jupyter Notebooks, and you likely already have it installed if you are viewing this file.
This program can also be run via any Python interpreter, including from the command line, if you have the technical knowledge to do so.

Python 3
This program is written using the latest version of Python to date. To ensure you are ready to run it, ensure that the top right corner of your Jupyter Notebook says Python 3. If it does not, try to change it by going to the Kernel menu, choosing Change Kernel, then Python 3. If you do not see this option, you may need to download the latest version of Anaconda here.

With that, you should be able to follow the steps below and get going within a few minutes!

Installation
The following steps are required before the program is run for the first time. They do not need to be repeated again on the same computer.

1. Install Tesseract
Tesseract is the tool this program uses to read text from pages that do not have machine-readable text. It is is a free, open-source program (sponsored by Google) that performs Optical Character Recognition (OCR). It must be installed first for this program to work properly. More information about Tesseract OCR can be found here.

Windows
Download the Tesseract OCR installer here.
Run the .exe file once it has been downloaded.
Accept all default options.

Mac
The easiest way is to install via Homebrew, a handy installer that works to easily install all kinds of usefuly programs, in addition to Tesseract OCR.
-Open Terminal (Press Command + Space, type "Terminal", press Enter)
-Paste: /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
-Press Enter
-Press Enter again
-Enter your computer password to authorize installation when prompted
-Homebrew has successfully installed once you see ==> Installation successful!
-Paste the following: brew install tesseract
-Press Enter
For experienced users, see here for other installation options.

Linux
If your distribution uses apt, like Ubuntu, the following should install Tesseract OCR:
sudo apt install tesseract-ocr
See here for more detailed instructions for a wide variety of distributions

2. Prepare Python
The cell below installs the Python programs required for this program to run.
Execute the cell by clicking on it and pressing Shift+Enter.

[-]


%run "installDependencies.py"
from IPython.core.display import HTML
HTML("<script>Jupyter.notebook.kernel.restart()</script>")
If the output above indicates All packages are installed, you are good to start using the program!

If not, try opening your command line (Windows: Open the program "Command Prompt", Mac: Open the program "Terminal") and paste the following, then press Enter: python -m pip install unidecode pytesseract PyMuPDF natsort

How to Use the Program

Prepare Your PDF Input

Legible Black and White Typed Text
It works best with PDF files that have clearly legible typed black text on a white background. The majority of the text should be in the same font and the same size. The program will still try to process files with coloured backgrounds or various non-standard fonts, but the quality of the output may be low.

Clearly Labelled Files
The output will be one single CSV file (can be opened as a spreadsheet in Microsoft Excel). The text from each page of each document will be included on a separate line. Each line will have: 
-The path of the source file, including preceding folders and the name of the file (Eg. "path/to/folder/with/PDF/2019/January/1Jan2019.pdf")
-The page number, relative to each file
-The number of words captured from the page
-The text of the page
Because of this format, it is most convenient for you to take the time to name your folders and files descriptively. The program processes the files in the same order that they appear on your computer, when sorted by file name. However, if your folders are randomly or inconsistantly named, it will make it harder to sort and analyze the data

Awareness of Time Required
This program extracts text in two different ways. First, it tries to see if any text is already embedded in the PDF (i.e., the PDF is "machine readable"). If there is no text embedded, the program then uses Tesseract OCR to read the letters on the page as plain text. It is not crucial to understand how this works, but it will make a different for how long the file(s) will take to process.

Machine readable PDF: ~0.009 seconds/page
Non-machine readable: ~1 second/100 words on page
While this does not make a large difference if the file has only a few pages, the time difference increases with larger files, and can take days for 20,000+ pages. In order to accurately estimate the time required, open up your PDF files and determine whether they are machine readable or not. The easiest way is to search for a word you know is in the file. If your PDF reader finds the word, it has "read" the file, and the file is machine readable. If it does not, it is likely not machine readanble, and will require OCR. Another way of checking is to try to highligh the text with your mouse, if it highlights the lines of text, the page is likely machine readable. If it highlights the entire page as one large box, it is likely not.
For larger files, it is common to have some non-machine readable files distributed within machine readable pages. This is common with advertisements in newspapers, for example. The program will process any machine readble file accordingly, and only use OCR on individual pages when necessary, so such file should still be processed relatively quickly.
In order to optimize the speed of processing, minimize other tasks being performed by your computer at the same time. Computers have limited processing resources, so watching videos, surfing the internet, or writing in a word processor will all negatively impact the processing time for your files. This is not to say that one cannot multitask while processing files, and the effect is only noticable on large batches of non-machine readable files that are continually processing for hours or days at a time.

Run the Program
In Jupyter Notebooks
In Jupyter Notebooks, you can either use the cell below (Under "Ready to Go!"), or navigate to the folder where you downloaded this program and create a new notebook.
In a new cell, paste: %run PDFtoCSV.py "path/to/folder/with/PDF"

From Command Line
If you do not want to run the program via Jupyter Notebooks, it is possible to run via the command line (Command Prompt or Terminal), by running the following command python path/to/download/PDFtoCSV.py /path/to/folder/with/PDFs, replacing the first path with the location of this program and the second with the location of your PDFs.

Ready to Go!
You are ready to start extracting text from your PDF files!
The simplist way is to use the cell below. Simply replace the section in quotation marks with the path to the file or folder you want to convert. For instructions on copying and pasting paths, see below.

%run PDFtoCSV.py "example/path/to/folder/with/PDFs"
Just in case you accidentally erased the command above, here it is again for you to copy and paste:
%run PDFtoCSV.py "example/path/to/folder/with/PDFs"

Troubleshooting Common Issues
Please enter a valid file or directory / The folder you have entered does not contain any PDF files
Include the full and exact spelling and syntax of the path to your file or folder. The best way to ensure this is to copy it directly, here's how:
Open the folder containing the folder or file you want to copy
On Windows:
Hold Shift and right click on the folder or file
Left click on the menu option "Copy as Path"
On MacOS
Right click on the folder or file
Hold the Option button
Left click on the menu option "Copy name as Pathname"
Paste in the cell above, replacing "path/to/folder/with/PDF"
Be sure to put a quotation mark before and after the path you have pasted
Press Shift + Enter to run the program

"There appears to be an issue with your Tesseract OCR installation"
Refer to 1. under the "Installation" section of this guide on how to install Tesseract OCR. If you have it installed, try uninstalling and re-installing, being sure to accept all default options on the installation.
"I could not find your Tesseract-OCR installation in the default location."
Refer to 1. under the "Installation section of this guide on how to install Tesseract OCR.
Open the file tesseractPath.txt in the same folder as this file, and follow the instructions there to locate your Tesseract program on Linux, or if it was installed in a non-default location on Windows or MacOS.

Other issues
This program is still in very early development, and at this point is not fully complete with robust error handling or options for non-standard situations. We attempted to make it as broadly usable as possible. Hopefully further versions will come that include more detailed options for handling unexpected issues.
