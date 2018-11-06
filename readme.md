# TexUtils
Just a collection of useful python scripts to make your tex life easier

## table.py
Automatically generates tex tables from your acquired data.
<p> IMPORTANT: You have to use the package siunitx in your .tex file if you want to import the
           generated file into your main document</p>
           
Usage:
<pre> <code>
x, y = np.genfromtxt('data.txt') # If using numpy. TexTable also accepts generic lists
table = TexTable([x, y], [r'Y / \si{\second}', r'My Y data'], label='table:mytable', caption='Description')
table.setRowRounding(0, 1) # Row given at index 0 should be rounded after 1 places
table.writeFile('myTable.tex')
</code></pre>

And in tex just include:

<pre> <code>
\begin{document}
....
\input{myTable.tex}
...
\end{document}
</code> </pre>

The TexTable takes two necessary arguments: 

1. First an array with your data rows
2. Second an array with the names the rows have

<p>Optional arguments are:</p>

- label - The label of the table
- caption - The Caption of the table
- roundPrecision - How many places should be rounded (default 2)

Set rounding options of individual rows:
use 
table.setRowRounding(rowIndex, precision)



## error.py
Generates your error formulas for gaussian error propagation in latex code and calculates your numerical
error values with the uncertainties package - all in one go.

Usage:
<pre><code>
x_error = Error('x + b * c', ('x', ufloat(10, 0.1)), ('b', ufloat(5, 0.3)), ('c', ufloat(2, 0.25))
print(x_error.getLatexError())
print(x_error.getNumericalError())
</code></pre>
