MOLECULE COMPLEXITY SORTER

A web application for sorting and filtering molecules by synthetic complexity.
Accepts CSV files with SMILES codes and molecular properties.

================================================================================
REQUIREMENTS
================================================================================

- Node.js v14+
- React
- lucide-react

Install with: npm install react lucide-react

================================================================================
CSV FORMAT
================================================================================

First row must be headers. Second column must contain SMILES codes.

Example:
Name,SMILES,MolecularWeight,LogP
Aspirin,CC(=O)Oc1ccccc1C(=O)O,180.16,1.19
Caffeine,CN1C=NC2=C1C(=O)N(C(=O)N2C)C,194.19,-0.07

================================================================================
COMPLEXITY CALCULATION
================================================================================

Complexity score is calculated from SMILES structure:

Character length × 0.5
Ring systems (digits) × 5
Branches (parentheses) × 3
Stereocenters (@) × 4
Aromatic atoms (lowercase) × 2
Heteroatoms (N,O,S,P) × 1.5
Double bonds (=) × 1.5
Triple bonds (#) × 2

Higher scores indicate more complex synthesis.

================================================================================
USAGE
================================================================================

Upload CSV File
---------------
Click upload area or drag file. Application parses data and calculates
complexity scores automatically.

Filtering
---------
Click "Add Filter" to create a new filter.
Enter column name (use autocomplete for available columns).
Select operator: > < = !=
Enter value to compare against.
Use "complexity" as column name to filter by calculated scores.
Click X to remove a filter.

Multiple filters work together. All conditions must be met.

Sorting
-------
Click any column header to sort by that column.
Click again to reverse order.
Default sort is by complexity, descending.

================================================================================
EXAMPLES
================================================================================

Find molecules with complexity above 50:
Column: complexity
Operator: >
Value: 50

Find molecules with molecular weight below 200:
Column: MolecularWeight
Operator: <
Value: 200

Find specific molecule:
Column: Name
Operator: =
Value: Aspirin

Exclude molecules with LogP of 0:
Column: LogP
Operator: !=
Value: 0

================================================================================
NOTES
================================================================================

- All processing happens in browser, no server upload
- SMILES must be in second column (column index 1)
- Empty SMILES entries get complexity score of 0
- Column names are case-sensitive for filtering
- Numeric comparisons only work on numeric columns
- Performance may degrade with >1000 rows

================================================================================
SMILES NOTATION
================================================================================

C = carbon
c = aromatic carbon
N, O, S, P = heteroatoms
= = double bond
# = triple bond
() = branches
digits = ring closures
@ = stereochemistry

Example: CC(=O)Oc1ccccc1C(=O)O is aspirin

================================================================================
TROUBLESHOOTING
================================================================================

"CSV must have at least a header row and one data row"
- Check file has minimum 2 rows
- Remove empty rows

Complexity scores show as 0
- Verify SMILES are in column 2
- Check SMILES strings are not empty

Filters not working
- Verify column name matches header exactly
- For numeric filters, ensure column contains numbers

File won't upload
- Confirm .csv extension
- Check file uses comma delimiters
- Open in text editor to verify format