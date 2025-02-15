<style type="text/css">
body {
    background: #00a !important;
    color: #ccc !important;
}
li {
    list-style-type: square !important;
    color: #ccc !important;
}
li::marker {
    color: #77f !important;
}    
hr {
    border-color: #55f !important;
    border-width: 2px !important;
}
h2 {
    color: #fff !important;
    border: 0 !important;
}
h3 {
    color: #cfc !important;
    border: 0 !important;
}
h4 {
    color: #ccc !important;
    border: 0 !important;
}
h5 {
    margin: 0 0 0.5em 0  !important;
    color: #88f !important;
    border: 0 !important;
    font-style: italic !important;
    font-weight: normal !important;
}
code {
    background: #000 !important;
    margin: 0 !important;
    padding: 8px !important;
    border-radius: 4px !important; 
    border: 1px solid #333 !important;
}
pre > code {
    background: transparent !important;
    margin: 0 !important;
    padding: 0 !important;
    border-radius: inherit !important; 
    border: 0 !important;
}
blockquote {
    border: 0 !important;
    background: transparent !important;
    margin: 0 !important;
    padding: 0 1em !important;
}
pre {
    border-radius: 4px !important;
    background: #000 !important;
    border: 1px solid #333 !important;
    margin: 0 !important;
}
a:link, a:visited, a:hover, a:active {
    color: #ff0 !important;
}
br + pre {
    border-radius: 0 !important;
    border-style: inset !important;
    border-width: 5px !important;
    border-color: #999 !important;
    background-color: #000 !important;
    box-shadow: 0px 10px 3px rgba(0, 0, 0, 0.25) !important;
    margin-top: -1em !important;
}
br + pre::before {
    content: "OUTPUT \A" !important;
    color: #555 !important;
    border-bottom: 1px solid #333;
    font-size: x-small;
    display: block !important;
    padding: 0 3px !important;
    margin: -1em -1em 1em -1em !important;
    -webkit-user-select: none; /* Safari */
    -ms-user-select: none; /* IE 10 and IE 11 */
    user-select: none; /* Standard syntax */    
}
br ~ h5 {
    margin-top: 2em !important;
}
.explanation {
    color: #995 !important;
    /* background-color: rgba(150, 150, 100) !important; */
    border-radius: 10em !important;
    border: 2px #441 dashed !important;
    padding: 8px 32px !important;
    margin-bottom: 4em !important;
    font-size: x-small !important;
}
</style>


## [DATA](DATA.md) [📖](https://qb64phoenix.com/qb64wiki/index.php/DATA)
---
<blockquote>

### The DATA statement creates a line of fixed program information separated by commas. The DATA can be later READ by the program at runtime.

</blockquote>

#### SYNTAX

<blockquote>

`DATA [value1, value2, ...]`

</blockquote>

#### DESCRIPTION

<blockquote>


* [DATA](DATA.md) is used at the beginning of every data field line with commas separating the values that follow.
* Values can be any literal [STRING](STRING.md) or numerical type. Variables cannot be used.
* [DATA](DATA.md) fields can be placed and [READ](READ.md) consecutively in the main program code body with or without line labels for [RESTORE](RESTORE.md) .
* [DATA](DATA.md) is best placed after the main program code.
* QB64 [DATA](DATA.md) can be placed inside a [SUB](SUB.md) or [FUNCTION](FUNCTION.md) procedures.
* [RESTORE](RESTORE.md) will only read the first data field if the [DATA](DATA.md) is not labeled or no label is specified in a [RESTORE](RESTORE.md) call.
* When using multiple [DATA](DATA.md) fields, label each data field with a line label so that each data pointer can be reset for multiple reads with [RESTORE](RESTORE.md) linelabel .
* QBasic comma separations were flexible to allow column alignments when creating them. QB64 removes spacing between commas.
* [STRING](STRING.md) [DATA](DATA.md) values with end spaces, QBasic keywords and values that include the comma character must be enclosed in quotation marks.
* [DATA](DATA.md) fields can only be created by the programmer and cannot be changed by a user or lost.
* Comments after a data line require a colon before the comment.
* If a [READ](READ.md) statement attempts to read past the last data value, an "Out of Data" error will occur. Use end of data markers when necessary.
* [DATA](DATA.md) fields can be placed after [SUB](SUB.md) or [FUNCTION](FUNCTION.md) procedures, but line labels are not allowed.

</blockquote>

#### EXAMPLES

<blockquote>



##### Example 1: Creating two DATA fields that can be READ repeatedly using RESTORE with the appropriate line label.
```vb
RESTORE Database2
READ A$, B$, C$, D$         'read 4 string values from second DATA field
PRINT A$ + B$ + C$ + D$     'note that quoted strings values are spaced

RESTORE Database1
FOR i = 1 TO 18
 READ number%                     'read first DATA field 18 times only
 PRINT number%;
NEXT

END

Database1:
DATA 1, 0, 0, 1, 1, 0, 1, 1, 1
DATA 2, 0, 0, 2, 2, 0, 2, 2, 2 :       ' DATA line comments require a colon

Database2:
DATA "Hello, ", "world! ", Goodbye, work!
```
  
<br>

```vb
Hello world! Goodbyework!
1  0  0  1  1  0  1  1  1  2  0  0  2  2  0  2  2  2
```
  
<br>



##### Example 2: How to RESTORE and READ DATA in a SUB procedure in QB64. Line labels can be used for multiple DATA fields.
```vb
DIM SHARED num(10) 'shared array or must be passed as a parameter
ReadData 2 '<<<<<<< change value to 1 to read other data
FOR i = 1 TO 10
 PRINT num(i);
NEXT
END

SUB ReadData (mode)
IF mode = 1 THEN RESTORE mydata1 ELSE RESTORE mydata2
FOR i = 1 TO 10
 READ num(i)
NEXT

mydata1:
DATA 1,2,3,4,5,6,7,8,9,10
mydata2:
DATA 10,9,8,7,6,5,4,3,2,1
END SUB
```
  
<br>

```vb
10  9  8  7  6  5  4  3  2  1
```
  
<br>


</blockquote>

#### SEE ALSO

<blockquote>


* [RESTORE](RESTORE.md) . [READ](READ.md)
* [\$EMBED](\$EMBED.md) . _EMBEDDED$
* [SUB](SUB.md) , [FUNCTION](FUNCTION.md)
</blockquote>
