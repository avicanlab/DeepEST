# DeepEST
This is the repository with the implementation of DeepEST, a multimodal method to perform protein function prediction for bacterial species. Given the characteristics of their genome, the functional characterization of bacteria cannot rely solely on protein sequences. In fact, it requires the use of data sources capable of capturing different dimensions of the protein functionality, i.e., protein structures and expression-location patterns.

The architecture of DeepEST, visualized in the following figure, is comprised of two main modules:
1) the fine-tuned structure module [1], and
2) the expression-location module.

Subsequently, the two modalities are integrated through learnable linear combination.

![method](https://github.com/BorgwardtLab/DeepEST/assets/56036317/bb421134-1ad6-4bc9-8220-440db949b624)

## Repository organization

### 1) DeepEST implementation
The ```python``` implementation of DeepEST is available under _train_model/_. The data to test the implementation is available with the release. Once the folder data has been places into _train_model/_, you can use the following command to train the model:

```
python3 train_DeepEST.py \
--split 0 \
--splitdir splits/Staphylococcus_aureus_MSSA476/ \
--config configs/fold0/config_combined_Staphylococcus_aureus_MSSA476.yaml \
--expr-loc data/expr-loc/Staphylococcus_aureus_MSSA476_genomic_info.csv \
--structures data/all_proteins.pkl \
--label data/matrix_label/label_matrix_Staphylococcus_aureus_MSSA476_thr10_new.csv \
--conversion_dict data/conversion_dicts/conv_Staphylococcus_aureus_MSSA476.txt \
--outdir predictions/ \
--species Staphylococcus_aureus_MSSA476
```

#### Dependencies
To successfully run the command above, the following libraries should be istalled:

### 2) DeepEST annotations on hypothetical proteins
The folder `hypothetical_proteins/` contains the annotations generated by DeepEST on the nearly 7'000 unannotated proteins from the 25 bacteria.

## Data
We study a selection of 25 bacterial species, namely:

![Species](https://github.com/BorgwardtLab/DeepEST/assets/56036317/7a24e712-8b1d-41c1-8990-a1272a8094a2)

In the following, we describe how to collect the data (gene expression and location data, protein structures, and GO terms annotations) we use to perform the study described in the manuscript. 

- ### Expression and location data
  As expression-location data, we use previously reported [PATHOgenex dataset](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE152295) [2], which contains both the genomic location information and the gene expression levels of 105,088 genes in 32 clinically relevant-human bacterial pathogens under 11 in vivo mimicking stress conditions and unexposed control. Specifically, as input features for our model, we consider the log-fold change values derived from the differential expression analysis of these 11 stress conditions in comparison to the control. 

- ### Protein structures
  We use protein structures downloaded from the [AlphaFold database](https://alphafold.ebi.ac.uk/) [3].

- ### GO terms annotations
  GO annotations are retrieved from the [UniProt database](https://www.uniprot.org/) [4] (accessed on July 12, 2023) using the RefSeq protein identifier of every known protein and the taxonomic reference code of a given pathogen's strain. 
To retrieve a particular GO term's children or ancestors we use the [GO ontology](https://geneontology.org/docs/download-ontology/) released on October 7, 2022.


## References
[1] Gligorijevi ́c, V., et al.: Structure-based protein function prediction using graph convolutional networks. Nat. Commun. 12, 3168 (2021)

[2] Avican, K., et al.: RNA atlas of human bacterial pathogens uncovers stress dynamics linked to infection. Nat. Commun. 12, 3282 (2021)

[3] Mihaly Varadi et al. AlphaFold Protein Structure Database: massively expanding the structural coverage of protein-sequence space with high-accuracy models. Nucleic Acids Research, 50(D1):D439–D444, 2021.

[4] The UniProt Consortium. UniProt: the Universal Protein Knowledgebase in 2023. Nucleic Acids Research, 51(D1):D523–D531, 2022.

## Contacts
For queries on the implementation and data, please contact:
- giulia.muzio@bsse.ethz.ch
- leyden.fernandez@umu.se


## Funding
This project has received funding from the European Union’s Horizon 2020 research and innovation programme under the Marie Sklodowska-Curie grant agreement (No 813533). Swedish Research Council (No. 2021-02466), Kempes-tiftelserna (JCK22-0017), Insamlingsstiftelsen, Medical Faculty at Ume ̊a University to K Avican and Icelab Multidisciplinary Postdoctoral Fellowship to L Fernandez.
