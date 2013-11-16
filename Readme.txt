GameMaker Spreadsheet 1.0

The GameMaker spreadsheet is an OpenOffice macro-enabled spreadsheet that can be used to print play money and cards for board games.

Features:
=========
- Save and load templates for cards and play money
- Insert pictures into cards and money templates
- A metalanguage for loading data
- Two-sided templates

Spreadsheet Organization
========================
The spreadsheet has 7 worksheets, each with a difference purpose.
- Sheet 1 is output for the play money
- Sheet 2 is output for cards
- Sheet 3 is the basic user interface for creating and editing templates
- Sheet 4 is the data sheet for cards
- Sheet 5 is where play money templates are stored
- Sheet 6 is where card templates are stored
- Sheet 7 is an extra scratch page used internally by the program

Creating, Saving, and Editing templates
=======================================
Sheet 3 is where you will be doing all of your editing work.  On the left side of the spreadsheet you will see options and buttons.  Options for printing play money are listed in cells A4 through A9.  Options for printing cards are listed in cells A13 through A20.
To create a template simply use the spreadsheet to enter and format text, borders, and images in the cell range you specify on Sheet 3.

Money options
=============

A4-A5. Denomination
In cell A5, enter the denomination of money you would like to save the template as.  When you go to load this template it will be listed as the name you inserted into cell A5.

A6-A7. Template Range
In cell A7, enter the template range of the money template.  Templates typically start at cell E22 but you can start anywhere you'd like (outside of column A).  Enter the range in AX:BY form.
For 2 sided templates, list two different ranges separated by a comma and no spaces.  It should look like AX:BY,CX:DY form.

A8-A9. Output Rows,Cols
In cell A9, put the number of rows and columns of play money you would like to print.  When you hit the print button copies of these templates will be put on Sheet 1 for physical printing.

The money drop-down list contains a list of saved money templates.  To load a saved template, simply select it on the drop-down list.

Pressing the Save button saves a money template to Sheet 5 for later retrieval.

Pressing the Delete button removes a money template from the list of saved money templates.

Pressing the Print button prints the currently loaded template to Sheet 1 for physical printing.  


Card Options
============

A13-A14. Type
In cell A14, enter the name of the type of card you would like to save the template as.  When you go to load this template it will be listed as the name you inserted into cell A14.

A15-A16. Template Range
In cell A16, enter the template range of the card template.  Templates typically start at cell E22 but you can start anywhere you'd like (outside of column A).  Enter the range in AX:BY form.
For 2 sided templates, list two different ranges separated by a comma and no spaces.  It should look like AX:BY,CX:DY form.

A17-A18. Data Rows
In cell A18, enter the range(s) of data rows, separated by commas, of the rows on Sheet 4 that will be used when printing cards.  Uses dashes to list row ranges.  Example: 4-12,15-20 uses rows 4 though 12 and 15 through 20 on sheet 4 as data sheets.
See the section on the data row metalanguage to better understand how the data rows will be used during output.

A19-A20. Output columns, Horizontal pad cells, Vertical pad cells
In cell A20, enter the number of output columns, horizontal pad cells, and vertical pad cells used when printing cards.  These should be separated by a comma with no spaces.

The money drop-down list contains a list of saved money templates.  To load a saved template, simply select it on the drop-down list.

Pressing the Save button saves a card template to Sheet 6 for later retrieval.

Pressing the Delete button removes a card template from the list of saved card templates.

Pressing the Print button prints the currently loaded template to Sheet 2 for physical printing.

2-Sided printing options
========================
Options for two-sided printing appar to the right of the other options.  These options are designed to make two supplied templates to have equal width and height for 2-sided printing.

The options are stored in a drop-down box.  They are as follows:
-Column: Select column to adjust
This allows the user to select a specific column within the range to be adjusted and only adjusts that specific column's width.

-Column: Proportionally adjust all
This option proportinally adjusts all columns in the template to be changed so tha the total width equals that of the other template.

-Column: Copy all widths
This option copies the widths of all columns to the other template.

-Row: Select row to adjust
This allows the user to select a specific row within the range to be adjusted and only adjusts that specific row's width

-Row: Proportionally adjust all
This options proprtionally adjust all row heights in the template to be changed so that the total height equals that of the other template.

-Row: Copy all heights
This option copies the heights of all rows to the other template.

To execute the selected option push one of the 4 buttons below the drop down list.  The buttons for card templates will be disabled when you save or load a money template.  The buttons for money templates will be disabled when you save or load a card template.  The "left" size refers to the first template listed in the appropriate template cell, while the "right" size refers to the second one listed there.


Best practices for 2-sided printing
===================================
A major issue in 2-sided printing is that of alignment.  To test alignment, simply put two different templates with some text and a thick border around them, print 2 or more rows of these templates, and make sure that you cannot see any lines through the other side.

To set up 2-sided printing, go to Page Preview, Format Page.  Under the Page tab, make sure left and right margins are equal, top and bottom margins are equal, set the page layout to "Mirrored", and make sure that both table alignment options are turned off.  Under the Sheet tab, select the Page order to be "Left to right, then down".  When you print, select "2-sided printing" under printer properties.  Do not select options such as "Flip pages up", "Preserve Layout" or multiple pages per sheet.

You may need to manually adjust the column widths between columns and you will need to adjust the columns widths on the outside.  The total width for each page should be 8 1/2 inches (including margins) but you will need to adjust the first page's width to be slightly less, and that "slightly less" amount is determined by your printer.

Using the Data Metalanguage
===========================
The data metalanguage is used to grab data from the data worksheet and insert it into the output print area for cards.

The text of each of the template cell is interpreted according to the rules of the metalanguage.  If no metalanguage instructions are found, then nothing is done to the text.  If starting with a metalanguage instruction, you may need to change the cell's number format to "text" from "currency".

Each metalanguage instruction begins with either a $ or a ^.  Here is a brief overview:

Metalanguage Instructions
=========================
$$: Output literal $.
$n: Output the data in column n of the current data row.
$?n: Test if column n of the current data row has data.  If not, skip the next metalanguage instruction.
$!: Advance the column to the next column with data in the current row.
$+n: Go forward n columns.
$-n: Go backward n columns.
$>: Go forward 1 column.
$<: Go backward 1 column.
$#: Begin Format processing.
$*: Begin picture insertion processing for the picture.
$@: Insert a picture to take up the entire cell.

^^: Output literal ^.
^n: Move to row n. 
^+n: Go down n rows.  If n is ~, go down rows until you reach a row without data in the current column.
^-n: Go up n rows.  If n is ~, do up rows until you reach a row without data in the current column.

$x,^y: Move to column x, row y.
$c or ^c: Output the data in the current column and row.

Formatting instructions
=======================
Formatting instructions are separated by a # and processed until a ## or the end of the input is reached.  They are as follows:

Font formatting
#FB: Bold the font.
#FI: Italicize the font.
#FSTK: Font strikethrough.
#FSUB: Font subscript.
#FSUP: Font superscript.
#FUN: Font underline.
#FZn: Set the Font size to n.
#FCr,g,b: Set the Font color to (red,green,blue).  Note: each value must be between 0 and 255 inclusive.
#FSxxx: Set the Font name to xxx.

Border formatting
All border formats begin with #BX, where X is the border to change.  Options for X are (T)op, (B)ottom, (L)eft, (R)ight, and (A)ll.
#BXWn: Set the border width to n.
#BXCr,g,b: Set the border color to (red,green,blue).  Note: each value must be between 0 and 255 inclusive.
#BXA: Add border.
#BXD: Delete border.

Alignment options
#VB: Vertically align text to cell bottom.
#VC: Vertically align text to cell center.
#VS: Vertically align text to the standard alignment (usually bottom).
#VT: Vertically align text to cell top.
#HC: Horizontally justify text to cell center.
#HS: Horizontally justify text to the standard alignment (usually left).
#HD: Horizontally justify text to be evenly distributed.
#HL: Horizontally left justify cell text.
#HR: Horizontally right justify cell text.

Cell orientation options
#OD: Orient cell downward.
#OH: Orient cell horizontally.
#OU: Orient cell upward.
#OV: Orient cell in a stacked fashion.

#Cr,g,b: Sets the cell's background color to (red,green,blue).  Note: each value must be between 0 and 255 inclusive.

#$: Get formatting information from the data sheet (use the metalanguage rules above to navigate the data sheet).

Picture Insertion Instructions
==============================
Picture insertion instructions are separated by a * and processed until a ** or the end of input is reached.  They are as follows:

*@: Resize the picture to fill the entire cell and then place it.
*$: Get picture location information from the data sheet (use the metalanguage rules above to navigate the data sheet).
*wn: Set the picture width to n.
*hn: Set the picture height to n.
*>: Insert the next picture right next to the last inserted one.
*=: Insert the next picture right below the last inserted one.
