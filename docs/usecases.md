## MassQL Query for Organophosphate Compounds in the Environment

**Author/s:** Nina Zhao

### MassQL Query

```
QUERY scansum(MS2DATA) WHERE MS2PROD=98.9847:TOLERANCEPPM=50:INTENSITYPERCENT=50 FILTER MS2PROD=98.9847
```

### MassQL Translation

Returning the summed scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 peak at m/z 98.9847 with a 50.0 PPM tolerance and a minimum percent intensity relative to base peak of 50.0%.
- Finding MS2 peak at m/z 98.9847.

### MassQL Query Link

[MassQL Query Link](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=e3504aff6ee14a619b19a3ffa3625fb6)

### Additional Data Analysis

#### GNPS MS/MS Library Search

[GNPS MS/MS Library Search](https://gnps.ucsd.edu/ProteoSAFe/status.jsp?task=1b0382c15423412cba012ed4162d1ebf)

#### Data Availability

MSV000087187

### Background

Organophosphate esters (OPEs) are widely used as flame retardants and plasticizers in consumer and industrial products. The environmental hazard of OPEs is of concern due to their increasing usage as the replacements of traditional brominated flame retardants and their toxicity effects, which include fecundity decrease, thyroid endocrine disruption, and developmental toxicity in fish. Most of the environmental investigations on OPEs employ targeted analysis with mass spectrometry, but recent studies utilizing non-targeted mass spectrometry have revealed novel OPEs. Therefore, screening strategies for OPEs in environmental samples are needed.

OPEs have the general structure O=P(OR)3, a central phosphate group with three alkyl or aromatic moieties. Previous studies have reported the phosphate ion (H4O4P+, m/z 98.9842) as the diagnostic fragment of this class of chemicals. We previously identified several OPEs in the marine water samples from Puget Sound. Here, we used MassQL to search for the phosphate ion fragment in the same dataset.

### Results

MassQL returned 771 spectra hits; among them, ~22% (182, belonging to 4 major precursors m/z) were noise spectra which required further filters on percent of total intensity to be ruled out. The rest of the spectra hits (589) belong to ~60 unique molecular features and show a true fragment of m/z 98.98. A subsequent library search identified four OPEs: tributyl phosphate, tris(chloroethyl) phosphate, tris(chloroisopropyl) phosphate, and tris(butoxyethyl) phosphate, explaining ~56% (331) of the non-noise spectra hits. Tributyl phosphate was not identified in our original publication based on traditional fold-change non-targeted analysis. This example demonstrated the possibility to screen for environmental contaminants in MS data without a predefined suspect list.


## MassQL Query for Organophosphate Compounds in the Environment at Data Repository Scale

**Author/s:** Nina Zhao

### MassQL Query

```
QUERY scansum(MS2DATA) WHERE MS2PROD=98.9847:TOLERANCEPPM=50:INTENSITYPERCENT=50 FILTER MS2PROD=98.9847
```

### MassQL Translation

Returning the summed scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 peak at m/z 98.9847 with a 50.0 PPM tolerance and a minimum percent intensity relative to base peak of 50.0%.
- Finding MS2 peak at m/z 98.9847.

### MassQL Query Link (repository-scale)

[MassQL Query Link](https://proteomics2.ucsd.edu/ProteoSAFe/result.jsp?task=f5094e83a4f042e88f0d423dcb52b11c&view=extract_results)

### Additional Data Analysis

#### Falcon Cluster, EPS = 0.3

[Falcon Cluster](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=f1a4a4c3496645e8b643f8d41c601d03)

#### GNPS Molecular Networking

[GNPS Molecular Networking](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=cf943d6808ed4d7da441184f531a62c3)

#### Data Availability

All public data from Q Exactive on GNPS

### Background

To discover novel organophosphate compounds, we ran the phosphate ion MassQL query developed in Use Case 1.1.1 over all Q Exactive data on the GNPS repository. The MassQL query returned 338,439 spectra hits in total. Based on a comprehensive list of organophosphate compounds (n = 95) compiled by Ye et al. (2021), only 15% (51,310) of the spectra hits could be explained by these known organophosphate compounds (based on precursor m/z match with 20 ppm mass error). Top matches included tris(chloropropyl) phosphate (31,039 matches), tributyl phosphate and isomers (12,967 matches), tri(2-ethylhexyl) phosphate (or structural isomers; 3511 matches), and triethyl phosphate (2171 matches). The remaining 85% matches represent a candidate pool for new organophosphate compounds.

### Results

We further analyzed the query results using molecular networking. MS-Cluster, the clustering tool for classical molecular networking on GNPS, failed to handle such a large amount of spectra and returned many repetitive clusters. We explored a newly developed clustering tool, Falcon, which very effectively reduced the number of repetitive clusters. Sending the Falcon output to molecular networking returned 169 spectra families. Mining into these spectra families led to new compound identification. For example, SI Figure 1.1.2 - 1a demonstrated a spectra family of organophosphate compounds with alkyl substituents. The m/z 267.17 represented tributyl phosphate with dimers at m/z 533.34, and the m/z 435.36 represented trioctyl phosphate (or structural isomers) with dimers at m/z 869.71 and trimers at m/z 1305.07. Notably, the group of m/z 211.03 matched the molar mass of dibutyl phosphate, which was not discovered by library search. SI Figure 1.1.2 - 1b demonstrated a spectra family of chlorinated organophosphate compounds. The m/z 428.89 matched tris(dichloro-propyl) phosphate, and m/z 327.01 matched tris(chloro-propryl) phosphate compounds. Such findings highlighted the capacity of MassQL coupled to classical molecular networking to connect related chemicals on a repository scale and to identify new chemicals.


TODO: Insert figures


## Detection of Fusaricidin Depsipeptides in Microbial Extracts

**Author/s:** Osama G. Mohamed and Ashootosh Tripathi

### MassQL Query

QUERY scaninfo(MS2DATA) WHERE 
MS2NL=255.23: TOLERANCEMZ=0.02 AND MS2PROD=256.23:TOLERANCEMZ=0.02

### MassQL Translation

Returning the scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 neutral loss peak at m/z 255.23 with a 0.02 m/z tolerance.
- Finding MS2 peak at m/z 256.23 with a 0.02 m/z tolerance.

### MassQL Query Link

[MassQL Query Link](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=3afe33c186a44bfe945a74d21c06f51e)

### MassQL Query Link (large scale)

[MassQL Query Link (large scale)](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=7fc6e39e34f84a159cb171b31ca03b09)

### Additional Data Analysis

#### GNPS Molecular Networking

[GNPS Molecular Networking](https://gnps.ucsd.edu/ProteoSAFe/status.jsp?task=9ef11868efa94bde892d27101bb579a4)

### Background

Fusaricidins are a class of cyclic lipopeptides isolated from _Paenibacillus_ sp. Their structures consist of two moieties, a cyclic polypeptide that consists of six amino acids and a guanidino-3-hydroxypentadecanoic acid fatty acid moiety (GHPD). This class of metabolites has shown in vitro antimicrobial activity against Gram-positive bacteria and _Fusarium_ fungi. Fusaricidins MS2 fragmentation spectra are characterized with the fragment product ion m/z 256.2389 (GHPD) and neutral loss of 255.23 (residual cyclopeptide moiety, MH-GHPD) (SI Figure 1.2 - 1).

The use of MassQL enabled us to quickly detect and group fusaricidins in a microbial extract. The current resources of University of Michigan Natural Products Discovery Core (UM-NPDC) include a library of over 50,000 natural product extracts (NPE) collected and curated from across the world, including Costa Rica, Papua New Guinea, Israel, Nepal, Panama, Peru, and the United States. To date, approximately 3000 NPEs have been chemically profiled using UHPLC-qTOF, and the collection is still growing. This tool can foster the discovery process of new congeners of interesting metabolites with characteristic tandem MS spectra.


TODO: Insert figure

## Impact of Leishmania major Infection on Glycerophosphocholine Lipids

**Author/s:** Laura-Isobel McCall

### MassQL Query

QUERY scaninfo(MS2DATA) WHERE 
MS2PROD=184.0739:TOLERANCEMZ=0.01:INTENSITYPERCENT=30:INTENSITYVALUE=500 AND 
MS2PROD=125.0004:TOLERANCEMZ=0.01:INTENSITYPERCENT=10:INTENSITYVALUE=1500 AND 
MS2PROD=104.1075:TOLERANCEMZ=0.01 AND 
MS2PROD=86.09697:TOLERANCEMZ=0.01:INTENSITYPERCENT=10:INTENSITYVALUE=2000

### MassQL Translation

Returning the scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 peak at m/z 184.0739 with a 0.01 m/z tolerance, a minimum percent intensity relative to base peak of 30.0%, and a minimum intensity value of 500.0.
- Finding MS2 peak at m/z 125.0004 with a 0.01 m/z tolerance, a minimum percent intensity relative to base peak of 10.0%, and a minimum intensity value of 1500.0.
- Finding MS2 peak at m/z 104.1075 with a 0.01 m/z tolerance.
- Finding MS2 peak at m/z 86.09697 with a 0.01 m/z tolerance, a minimum percent intensity relative to base peak of 10.0%, and a minimum intensity value of 2000.0.

### MassQL Query Link

[MassQL Query Link](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=abb71fc649a945fc950ad7fd684eefeb)

### Additional Data Analysis

#### GNPS Feature-based Molecular Networking

[GNPS Feature-based Molecular Networking](https://gnps.ucsd.edu/ProteoSAFe/status.jsp?task=451754c383de461e9e4abdf6eb3199d2)

#### Data Availability

MSV000081004

### Background

Current treatments for neglected parasitic diseases suffer from low efficacy, high rates of adverse effects, and emergence of drug resistance. Identifying metabolic pathways altered by infection in vivo may lead to the discovery of new antiparasitic treatment strategies, which are sorely needed. Studies of infection-modulated metabolites have revealed infection-induced metabolic perturbations in multiple members of the glycerophosphocholine family of phospholipids, necessitating a detailed investigation of this family of metabolites under infection conditions.

Glycerophosphocholines have four diagnostic MS2 fragmentation peaks in positive mode: m/z 184.0739 (phosphocholine), m/z 125.0004 (2,2-Dihydroxy-1,3,2-dioxaphospholan-2-ium), m/z 104.1075 (choline), and m/z 86.09697 (N,N,N-Trimethylethenaminium) from the phospholipid head group. We therefore built a MassQL query to search a dataset of _Leishmania major_-infected and uninfected mouse ear tissue.

### Results

The MassQL query returned all of the glycerophosphocholines that had previously been annotated via molecular networking and manually inspected for the presence of the four MS2 glycerophosphocholine diagnostic peaks. Prior manual analysis had taken over 4 hours, whereas the MassQL run took 2.5 minutes, followed by approximately 15 minutes of results exploration. In addition, this query returned four more features (m/z 518.3235 retention time 203.635 sec, m/z 552.3299 retention time 172.307 sec, m/z 600.403 retention time 224.992 sec, and m/z 768.5895 retention time 366.716 sec). Using LIPIDMAPS and based on precursor mass, we annotate m/z 518.3235 as LPC 18:3, m/z 552.3299 as PC 19:0, m/z 600.403 as LPC 24:4, LPC O-24:5;O or PC O-24:4, and m/z 768.5895 as PC O-36:4. These features had been missed in our prior analyses because they were singleton network nodes and had not returned a library match using our prior networking parameters.


TODO: Insert Figure

## Metabolism of Antibiotic Trimethoprim by Burkholderia cenocepacia

**Author/s:** Neha Garg and Andrew McAvoy

### MassQL Query

QUERY scaninfo(MS2DATA) WHERE 
MS2PROD=291.1458 AND MS2PROD=123.0665

### MassQL Translation

Returning the scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 peak at m/z 291.1458.
- Finding MS2 peak at m/z 123.0665.

### MassQL Query Link

[MassQL Query Link](https://proteomics2.ucsd.edu/ProteoSAFe/result.jsp?task=db21c5c316034b09a74668b53828b39b&view=query_results)

### Additional Data Analysis

#### GNPS Feature-based Molecular Networking

[GNPS Feature-based Molecular Networking](https://gnps.ucsd.edu/ProteoSAFe/status.jsp?task=451754c383de461e9e4abdf6eb3199d2)

#### Data Availability

MSV000084945

### Background

Trimethoprim, when combined with sulfamethoxazole, is a bactericidal antibiotic used by clinicians to treat bacterial infections, such as those caused by _Burkholderia cepacia_ complex (Bcc) bacteria in cystic fibrosis patients. _Burkholderia_ spp. are well known for their ability to metabolize xenobiotic compounds. In a previous untargeted metabolomics study, we cultured Bcc bacteria in the presence and absence of trimethoprim. In MS/MS, trimethoprim features a prominent peak with m/z 123.0665 generated by cleavage of a carbon-carbon bond of the methylene connecting the two rings, yielding the 2,4-diaminopyrimidin-5-yl-methylium fragment ion (SI Figure 1.4 - 1). With MassQL, we were able to identify spectra containing fragment masses corresponding to trimethoprim (m/z 291.1452) and the 2,4-diaminopyrimidin-5-yl-methylium fragment, allowing us to mine our dataset for metabolomic features that correspond to novel biotransformation products of trimethoprim.

### Results

This MassQL query returned a list of metabolites which display an MS2 fragmentation pattern indicative of a trimethoprim substructure, facilitating the identification of trimethoprim biotransformation products. Manual inspection revealed that 33 out of the 47 candidate features truly contained a trimethoprim substructure, which can undoubtedly be improved by optimizing the query. Previously, we relied on MS2LDA to find compounds containing a trimethoprim substructure, which involves extracting Mass2Motifs from data, manually inspecting the Mass2Motifs found in trimethoprim, and searching for all other molecules which contain relevant Mass2Motifs. MassQL provided additional flexibility to refine the Mass2Motif pattern. Notably, the MassQL query correctly identified a molecule with m/z 549.129 as containing a trimethoprim substructure, which was not recognized by MS2LDA analysis. Although manual inspection of raw data should always be performed to verify in silico predictions, MassQL has the potential to greatly streamline metabolomic analysis in a manner that can be creatively applied based on the unique analysis needs of a particular dataset.

TODO: Insert Figure

## Investigating Cannabidiol Degradation Products using MassQL 

**Author/s:** Matthew J. Bertin and Riley D. Kirk

### MassQL Query

QUERY scaninfo(MS2DATA) WHERE 
MS2PROD=259.5:TOLERANCEMZ=0.5

### MassQL Translation

Returning the scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 peak at m/z 259.5 with a 0.5 m/z tolerance.

### MassQL Query Links

- **Day 1:** [MassQL Query Link (day 1)](https://proteomics2.ucsd.edu/ProteoSAFe/result.jsp?task=d9c7673620b54e58a15f967334a5024d&view=query_results)
- **Day 4:** [MassQL Query Link (day 4)](https://proteomics2.ucsd.edu/ProteoSAFe/result.jsp?task=c80fcbe42f7048678c66ca379487f53a&view=query_results)

### Additional Data Analysis

#### GNPS Molecular Networking

- **Day 1:** [GNPS Molecular Networking (day 1)](https://gnps.ucsd.edu/ProteoSAFe/status.jsp?task=432b9dff5ef143b69b719ef42a41d9d2)
- **Day 4:** [GNPS Molecular Networking (day 4)](https://gnps.ucsd.edu/ProteoSAFe/status.jsp?task=bd728f3e31ac447384118dc3003cba01)

### Background

Cannabidiol (CBD) is a major phytocannabinoid found in Cannabis plants. The use of CBD continues to gain interest in the pharmaceutical, nutraceutical, and even the cosmeceutical industries. Detection and annotation of cannabidiol degradation products remain important for understanding the stability and quality of the now numerous CBD products available to the public. This understanding is especially critical with recent research demonstrating the biological activity (inhibition of topoisomerase II⍺ and β) of an oxidized cannabidiol quinone (CBDQ). 

### Methods

We analyzed purified CBD at two time periods (t = 0 d and t = 4 d) following exposure to natural light. The clear solution on day 0 began to take on a pale yellow color by day 4. LC-MS/MS data were acquired in data-dependent mode using a Thermo Scientific LTQ XL. We utilized mass query language to identify product ion m/z 259, a prominent fragment ion from cannabinoid precursors. We subsequently subjected each query analysis to molecular networking and examined the changes in chemical space over time.

### Results

At day 0, eight unique precursor m/z values were identified with the m/z 259 product ion. By day 4, over fifty unique precursor m/z values were identified, including a putative identification of CBD quinone (m/z 329), and many other likely degradation products. This approach shows an effective means to mine mass spectrometry data to identify potential CBD degradation molecules for quality control as more and more consumers utilize these products.

TODO: INsert figure

## Finding Drug Metabolites from Public Fecal Datasets

**Author/s:** Kyo Bin Kang

### MassQL Query

QUERY scaninfo(MS2DATA) WHERE 
MS2PROD=311.1508:TOLERANCEMZ=0.0025:INTENSITYPERCENT>5

### MassQL Translation

Returning the scan information on MS2.  
The following conditions are applied to find scans in the mass spec data:

- Finding MS2 peak at m/z 311.1508 with a 0.0025 m/z tolerance and a minimum percent intensity relative to base peak of 5.0%.

### MassQL Query Link

[MassQL Query Link](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=45b72be5b8e54d0d92959ec57f4f4558)

### Additional Data Analysis

N/A

### Data Availability

MSV000080673 and MSV000082221

### Background

In a previous study, we identified 68 putative metabolites of sildenafil by applying molecular networking analysis on LC-MS/MS data of in vitro microsomal biotransformation experiments. The MASST search of these spectra revealed that at least four public datasets (all the data were human fecal extracts) contained intact sildenafil or its major metabolite of m/z 449.1971. However, other metabolites were not found in the MASST analysis. Further investigation revealed that the matched data actually contained other metabolites, but they were not detected due to the low cosine similarity, which was mainly caused by significantly different ion intensities of fragment ions.

### Methods

We queried a common fragment of sildenafil metabolites, m/z 311.1508, and this query revealed the occurrence of other sildenafil metabolites in four matched datasets. We found 150 MS/MS scans containing a fragment ion of m/z 311.1508 from four public fecal extract data files. Some of these were identified as sildenafil metabolites in our previous study by comparing their spectra with the experimental spectra acquired in our in vitro work.

### Results

In the previous study, we discussed that these metabolites were not found in the MASST search because they showed low cosine similarity to the experimental spectra due to the different relative intensities between fragments. By visualizing extracted ion chromatograms (EICs) of identified metabolites and manually comparing m/z values of major fragment ions, we successfully found drug metabolites with the characteristic fragment ion using MassQL. This demonstrates that we can find drug metabolites from public datasets more easily even when their MS/MS spectra show low cosine similarity to our reference spectra.

TODO: Insert figure