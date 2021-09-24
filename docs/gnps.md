## GNPS MassQL Workflow

You can execute your MassQL queries against your own data or public data at GNPS in a highthroughput fashion. Whether its one file or 250K, its possible at GNPS. 

Check out the workflow [here](https://proteomics2.ucsd.edu/ProteoSAFe/index.jsp?params=%7B%22workflow%22%3A%20%22MSQL-NF%22%7D).


### Input Parameters

1. Query
1. Spectrum Files
1. Paralleize within a single file - ignore this
1. Parallelize Across All Files - To increase a little bit of speed if you have multiple files, turn to Yes
1. Extract Found MS Spectra - if you want to extract the found MS spectra for networking
1. Parallelize across the Cluster - admin only

### Query

Enter your query in this field. You can simply paste one in or write it here. 

!!! note "Multiple Queries"
    If you want to run multiple queries you can separate each query with ```|||``` and all results are merged together

### Results Views

#### Query Results

You can see all query results.

#### Extraction Results

If you selected the extraction, then you can view the extracted spectra in case its not possible to view the spectra from the original query data. 

#### Molecular Networking

You can take the extracted data and create a molecular network. 

#### Falcon Clustering

You can take the extracted data and cluster the data with Falcon to create a molecular network downstream. Generally, Falcon performs better at clustering when reducing redundancy of the same precursor.

#### Library Search

You can take the extracted data and search the library.

### Troubleshooting

1. If you don't get any results, go ahead and check the "Workflow Trace" to make sure its not all failed. 
1. Checkout the interactive app to try out your query on GNPS Libraries

## Examples

### Sanity Test

[Link](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=2fd52d1d64074c70aef82658e86c77d0)
### Iron Siderophore

[Link](https://proteomics2.ucsd.edu/ProteoSAFe/status.jsp?task=d3dad0ccc388442bb2a6a7d2beb28293)