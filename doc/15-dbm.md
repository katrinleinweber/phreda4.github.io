﻿# Memory Data Base

Library for memory database with char separators, variable length registers.

`^r4/lib/db2.txt`

Library for make form for edit, include db2.

`^r4/lib/formkit.txt`

## Database Definition

The database is a collection of records separated by the character `~`, each field is separated by the character `|` and within the field you can separate value with the character `_`, this definition is arbitrary, and you could have chosen non-printable characters but you tried to simplify to edit the files with a common text editor

See the demo in apps/database agenda.

```
#dbagenda 0 "db/agenda/agenda.db"

#fkagenda 0 "db/agenda/agenda.fk"

#gragenda 0 0
$400 $201 $202 $203 $304 0
"Nombre|Movil|Particular|Trabajo|e-mail"
```

`dbagenda` define the file for store the db, `fkagenda` define the form for entry the datas and `gragenda` define a grid for view the db.
The file `db/agenda/agenda.fk` define the field with type, for edit, and size. Remember the fields are positional, not for name, the name is decorative.

```
Agenda~
Nombre|A80~
Movil|A20|9999999999~ Particular|A20|9999999999~ Trabajo|A20|9999999999~
Email|A40~ Direccion|A40~
```

load the db and the form:

```
	mark
	'fkagenda fkload
	'dbagenda dbload
```

## Log Version

There are words for make a db with a log file, every change in the db is append to a log file id disk and you can reconstruct the entire db or make a replicate with a timestamp.

## Work with database

In lib/parse.txt you have word for select the correct field. The idea is keep the adress of register an search the next control char

```
::>>s | adr -- adr'	| go to next separator
::>>f | adr -- adr' | go to next field
::fld# | adr -- adr cnt	| cnt of fields
::>>fi | adr -- adr'	| next record
::reg# | adr -- adr cnt | count record
```

In lib/db2.txt

For traverse de database, vec is a word for operate over the register.

```
::dbmap | vec 'db -- ; vec | vec nro adri adrr -- vec nro adri | nro is from max to 0

::dbmapn | vec 'db -- ; vec | vec nro adri adrr -- vec nro adri | nro is 0 to max
```

For insert, update and delete registers. There are versions with log.

```
::dbinsert | 'db --   ; inserta memoria al final del archivo
::dbupdate | nroreg 'db --
::dbdelete | nro 'db --
```

For sort in diferents type of registers. For every db there are a index array, this word sort this index.

```
::dbsort | fld 'db -- ;
::dbsortstr | fld 'db -- ;
::dbsortdate | fld 'db --
```

For Filter, again, over the index array.

```
::dbfilterv | 'que 'db --
```

For searchany value
```
::dbsearchstr | "" nro 'db -- reg/0
::dbsearchany | "" nro 'db --  reg/0
::dbsearchnext | "" nro 'db --  reg/0
```

For example: I have a database of articles and I need to obtain the different suppliers of the articles, for this I will go through the database and get the different names of suppliers in a string arrangement.
