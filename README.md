# IUPAC Digitized pKa Dataset 

[![DOI](https://zenodo.org/badge/536654885.svg)](https://zenodo.org/badge/latestdoi/536654885)

**Important note: This is an early release of this dataset. The detailed process of digitization and curation of this dataset can be found in the *IUPAC pKa Data Digitization Report* attached in this repository. Our validation process is ongoing and will continue. Please be advised that a few errors and inconsistencies may still exist.** 

### Dataset version: v2.3

## Description

This repository includes "high-confidence" pKa data digitized from three reference works:
 - **Serjeant**: International Union of Pure and Applied Chemistry, E. P Serjeant and Boyd Dempsey. *Ionisation Constants of Organic Acids in Aqueous Solution*; Oxford/Pergamon, 1979 (Oxford IUPAC chemical data series)
 - **Perrin**: International Union of Pure and Applied Chemistry, DD Perrin. *Dissociation Constants of Organic Bases in Aqueous Solution*; Butterworths, 1965
 - **Perrin Supplement**: International Union of Pure and Applied Chemistry, DD Perrin. *Dissociation Constants of Organic Bases in Aqueous Solution, Supplement*;  Butterworths, 1972

With permission from the copyright holder, the International Union of Pure and Applied Chemistry (IUPAC), the reference books were scanned, converted to digital data, checked for accuracy, and curated for accessibility, interoperability, and reusability between the dates of Friday, Sept. 10, 2021 and Thursday, Sept. 15, 2022 by Jonathan Zheng (jonzheng@mit.edu). Further processing and curation was performed between Jan. 8, 2024 to Feb. 22, 2024 by Jonathan Zheng and Olivier Lafontant-Joseph (olivj23@mit.edu). Further updates were committed on: July 10th, 2024, and March 21st, 2025.

## Contributors:
Jonathan Zheng

https://orcid.org/0000-0002-4863-1325 

Green Group, Department of Chemical Engineering

Massachusetts Institute of Technology

jonzheng@mit.edu


Olivier Lafontant-Joseph

Green Group, Department of Chemical Engineering

Massachusetts Institute of Technology

olivj23@mit.edu

## License
Copyright &copy; 2025 International Union of Pure and Applied Chemistry.

This material is available for reuse under a [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) license with the following attribution: Reproduced by permission of International Union of Pure and Applied Chemistry.

## Recommended Citation
Zheng, Jonathan W. and Lafontant-Joseph, Olivier. (2025) IUPAC Digitized pKa Dataset, v2.3. Copyright &copy; 2025 International Union of Pure and Applied Chemistry (IUPAC), The dataset is reproduced by permission of IUPAC and is licensed under a [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/). Access at https://doi.org/10.5281/zenodo.7236453. 

This GitHub repository serves as a working copy for the dataset. Please refer to the Zenodo DOI badge linked at the top of this README.


## Data & File Overview

**File List**
 * `iupac_high-confidence_v2_3.csv` : pKa dataset.
 * `IUPAC_pK_DataDigitizationReport.pdf` : Report describing methods of creating this dataset.
 * `reference_code_translation.csv`: Spreadsheet containing reference codes.
 * `method_translation.csv`: Spreadsheet containing method codes.
 * `jupyter_notebooks/1_automatically_process_messy_OCR_demo.ipynb` : Jupyter notebook showing how Amazon Textract OCR output was streamlined to page.
 * `jupyter_notebooks/2_combine_and_analyze_scanned_work_serjeant.ipynb`: Jupyter notebook combining double-checked scans into one composite DataFrame, streamlining to a useful computer-readable format, and applying IUPAC to SMILES translations.
 * `jupyter_notebooks/3_further_process_data.ipynb`: Jupyter notebook combining outputs from each reference work and performing final postprocessing.
 * `jupyter_notebooks/data_sample/textbook_original_scan.pdf`: Image scan of data sample; used for Jupyter notebook demos.
 * `jupyter_notebooks/data_sample/data.csv`: Result of inputting the image scan pdf into Amazon Textract; used for Jupyter notebook demos.
 * `jupyter_notebooks/names/sample_names_OUT.csv`: Sample of IUPAC name translations following typical workflow; used for Jupyter notebook demos.

Further data was collected that is not included in this dataset. "Low-confidence" data (i.e. only one source translating IUPAC name to SMILES; or different name translators gave different results) were excluded, as well as entries whose names could not be programatically translated, and dissociation types that could not be unambiguously assigned (i.e. pKaH versus pKa). Raw scans of the reference books are also excluded from this data set.

Please email jonzheng@mit.edu or post an issue on the GitHub page if any errors are discovered.

## Methodological Information
This dataset was obtained by scanning the reference books listed above, and then using OCR (Amazon Textract) to extract the images into text. After some light processsing of the intermediate data files, scripts were then written to process the text into an organized tabular format that resembles the layout of the textbook, to aid members of the Green Group at MIT manually check the digital data for fidelity to the original reference data. The digital tables were then processed again to extract the information to a convenient form for computational use, and to attempt to translate the IUPAC names to SMILES strings. This final format was then manually and programatically checked. *More information can be found in the report attached in the repository.*

Proprietary software Amazon Textract was used to perform the OCR, and Chemaxon Molconvert was used to aid in translating IUPAC names to structures. 

Open-source software used to aid in the OCR process: `unpaper`, `OCRmyPDF`, `camelot`, `tabula`. IUPAC to SMILES translation was aided by `OPSIN`, PubChem, and the Chemical Identifier Resolver.

Sample Jupyter notebooks showing the data extraction process are included in this repository to demonstrate the processing methods. Packages `rdkit` and `pandas` are required to run the demos at minimal capacity. For extended usability, install `pubchempy`, `py2opsin`, and `cirpy` as well.

**To run the Jupyter notebooks:** Install the required prerequisite packages. Run the Jupyter notebooks in order from 1 to 3. You should not need to alter any of the scripts. If running the minimal example without `pubchempy` and `cirpy`, either comment out or skip the cells that involve those packages.

`1_automatically_process_messy_OCR_demo` takes the OCR output from Amazon Textract and organizes into human-readable tables. 

`2_combine_and_analyze_scanned_work_serjeant` takes the human-readable tables and further processes them to computer-readable tables.

`3_further_process_data` further takes the computer-readable data and performs final processing on the data, resulting in the final polished dataset format presented here.

## Quality assurance
Before publication, several programmed checks were performed on the dataset.
 * Checking range and distribution of pKa values.
 * Checking for common typos in Remarks, pKa types, temperatures, and chemical names.
 * Manual review of all entries that failed to produce a SMILES (in case the translation failure was caused by a name typo).
 * Manual review of amphoteric molecules to check the validity of the dissociation type (example: pKaH vs. pKa vs. pKb)
 * Standardizing formats (e.g. formatting "pk" as "pKa", "pKa" as "pKa1", standardizing "V. Uncert." versus "Very Uncert.", etc.).

## Data-specific information

### **Columns**:
* `unique_ID#`: A unique code for each distinct molecule in the dataset, composed of the reference work code plus the entry number of the chemical species in the original reference work.
* `SMILES`: SMILES string translated from the IUPAC names provided in the original reference work.
* `InChI`: InChI string derived from the SMILES strings
* `pka_type`: Type of dissociation constant. Examples: pKaH1 = conjugate acid's first dissociation; pKb = basic dissociation constant; The vast majority of entries will be of the form pKaH, pKa, or pKB, but there are some exceptions in the reference works that include parentheses to identify an unusual protonation site or structure, e.g. pK(indole-ring) is pK for protonation on indole ring. (This convention may be changed in a later version). Many amphoteric molecules species are also present in this dataset, for which several pK values are reported. The original reference works do not often distinguish which values are acidic and which are basic. This distinction can be automatically made if only two acidities are reported, in which case the lower value is assumed to be basic and the higher as acidic. For all entries with more than 2 pK values that are potentially amphoteric, we manually examined the chemical structures to determine the labels. Out of the original data corpus, 1,275 entries had ambiguous labels we could not manually assign, so we excluded them from the high-confidence dataset. Future work may include resolving the labels for that missing set.
* `pka_value`: the pK value
* `T`: temperature (deg. C)
* `remarks`: Comments for this specific datapoint.
* `method`: Code for the method used to determine this datapoint.
* `assessment`: IUPAC critical evaluation of the data uncertainty.
* `ref`: Code for the reference to the original source of this datapoint. 
* `ref_remarks`: Remarks pertaining specifically to the reference for this entry; e.g. "Thermodynamic quantities are derived from the results".
* `entry_remarks`: Remarks pertaining to all entries for this chemical species, usually pointers to other data sources (e.g. Other values in B10).
* `original_IUPAC_names`: IUPAC identifier for the chemical species originally presented in the reference work (with a few exceptions, see the report for details).
* `name_contributors`: The names of the methods that produced viable SMILES names from the IUPAC translation.
* `num_name_contributors`: The number of methods that yielded a successful SMILES translation.
* `original_IUPAC_nicknames`: Secondary names identified from the IUPAC identifier for the chemical species originally presented in the reference works
* `source`: Name of the reference book: perrin, perrin_supp, or serjeant .
* `pressure`: Pressure (a handful of entries include very high pressure entries which might yield unexpected results if not filtered, so this column is added to help filter these out).
* `acidity_label`: Descriptor indicating whether the pK is an acidic (A), conjugate acid (AH), basic (B), or "other" dissociation constant.
* `original_T`: Displays the original temperature if it was corrected for purposes of standardization. (In the T column, room temperature was converted to 25 degrees Celsius, and any approximate temperatures were reported without their approximation sign.)
* `cosolvent`: Solvent information, if parsable from the remarks column.

### **Rows**: 
There are 24,211 rows corresponding to 10,626 unique molecules in the dataset (unique on the basis of InChI strings).

Specialized abbreviations used: 
* `pK`: dissociation constant of any type, e.g. a pKa, pKaH, pKb, etc.
* `pKa`: acid dissociation constant
* `pKa1, pKa2, pKa3, ...`: first, second, third (etc) acid dissociation constants
* `pKaH`: acid dissociation constant of a base's conjugate acid
* `pKb`: base dissociation constant, or 14-pKAH
* `I`: ionic strength, equal to 1/2 * Sum(ci * zi^2)
* `m`: concentration in mole/1000g of water
* `c`: concentration in mole/L
* `κ`: specific conductance of water used, in 10^-6 ohm^-1 cm^-1
* `T`: temperature (usually in deg. C)
* `H0`: Hammett acidity function; other acidity functions follow a similar nomenclature e.g. H_, HR, etc.

In the case of data uncertainty, the evaluation originally posited by the authors is to used "Reliable", "Approximate", and "Uncertain" evaluations. The suggested reliability for these designations is:
* Reliable: ΔpK <= +/- 0.005
* Approximate: ΔpK <= +/- 0.04
* Uncertain: ΔpK > 0.04

## Acknowledgement
People involved with sample collection, processing, analysis and/or submission: 
- Green Group, Department of Chemical Engineering, MIT
- Ye Li, MIT Libraries
- IUPAC volunteers: Leah McEwen, Stuart Chalk
- PubChem volunteers: Evan Bolton, Jeff Zhang

[//]: # (This addition is derived from https://github.com/deepmind/mathematics_dataset/blob/master/README.md)
[//]: # (https://chrisgorgo.medium.com/making-github-hosted-datasets-discoverable-by-google-dataset-search-13527f2f657a)

## Dataset Metadata
The following table is necessary for this dataset to be indexed by 
<a href="https://datasetsearch.research.google.com">Google Dataset Search</a>.
<div itemscope itemtype="http://schema.org/Dataset">
<table>
  <tr>
    <th>property</th>
    <th>value</th>
  </tr>
  <tr>
    <td>name</td>
    <td><code itemprop="name">IUPAC Digitized pKa Dataset</code></td>
  </tr>
  <tr>
    <td>creator</td>
    <td>
      <div itemscope itemtype="http://schema.org/Person" itemprop="creator">
        <table>
          <tr>
            <th>property</th>
            <th>value</th>
          </tr>
          <tr>
            <td>name</td>
            <td><code itemprop="name">Jonathan Zheng</code></td>
          </tr>
          <tr>
            <td>sameAs</td>
            <td><code itemprop="sameAs">https://orcid.org/0000-0002-4863-1325</code></td>
          </tr>
        </table>
      </div>
      </td>
  </tr>
  <tr>
    <td>url</td>
    <td><code itemprop="url">https://github.com/IUPAC/Dissociation-Constants</code></td>
  </tr>
  <tr>
    <td>sameAs</td>
    <td><code itemprop="sameAs">https://doi.org/10.5281/zenodo.7236452</code></td>
  </tr>
  <tr>
    <td>description</td>
    <td><code itemprop="description">This repository includes "high-confidence" pKa data digitized from three reference works:<br/>
 - International Union of Pure and Applied Chemistry', E. P Serjeant and Boyd Dempsey. 'Ionisation Constants of Organic Acids in Aqueous Solution'; Oxford/Pergamon, 1979 (Oxford IUPAC chemical data series)<br/>
 - International Union of Pure and Applied Chemistry, DD Perrin. *Dissociation Constants of Organic Bases in Aqueous Solution*; Butterworths, 1965<br/>
 - International Union of Pure and Applied Chemistry, DD Perrin. *Dissociation Constants of Organic Bases in Aqueous Solution, Supplement*;  Butterworths, 1972<br/>
With permission from the copyright holder, the International Union of Pure and Applied Chemistry (IUPAC), the reference books were scanned, converted to digital data, checked for accuracy, and curated for accessibility, interoperability, and reusability between the dates of Friday, Sept. 10, 2021 and Thursday, Sept. 15, 2022 by Jonathan Zheng (jonzheng@mit.edu). Further processing and curation was performed between Jan. 8, 2024 to Feb. 22, 2024 by Jonathan Zheng and Olivier Lafontant-Joseph (olivj23@mit.edu). Further updates were committed on: July 10th, 2024, and March 21st, 2025.
</code></td>
  </tr>
  <tr>
    <td>provider</td>
    <td>
      <div itemscope itemtype="http://schema.org/Organization" itemprop="provider">
        <table>
          <tr>
            <th>property</th>
            <th>value</th>
          </tr>
          <tr>
            <td>name</td>
            <td><code itemprop="name">The International Union of Pure and Applied Chemistry (IUPAC)</code></td>
          </tr>
          <tr>
            <td>sameAs</td>
            <td><code itemprop="sameAs">https://iupac.org</code></td>
          </tr>
        </table>
      </div>
      <div itemscope itemtype="http://schema.org/Organization" itemprop="provider">
        <table>
          <tr>
            <th>property</th>
            <th>value</th>
          </tr>
          <tr>
            <td>name</td>
            <td><code itemprop="name">Green Group, Department of Chemical Engineering, Massachusetts Institute of Technology (MIT)</code></td>
          </tr>
          <tr>
            <td>sameAs</td>
            <td><code itemprop="sameAs">https://greengroup.mit.edu/</code></td>
          </tr>
        </table>
      </div>
    </td>
  </tr>
  <tr>
    <td>citation</td>
    <td><code itemprop="citation">https://doi.org/10.5281/zenodo.7236452</code></td>
  </tr>
  <tr>
    <td>license</td>
    <td><code itemprop="license">https://creativecommons.org/licenses/by-nc/4.0/</code></td>
  </tr>
</table>
</div>
