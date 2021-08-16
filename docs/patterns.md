This page includes common patterns that you might want to query for in mass spec data

---

# Query Mass Spectrometry Data

### MS1 precursor ion/s based on monoisotopic mass with absolute mass error
Finding MS1 peak at m/z 256.1696 with a 0.01 m/z tolerance.
```
QUERY scaninfo(MS1DATA) WHERE 
MS1MZ=256.1696:TOLERANCEMZ=0.01
```

### MS1 precursor ion/s based on monoisotopic mass with relative mass error
Finding MS1 peak at m/z 256.1696 with a 5.0 ppm tolerance.
```
QUERY scaninfo(MS1DATA) WHERE 
MS1MZ=256.1696:TOLERANCEPPM=5
```

### MS1 precursor ion/s based on monoisotopic mass and isotope mass with relative mass error
Finding MS1 peak at m/z 256.1696<br>
Finding MS1 peak at m/z 258.1656 with a 5.0 PPM tolerance.<br>
*example: monoisotopic mass + 1.996 for 34S
```
QUERY scaninfo(MS1DATA) WHERE
MS1MZ=256.1696 AND
MS1MZ=258.1656:TOLERANCEPPM=5
```

### MS1 precursor ion/s with 34S isotope pattern
Finding MS1 peak at m/z X.<br>
Finding MS1 peak at m/z X+1.996 with a 5.0 PPM tolerance.
```
QUERY scaninfo(MS1DATA) WHERE 
MS1MZ=X AND
MS1MZ=X+1.996:TOLERANCEPPM=5
```

### MS2 spectrum with product ion with absolute mass error
Finding MS2 peak at m/z 167.0857 with a 0.01 m/z tolerance.
```
QUERY scaninfo(MS2DATA) WHERE
MS2PROD=167.0857:TOLERANCEMZ=0.01
```

### MS2 spectrum with product ion with relative mass error
Finding MS2 peak at m/z 167.0857 with a 5.0 ppm tolerance.
```
QUERY scaninfo(MS2DATA) WHERE
MS2PROD=167.0857:TOLERANCEPPM=5
```

### MS2 spectrum with multiple product ions with relative mass error
Finding MS2 neutral loss peak at m/z 176.0321.<br>
Finding MS2 peak at m/z 85.02915 a 5.0 PPM tolerance.
```
QUERY scaninfo(MS2DATA) WHERE
MS2NL=176.0321 AND
MS2PROD=85.02915:TOLERANCEPPM=5
```

### MS1 scan associated with MS2 spectrum containing a product ion with absolute mass error
Finding MS1 scan associated with MS2 spectrum - relevant to data-dependent acquisition experiments
```
QUERY MS1DATA WHERE
MS2PROD=167.0857:TOLERANCEPPM=5
```

---

# Query Liquid/Gas Chromatography - Mass Spectrometry Data

### Total ion chromatogram
Returning the summed scan information on MS1.
```
QUERY scansum(MS1DATA)
```

### Extracted ion chromatogram
```
QUERY scansum(MS1DATA) FILTER
MS1MZ=256.1696:TOLERANCEPPM=5
```

---

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

