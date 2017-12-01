
emailSender is a commandline 'mailmerge' mass email sender. From a textfile containing the email's text, any words surrounded by double underscores (\_\_like\_this\_\_) are replaced by values from datafile, and then emailed. The 'to' addresses can also come from a datafile. 

emailSender is for large-scale, data-table driven, commandline or programatic email sending. 

This program relies on Mutt to actually send the email, so Mutt has to be installed. 


=== usage ===

```
emailSender
     -e emailTextFile 
     -s subjectLine 	# __aaa__ substitution fields can be used
     --from from@email.address 
     --fromName  "Mr Richard Pearse" 
     --to {colNumber|to@email.com} 
     --desc "description of email(s)"  
     [-i datafile ] 	
     [--no-DB]			# no recording in the DB at all
	 [--no-save-email]	# no copy of the email (only) into the DB  
     [--noEmailChecks]	
     [[--c1 placeHolderText] [--c4 placeHolderText] ...] 
     [[--attach fileName1.coc] [--attach fileName2.jpg] ... ]
```

=== data subsitution === 

Any of the first 9 columns of the datafile can be used. The columns in the datafile must be separated by tabs. Each column in the datafile is matched to placeholder texts (\_\_placeholder\_\_) in the email text file  any of c1 to c9. For example ```--c3 __detail_5_name__``` replaces each field \_\_detail_5_name\_\_ in the email text with data from the third (for --c3) column in the datafile. The data-file fields are 1 based (not 0)

=== attachments ===

Any number of attachments can be added, using --attach SomeFileName.doc, --attach Another.... 

=== controlling emailSender ===

If the env var 'debug' is set to 'true' (and export-ed) then 
-  the emails are sent to a test email address instead, and
-  debug messages will be printed
Type "export debug=true" at the command prompt to set this 

Unless '--no-DB' is used, the email address and a company have to ALREADY be in the master contact table ("static") for this program to run properly. Currently hardcoded to use the 'contact' database .

WARNING: this program KILLs any running (or hung) mutt instances


== TO DO ==

The database name, table name and the database field names have need to be set in a conf file rather than 'hard' coded. 


