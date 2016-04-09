# Download journals in bulk from the Medical Heritage Library

The [Medical Heritage Library](http://www.medicalheritage.org/) is terrific for searching and browsing, but it also has great potential for text- and image-mining. In order to work with the MHL's materials at scale, you'll need to download a large number of documents. You *could* individually download every document you want, but with some simple commands, you can speed up that process significantly. Plus you can use these apply basic techniques to many different bulk-downloading tasks.

In this tutorial, we'll learn how to use a program called **wget** to download the entire run of a journal from the Medical Heritage Library.

As is the case with so many technical tasks, formatting and manipulating your data (in this case, your list of journal volumes) is *much* more time-consuming than actually doing the thing you're interested in doing! So we'll proceed in four basic steps:

1. Download and install some free software.
1. Decide which journals we want.
1. Set up a document that contains the URLs of these journals. (This is the time-consuming part!)
1. Use wget to download these journals.

This tutorial has many steps, but that's only because it combines these four basic tasks. Each step should be straightforward, and this process will go faster the next time you do it.

## 1. Install a text editor

You'll need a decent text editor in order to properly format your URLs. Microsoft Word and the like won't work, because these word processors embed invisible characters in your document in order to provide formatting information. We'll use a text editor for this tutorial. If you go on to do any programming or coding later, you'll be glad you have one.

Let's use Atom, which is free and has versions for both Macs and PCs. Head to [https://atom.io/](https://atom.io/) to download and install the Atom text editor.

![][1]

[1]: images/download-journals-in-bulk-from-the-medical-heritage-library/install-a-text-editor.png

## 2. Install wget

Wget is a small software package that you run from your computer's **command line**. Its specialty is downloading webpages and files from the web. It's the program that we'll use later in this tutorial to download our journals. I won't walk you through the steps to install wget because a good tutorial already exists [here](http://programminghistorian.org/lessons/automated-downloading-with-wget).

Follow the linked tutorial until you get to **Step Two** (or follow the tutorial all the way through, since it's very helpful in understanding how wget works).

## 3. Figure out what you want (1)

The MHL has made our life a lot easier by providing a list of all its journals in a spreadsheet. You can download the spreadsheet by going to the MHL's [list of journals](http://www.medicalheritage.org/historical-american-medical-journals/) and clicking on the link shown below.

(**CSV**, which stands for **comma-separated values,** is a generic term for a spreadsheet. It's a little bit like a .txt document versus a .docx document. By default, CSVs usually open in Excel, or whichever spreadsheet application you have on your computer.)

![][2]

[2]: images/download-journals-in-bulk-from-the-medical-heritage-library/figure-out-what-you-want--1-.png

## 4. Figure out what you want (2)

Double-click the CSV file you downloaded. It should open in Excel, if you have Excel installed. (If you don't have Excel, you can open the file in something like [Google Sheets](https://docs.google.com/spreadsheets/u/0/).) Look over the list of journals and decide which one you'd like to download in bulk. For the purposes of this tutorial, let's focus on the *American Homeopath*.

Let's delete the rest of the journals on our spreadsheet, just to make our spreadsheet a little easier to work with. While you're at it, you can delete all of the columns except the URL column, since we won't be using them.

![][3]

[3]: images/download-journals-in-bulk-from-the-medical-heritage-library/figure-out-what-you-want--2-.png

## 5. Investigate the URLs (1)

Our spreadsheet contains URLs, but they don't go straight to the PDFs that we want to download. Instead, they go to a main page for that journal volume, which contains an embedded book viewer, plus links to the journal volume in different formats.

![][4]

[4]: images/download-journals-in-bulk-from-the-medical-heritage-library/investigate-the-urls--1-.png

## 6. Investigate the URLs (2)

Let's take a closer look at those links to the volume in different formats. If you right-click on the **PDF** link on the lower right-hand part of the page, you can copy the link address.

Paste it into a text document, so you can see what the address is. It should look something like [https://archive.org/download/homoeopa12chic/homoeopa12chic.pdf](https://archive.org/download/homoeopa12chic/homoeopa12chic.pdf) .

![][5]

[5]: images/download-journals-in-bulk-from-the-medical-heritage-library/investigate-the-urls--2-.png

## 7. Compare the two URLs

If you compare the URL that goes to the PDF with the URL that goes to the main page for each journal volume, you'll see that they're a lot alike, but they also contain a couple of differences. Where the first link contains the word **details**, the second contains the word **download**. And the second URL has an extra chunk at the end: **/homeopa12chic.pdf**.

In order to automatically download the journal volumes as PDFs, we need to alter our column of URLs so that instead of linking to the main page for each journal volume, each link goes directly to the PDF for that volume.

![][6]

[6]: images/download-journals-in-bulk-from-the-medical-heritage-library/compare-the-two-urls.png

## 8. Alter the URLs (1)

The first part of our task is pretty simple. We can use **find and replace** (**Edit -> Find -> Replace**) to replace details with download.

But what about that extra piece at the end?

![][7]

[7]: images/download-journals-in-bulk-from-the-medical-heritage-library/alter-the-urls--1-.png

## 9. Alter the URLs (2)

There are many ways we could get the results we need, but let's stick with Excel. (You can do this with Google Sheets, too.) We'll start by separating each part of the URL into a different cell, so that the URLs are easier to work with.

Select the URLs in the URL column. Then, from Excel's **Data** tab, click on **Convert Text to Columns**. In the window that pops up, select **Delimited. **Then, in the next window, select the **Other** radio button and enter / as the delimiter. This means that the fields you want to separate are divided by a /.

Then click **Finish**.

![][8]

[8]: images/download-journals-in-bulk-from-the-medical-heritage-library/alter-the-urls--2-.png

## 10. Your URLs are broken into chunks

Your URLs will be a little easier to work with, now that each part of them is in a separate cell.

![][9]

[9]: images/download-journals-in-bulk-from-the-medical-heritage-library/your-urls-are-broken-into-chunks.png

## 11. Alter the URLs (3)

Now copy the last column into the next column (column **F **in the image below). And in the next column (column **G **in the image below), copy .pdf into every row.

(You can type .pdf into cell G1, then grab the cell's bottom right corner and drag it straight down to copy .pdf into every cell in the column.)

![][10]

[10]: images/download-journals-in-bulk-from-the-medical-heritage-library/alter-the-urls--3-.png

## 12. Alter the URLs (4)

OK, we now have the basic parts we need for each URL. Let's glue those addresses back together.

In the next column (column **H** in the image below), enter the following fomula: =CONCATENATE(A2,"/",B2,"/",C2,"/",D2,"/",E2,"/",F2,G2). This instructs Excel to combine all the preceding cells in the row, separating each part with a backslash. The one exception is the last part of the URL, **.pdf**, which doesn't have a preceding slash.

After you enter the formula, press return. Now we want to paste that formula into every cell. Drag the bottom right corner of the cell into which you've entered the formula (cell **H2** in the image below) straight down, so that the formula is copied into each cell in column **H**, until you reach the end of your list of URLs.

Luckily, Excel is smart enough to modify the formula as you paste it down, so that the formula refers to the cells in the appropriate row.

![][11]

[11]: images/download-journals-in-bulk-from-the-medical-heritage-library/alter-the-urls--4-.png

## 13. You have your URLs!

At last, we have URLs that lead directly to the PDFs we want! Try pasting one into your browser's address bar in order to make sure it works. The URL should lead directly to the PDF version of the journal volume.

Now, copy your new URLs into the **Atom** text editor you downloaded in the first step.

![][12]

[12]: images/download-journals-in-bulk-from-the-medical-heritage-library/you-have-your-urls-.png

## 14. Save your URLS as plain text

Now your URLs (the ones that link to PDFs) should be copied into a new document within the Atom text editor. We won't do much with them, though. We'll just save that text document as **urls.txt**. Save that document into a new, empty folder on your computer (I've called my new folder **journals**), since this is also where your downloaded journals will reside.

An aside: You might wonder why we have to go through all of this, when all we're doing is copying and pasting our list of URLs. You *do* have a built-in text editor on your Mac, called **Text Edit**. But that's not a good choice for cutting and pasting your URLs from Excel. That's because when you copy your URLs from Excel, that block of text retains some invisible, Microsoft-specific characters called **carriage returns** at the end of every line. Those carriage returns will confuse wget. Text Edit doesn't eliminate those carriage returns, but Atom is smart enough to remove them.

![][13]

[13]: images/download-journals-in-bulk-from-the-medical-heritage-library/save-your-urls-as-plain-text.png

## 15. Navigate to the folder in which you stored your list of URLs

You may remember, from back when we downloaded our virtual machine, that you can use the **command line** (also called the **terminal** or **command prompt**) to make your way into different folders on your computer. We need to do that again, in order to run wget from the right place.

Follow **steps four and five** on [this tutorial](https://github.com/bmschmidt/medicalHeritageVM), except instead of navigating into the medicalHeritageVM-master folder, navigate into the folder in which you've stored your list of URLs.

![][14]

[14]: images/download-journals-in-bulk-from-the-medical-heritage-library/navigate-to-the-folder-in-which-you-stored-your-list-of-urls.png

## 16. Run a little bit of code

This part could hardly be easier! Now that you're in the folder that contains **urls.txt**, type wget -i urls.txt into your terminal or command prompt. (If you named your list of URLs something besides **urls.txt**, substitute that name for **urls.txt** in the code snippet.)

Now watch as your computer automatically downloads your files into the same folder where your list of URLs resides!

![][15]

[15]: images/download-journals-in-bulk-from-the-medical-heritage-library/run-a-little-bit-of-code.png

## 17. Success!

When your computer finishes obtaining those journal volumes, you'll have a folder full of PDFs, ready to be mined.

The next time you do this, things will go much more quickly, since you'll have all the software installed and ready to go.

You can use these same techniques for many bulk-downloading tasks in the future. Manipulating URLs (and other structured data) is easier if you have a tool called [OpenRefine](http://openrefine.org/) on your computer. So if you've caught the data-manipulation bug, you may want to install OpenRefine and [follow a tutorial on how to use it](http://programminghistorian.org/lessons/cleaning-data-with-openrefine). Then you'll have bulk-downloading superpowers!

![][16]

[16]: images/download-journals-in-bulk-from-the-medical-heritage-library/success-.png
