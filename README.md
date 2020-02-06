# PySpread
A tiny functional python library which leverages 'Lazy Evalutation' to emulate spreadsheet functionality. 
## How it works
PySpread's spreadsheet object is a 2D row, col, dictionary.
`spr = Spread((3,6), isZeroed=True) # Defines a spreadsheet with 3 rows and 6 cols`

Spread stores all data as functions wrapped in an FCell/Cell object inside its dictionary.
`Cell(Return(10)`
`FCell(spr, op(OP.add, [(0,0), (0,1), (0,2), (0,3)]))`

Functions that are stored within PySpread are only evaluated when they are shown to the screen.
Functions can be composed with one another using arbirary operators. This allows calcualtions to be defined but not yielded until needed.
```
add_cells_op = op(OP.add, [(0,0), (0,1), (0,2), (0,3)]) # Defines addition across several cells.
sub_cells_op = op(OP.sub, [(1,0), (1,1), (1,2), (1,3)]) # Defines subtraction across several cells.
add_and_sub_calc = opf(OP.add, [add_cells_op, sub_cells_op]) # Binds an addition between the results of these two calculations.
spr.update((2, 5), FCell(spr, add_and_sub_calc))) # Updates the cell at 2,5 with the calculations
...
spr.pp() # Calculations are finally evaluated when printing to the screen
```

### Cell/FCell
A function is wrapped in a Cell object is when it does not require an underlying datastructure to return.

If a function needs a datastructure (for example it wants to call select on a *spreadsheet*) then it is wrapped in an FCell object. FCell will curry the value specified in its constructor into its function.
`FCell(spr, op(OP.add, [(0,0), (0,1), (0,2), (0,3)])) # spr is curried into the "op" partial function`

### Whats next?
The next steps for this project are to add a tree based caching system and a frontend gui. If you find this project interesting reach out to me and we may be able to collaberate.



