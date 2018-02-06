# lookout

## Introduction

Some calendar tools such as Outlook allow for exporting diary data as
CSV (Comma Separated Value) file.  This package, `lookout.el`, allows
for importing such files into Emacs.

In order to import a CSV file you have to call `lookout-create-diary`.
When you call `lookout-create-diary` make sure that the target file
does not exist or contain valuable data.  The contents of the target
diary file are lost!

You have to tell `lookout-create-diary` how to interpret the CSV
data.  This is done by configuring the variable
`lookout-diary-mapping-table`.  The way how diary data are formatted is
determined by the variables `lookout-appointment-format` and
`lookout-unmarked-categories`.  You can adjust these parameters by
calling

    M-x customize-group RET lookout RET

In order to make things secure and work properly it is recommended to
direct the output of `lookout-create-diary` to a separate file, which
gets included from the "real" diary file.  Put the line

    #include ".../my-lookout-diary"

in your diary file.  You probably want to add the following lines to
your `~/.emacs`:

    (add-hook 'list-diary-entries-hook 'include-other-diary-files)
    (add-hook 'mark-diary-entries-hook 'mark-included-diary-files)

Here is a sample routine that shows how to use this package.

    (defun lookout-diary-test ()
      "Test routine -- Don't call this! Just look."
      (interactive)
      (lookout-create-diary "~/kalender.csv"
    	                    "~/tmp/my-csv-diary"
    			    t)
      (save-buffer))

There is a similar command for importing address data into the Big
Brother Data Base: `lookout-create-bbdb`.  However, it has not been
tested very much.  It should not delete or modify existing BBDB
entries, but it will add lots of new user fields, one for each
column in the input CSV file.  Be careful!


## Requirements:

In order to use this package you must have installed `csv.el`, at least
version 2.0.

BBDB import requires BBDB 2.35 (or later).
