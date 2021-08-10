

## What is Mass Spec Query Language

The Mass Spec Query Langauge (MassQL) is a domain specific language meant to be a succinct way to 
express a query in a mass spectrometry centric fashion. It is inspired by SQL, 
but it attempts to bake in assumptions of mass spectrometry to make querying much more
natural for mass spectrometry users. Broadly we attempt to design it according to several principles:

1. Expressiveness - Capture complex mass spectrometry patterns that the community would like to look for
1. Precision - Exactly prescribe how to find data without ambiguity
1. Relatively Natural - MassQL should be relatively easy to read and write and even use as a way to communicate ideas about mass spectrometry, you know like a language. 

## Developers

Mingxun Wang is the creator and main developer of MassQL. Please contact me if you have questions! I'm hoping this becomes a community effort so reach out if you want to help/use MassQL. 

## Definition of a Query

There are several parts

```
QUERY
<Type of Data>
WHERE
<Condition>
AND
<Condition>
FILTER
<Filter>
AND
<Filter>
```

### Type of Data

This determines the type of data you want to get. At its most fundamental level, its the peaks
for either 

1. MS1DATA
1. MS2DATA

Further, there are functions that can modify this data

1. scaninfo - This provides likely the most information you'd want for each scan
1. scansum - Summation of the scan
1. scannum - Returns the scan number 


!!! info "Experimental Functions"
    1. scanrangesum
    1. scanmaxint
    1. scanmaxmz
    1. scanrun


### Conditionals

These are conditions to filter for scans of interest (by looking for peaks and sets of peaks) within the mass spectrometry data. You can create clauses, 
which are specific conditions and the associated qualifiers. You may further combine multiple conditions with AND operators. 

!!! info
    The syntax for this is ```<condition>=<value>```, e.g. ```MS2PROD=144.1```.

The types of conditions are as follows

#### RTMIN

Setting the minimum retention time in minutes
#### RTMAX

Setting the maximum retention time in minutes

#### SCANMIN

Setting the minimum scan number (this is inclusive)

#### SCANMAX

Setting the maximum scan number (this is inclusive)

#### CHARGE

Finding MS2 spectra with a given charge if reported by the instrument

#### POLARITY

The polarity that will be chosen. (Positive, Negative)

#### MS2PROD

Looking for an MS2 peak

#### MS2PREC

Looking for an MS2 precursor m/z

#### MS2NL

Looking for a neutral loss from precursor in the MS2 spectrum

### Qualifiers

These can be attached to conditions to modify some properties about the peaks we are looking for. 

#### Mass Accuracy

These two fields enable setting a peak m/z tolerance

```
TOLERANCEMZ=0.1
TOLERANCEPPM=50
```

#### Intensity Relative to Full Spectrum

These two fields enable to set an minimum intensity

```
INTENSITYVALUE=1000
INTENSITYPERCENT=10
INTENSITYTICPERCENT=10
```

INTENSITYVALUE - This indicates a minimum intensity value in terms of arbitrary units.
INTENSITYPERCENT - This indicates a minimum percent of maximum peak in the spectrum.
INTENSITYTICPERCENT - This indicates a minimum percent of total TIC in the spectra. 

#### Intensity Relative to Other Peaks

Here we can start imposing relative intensities between peaks

```
INTENSITYMATCHREFERENCE
INTENSITYMATCH=Y
INTENSITYMATCH=Y*2
INTENSITYMATCHPERCENT=10
```

!!! info "Intensity Matching Between Peaks"
    This is actually complicated, but you'll end up with one peak per variable that is the reference
    and all others are relative to that reference. 
    ```
    WHERE 
    MS1MZ=X:INTENSITYMATCH=Y:INTENSITYMATCHREFERENCE # This is the reference peak which all other peaks' intensities will be compared to
    AND 
    MS1MZ=X+2:INTENSITYMATCH=Y*2:INTENSITYMATCHPERCENT=1 # The Y*2 denotes that it must be 2 times the intensity of the first peak
    ```

### Values of Conditions, Qualifiers

As mentioned above, the value of certain conditions can be numbers (more precisely floats). However, its sometimes in convenient to have to actually calculate out the m/z for an MS2PROD condition and also the derivation is obfuscated if its just a single number. You can simply list it out as a numerical expression

```
MS2PROD=100+14
```

and this will get calculated to mean

```
MS2PROD=114
```

You can even do more advanced things that are native to chemistry/biochemistry without having to look up numbers, and they are listed below

#### Molecular Formula

To save us all a little bit of time convert lookup of formulas into masses, you can use the syntax:

```
MS2PROD=formula(H2O)
```

to easily calcualte the mono isotopic mass of H2O. It will substitute as

```
MS2PROD=18.01056468403
```

!!! info "Advanced Usage"
    If you want to make functions out of formula masses, you totally can, like below

    ```
    MS2PROD=100 + formula(CH2)*2
    ```

#### Amino Acid Masses

To calculate amino acid masses, you can use the following syntax

```
MS2PROD=100 + aminoaciddelta(G)
```

which will calculate out to 

```
MS2PROD=157.02146372057
```

!!! note "Multiple Amino Acids"
    If you want to use multiple amino acids, no problem:

    ```
    MS2PROD=aminoaciddelta(GA)
    ```

#### Peptide Masses

If you're in the proteomics camp, you can automatically calculate peptide fragementation. 

```
MS2PROD=peptide(G, charge=1, ion=y)
```

will yield

```
MS2PROD=76.03930487103999
```



### Filters

Filters are like conditional but we don't elimate scans based on the condition. Rather, we simply filter out peaks within the spectra. 

This is useful for things like SRM or SIM/XIC. 

## MassQL Patterns

If you're interested in doing some more advanced queries in MassQL, we have a dedicated patterns page to show you 
ways we've approached some interesting applications. By no means is it comprehensive, but we hope it helps. Check it out [here](patterns.md).

## Examples

### XIC Generation

MS1 XIC, m/z = 100

```
QUERY scansum(MS1DATA) FILTER MS1MZ=100:TOLERANCEMZ=0.1
```

### MS2 With Sugar Loss - Neutral Loss Scan

Neutral Loss, 163 Da

```
QUERY scaninfo(MS2DATA) WHERE MS2NL=163
```

### Brominated Compounds

```
QUERY scaninfo(MS2DATA) WHERE 
MS1MZ=X:INTENSITYMATCH=Y:INTENSITYMATCHREFERENCE 
AND MS1MZ=X+2:INTENSITYMATCH=Y:INTENSITYMATCHPERCENT=5
AND MS2PREC=X
```
### MS2 with distinct fragment(s) - Precursor Ion Scan

One Product Ion, m/z = 660.2
```
QUERY scaninfo(MS2DATA) WHERE MS2PROD=660.2:TOLERANCEMZ=0.1
```

Two Product Ions, m/z = 660.2 and 468.2
```
QUERY scaninfo(MS2DATA) WHERE MS2PROD=660.2:TOLERANCEMZ=0.1 AND MS2PROD=468.2:TOLERANCEMZ=0.1
```

## How To Use MassQL

### Python API

We have a python API that you can utilize in your own software. 

### Commandline Utility

We have a standalone script that can execute queries on single spectrum files. 

### Nextflow Workflow

We have a nextflow workflow to enable scalable queries across hundreds of thousands of mass spectrometry files. 

### ProteoSAFe Workflow

We have a proteosafe workflow that we have created that nicely integrates into GNPS - Try the beta [here](https://proteomics2.ucsd.edu/ProteoSAFe/index.jsp?params=%7B%22workflow%22%3A%20%22MSQL-NF%22%7D).

#### Workflow Details

There are several options that you probably will care about

1. Extracting found MS scans as part of output, default this is off, if you want to do downstream molecular networking - turn this on
1. If you want to run multiple queries together, you can now, just separate your queries with ```|||``` and then results from multiple queries will be merged together


### Web API

We have built out a web API for people to use, especially for parsing. 

```
https://msql.ucsd.edu/parse?query=QUERY%20MS2DATA%20WHERE%20MS1MZ=100
```

Simply put in the query as a url encoded parameter and a JSON representation of the parse is returned. 

### Interactive Web Sandbox

Checkout the interactive sandbox [here](https://msql.ucsd.edu/). 

## Debugging Your Query

I would recommend you check out the interactive sandbox listed above. One of the features here is we try to translate your MassQL query into a visualization and into English. Generally issues with queries run into problems with of misunderstanding what each condition and qualifier mean or setting your requirements a bit too strict. Both the visualization and translation to English helps with that. 