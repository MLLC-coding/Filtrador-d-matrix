**Filtrador de matrix 2**

Filtrador de matrix is a lightweight Python script built with pandas.
It takes a list of strings (**L**) and filters the rows of a target matrix (**T**) by matching the elements in the first column of the matrix.

The script automatically ignores the header (title) of both the list and the target matrix.

**Example use case**:
Extract the interactions of a specific set of genes expressed in Experiment A from a large matrix containing all genome-wide miRNA–gene interactions.
In this example, the first column of the matrix contains gene IDs, and the list file provides the subset of gene IDs of interest.
