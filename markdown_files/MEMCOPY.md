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


## [_MEMCOPY](MEMCOPY.md) [📖](https://qb64phoenix.com/qb64wiki/index.php/_MEMCOPY)
---
<blockquote>

### The _MEMCOPY statement copies a block of bytes from one memory offset to another offset in memory.

</blockquote>

#### SYNTAX

<blockquote>

`_MEMCOPY sourceBlock , sourceBlock.OFFSET , sourceBlock.SIZE TO destBlock , destBlock.OFFSET`

</blockquote>

#### PARAMETERS

<blockquote>


* sourceBlock is the source memory block name created [AS](AS.md) _MEM .
* sourceBlock.OFFSET is the dot _OFFSET within the source memory block to read from.
* sourceBlock.SIZE is the total number of bytes to transfer based on actual size.
* destBlock is the destination _MEM memory block name to transfer data to.
* destBlock.OFFSET is the dot _OFFSET within the dest _MEM memory block to write to.
</blockquote>

#### DESCRIPTION

<blockquote>


* The dot [OFFSET](OFFSET.md) is the memory block's start location in memory. Add bytes to place data further into the block.
* The dot SIZE is the total byte size of the memory block to transfer. You can transfer all or a portion of the data bytes.
* The memory block regions may overlap.
* Always free memory blocks after values have been transferred to variables and are no longer required.

</blockquote>

#### EXAMPLES

<blockquote>



##### Example: Swapping data from one STRING variable to another. Fixed length strings are recommended for speed.
```vb
DIM m AS _MEM
DIM n AS _MEM

m = _MEMNEW(10)
n = _MEMNEW(100)

_MEMPUT m, m.OFFSET, "1234567890"

s$ = SPACE$(10) 'to load into a variable length string set its length first
_MEMGET m, m.OFFSET, s$
PRINT "in:[" + s$ + "]"

_MEMCOPY m, m.OFFSET, m.SIZE TO n, n.OFFSET 'put m into n

b$ = SPACE$(10)
_MEMGET n, n.OFFSET, b$
PRINT "out:[" + b$ + "]"
_MEMFREE m: _MEMFREE n 'always clear the memory when done
```
  
<br>

```vb
'copy array a to array b one index at a time:
FOR i1 = 0 TO 100
   FOR i2 = 0 TO 100
       b(i1, i2) = a(i1, i2)
   NEXT
NEXT

'copy array a to array b in memory instantly:
DIM ma AS _MEM: ma = _MEM(a()) 'place array data into blocks
DIM mb AS _MEM: mb = _MEM(b())
_MEMCOPY ma, ma.OFFSET, ma.SIZE TO mb, mb.OFFSET
_MEMFREE ma: _MEMFREE mb 'clear the memory when done
```
  
<br>


</blockquote>

#### SEE ALSO

<blockquote>


* _MEM , _MEM (function)
* _MEMNEW , _MEMGET (function)
* _MEMIMAGE , _MEMELEMENT
* _MEMGET , _MEMPUT
* _MEMFILL , _MEMFREE
</blockquote>
