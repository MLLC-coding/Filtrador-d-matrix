# Filtrador de matrix 2
Filtrador de matrix uses a list of strings as an input to filter down a matrix according availability of elements of the list L in column m of matrix. 
Expression Matrix of dataset X--(1)-->Filtered expression matrix based on L.
Filtrador de matrix is a script of pandas (python).
Use example: obtain the differentially upregulated miRNAs expression matrix out of a expression matrix of all miRNAs found. 
To run **filtrador de matrix2** on Windows, 1) create a list of genes you interested in and sabe in txt, and name it list.txt 2) save the matrix on excel separated by ";" and name it target_matrix.csv, and 3) copy and paste the following code into IDLE or any Python IDE modify the file paths accordingly:

import os
print(os.getcwd())

#filtrador de matrix
#!/usr/bin/env python
import pandas as pd
print("welcome to filtrador de matrix 2")
# Load the data matrix and the list of miRNA names
data_matrix_file = r"C:\Users\User01\Documents\target_matrix.csv" #path to target matrix
mirna_list_file = r"C:\Users\User01\Documents\list.txt" #path to list
output_file = r"C:\Users\User01\Documents\filtered_matrix.csv"  # Output file for the filtered data matrix
# Load the data matrix (assuming it's a tab-delimited file)
data_matrix = pd.read_csv(data_matrix_file, delimiter=';')  # Adjusted delimiter to ';'
# Load the list of miRNA names, skipping the first line (header)
with open(mirna_list_file, 'r') as file:
    next(file)  # Skip the first line (header)
    mirna_list = [line.strip() for line in file]
# Initialize a list to collect rows instead of concatenating DataFrames in each iteration
filtered_rows = []
# Iterate through the miRNA list and filter the data matrix
for mirna in mirna_list:
    if mirna in data_matrix.iloc[:, 0].values:  # Check if miRNA is in the first column
        print(f"\nFound string: {mirna}")
        # Append all rows that match the miRNA to the filtered list
        filtered_rows.append(data_matrix[data_matrix.iloc[:, 0] == mirna])
# Concatenate all filtered rows into a single DataFrame
if filtered_rows:
    filtered_matrix = pd.concat(filtered_rows, ignore_index=True)
else:
    filtered_matrix = pd.DataFrame(columns=data_matrix.columns)  # Empty DataFrame if no matches
# Write the filtered matrix to a CSV file
filtered_matrix.to_csv(output_file, index=False)
print(f"\nFiltered data matrix saved to {output_file}.")
