## SQL ##
### DDL ###
Use schemas per service.
Schema names should be lower case.
Tables should start with an upper case letter.
Tables should define what they contain but not repeat information we already know from the schema name, e.g. if in the *content* schema then use Type rather than ContentType for a table name.
Column names should be camel case starting with a lower case letter.
2 letter names should use the camel case convention, e.g. somethingId rather than somethingID.
Default names are fine for index names.
Tables should all have primary keys.
Surrogate keys are fine.
Use of foreign keys is applauded.
All tables should have an orgId column.

### DML ###
Where DML isn't generated the following should apply.
Be neat.
Key words should be upper case.
Object names should follow the DDL conventions.
Keep as close to ANSI standard SQL as possible.

## Javascript ##
Be neat.
Use 2 spaces for indentation.
Lint.
Use semi colons.
Comment freely.
Use JSDoc comments for all functions.
Variables should be declared at the start of blocks.
Variables should be listed alpabetically where practical.
Variable and function names should be camel case.
Most variables and functions should start with lower case letters.