This page includes common patterns that you might want to query for in mass spec data

### MS2 spectra with a given MS1 isotopic pattern

If you're looking for molecules with an isotopic pattern and want to get the MS2 spectra associated with it, we have a pretty easy way to do this. 

Since you're looking for a variable m/z denoted as X, once you find it, simply enforce the MS2 precursor m/z to also be X.

!!! note
    This will cause isotopic patterns that lack MS2 to be dropped

Here is a quick example of a query

```
QUERY scaninfo(MS2DATA) WHERE 
MS1MZ=X AND 
MS1MZ=X+1 AND 
MS2PREC=X
```

