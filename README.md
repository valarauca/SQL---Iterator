# SQL---Iterator
I have to learn SQL at work. I know list operators, but not SQL. The goal of this document is to provide a bit of a brain dump on how these two concepts map to one another.

The list comphrension style is roughly: https://doc.rust-lang.org/std/iter/trait.Iterator.html

If you stumble across this I made it for personal reference IDFK if it's correct.


###SELECT FROM:

    SQL:
      SELECT $field FROM $table WHERE $LAMBDA
    LIST:
      table.iter()
        .filter($LAMBDA)      //filter by function
        .map($row -> $field)  //map row to a single field (or several it depends)
      
      
###INTERSECT:

Chain output of 2 statements

    SQL:
      SELECT * FROM $table WHERE $LAMBDA_0
      INTERSECT
      SELECT * FROM $table WHERE $LAMBDA_1
    List:
      table.iter()
        .filter($LAMBDA_0)
        .chain(
                table.iter()
                  .fitler($LAMBDA_1)
              )
        
###EXCEPT:

Filter a Filter

    SQL:
      SELECT * FROM $table WHERE $LAMBDA_0
      EXCEPT
      SELECT * FROM $table WHERE $LAMBDA_1
    LIST:
      table
        .iter()
        .filter($LAMBDA_0)
        .filter($LAMBDA_1)
        
        
###WITH

Define lambda functions.

    SQL
      WITH $VIEW as SELECT * FROM $LAMBDA_0
      SELECT * FROM $VIEW 
