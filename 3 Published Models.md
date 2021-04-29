Before I start building my own prediction models, I have to firstly learn about other people's work. I shared the following contents in the group meeting, and the slides used are uploaded.

Three published models are introduced here, all of which aim to predict the liquid-liquid phase separation property from AA sequences.
* FuzDrop

Publish information<br>
Title: Widespread occurrence of the droplet state of proteins in the human proteome<br>
Journal: Proc Natl Acad Sci U S A<br>
Date: Dec 29, 2020<br>
URL: https://www.ncbi.nlm.nih.gov/pubmed/33318217<br>

* PSAP

Publish information<br>
Title: Predicting protein condensate formation using machine learning<br>
Journal: Cell Rep<br>
Date: Feb 2, 2021<br>
URL: https://www.ncbi.nlm.nih.gov/pubmed/33535034<br>

* DeePhase
Publish information<br>
Title: Learning the molecular grammar of protein condensates from sequence determinants and embeddings<br>
Journal: Proc Natl Acad Sci U S A<br>
Date: Apr 13, 2021<br>
URL: https://www.ncbi.nlm.nih.gov/pubmed/33827920<br>
Prediction tool: https://deephase.ch.cam.ac.uk/<br>

# Overview of basic steps to build a model
A work concerning a prediction model should include the following parts:
1. Set up labelled datasets<br>
Decide which sequences do phase separate and which do not, or there can be a third catagory.
2. Feature engineering<br>
This part usually uses prior knowledge about the AA properties that influences phase separation abilities. Researchers perform statistical analysis to show whether there's significant difference of a certain feature between different datasets (set up in step 1). Even features computed by machine learning requires this step to increase interpretation.
3. Mode Training<br>
Using features generated (from physics or ML embedding) to train the model, which can be logistic regression, random forest etc.
4. Model testing<br>
  4.1 Test sets<br>
  Researchers have to find a different dataset to test the models, not just a split part from the training set (that is the validation set). This shows generality of the model.<br>
  4.2 Accuracy, sensitivity, robustness, generality, ROC, AUC<br>
  Of course these are parametres to be presented in order to prove a successful work..
5. Lab experiments<br>
Some articles include lab experiments to check whether their prediction works, though only limited number of proteins can be varified in this way.
6. Interpretation <br>
Results given by ML models usually requires interpretation of known physical knowledge.
7. Application <br>
LLPS prediction performed on experimentally untouched proteins or genome wide might provide implications.

* In this introduction, only datasets set-up, feature engineering, and model training are concerned.

# FuzDrop
## Publish information
Title: Widespread occurrence of the droplet state of proteins in the human proteome<br>
Journal: Proc Natl Acad Sci U S A<br>
Date: Dec 29, 2020<br>
URL: https://www.ncbi.nlm.nih.gov/pubmed/33318217<br>

## Data source
* PhaSepDB dataset (http://db.phasep.pro/), including 3 resources<br>
1) proteins from the literature with in vivo and in vitro experimental data on liquid–liquid phase separation (REV, 351 proteins)<br>
2) proteins from UniProt associated with known organelles (UNI, 378 proteins)<br>
3) proteins identified by high-throughput experiments of liquid–liquid phase separation (HTS, 2,572 proteins)<br>
* PhaSePro (https://phasepro.elte.hu) protein regions associated with liquid–liquid phase separation (PSP)
* LLPSDB (http://bio-comp.org.cn/llpsdb) 
* proteins can phase separate spontaneously as one component (droplet-driving proteins, LPS-D, 133 proteins); require a partner to undergo liquid–liquid phase separation (droplet-client proteins, LPS-C, 41)

## Datasets
* S1: positive set<br>
REV(351), UNI(378), HTS(2572), PSP(121), LPS-D(133), LPS-C(41)<br>
LLPS(445) = REV + HTS + LPS-D<br>
* S2: negative set<br>
1. human negative set (hsnLLPS dataset, 18,108 proteins)<br>
2. Multiple-organisms negative set (nsLLPS)<br>
organism distribution from the LLPS dataset<br>
randomly chose sequences according to the frequencies of these organisms in the LLPS dataset with 10 times enrichment<br>

## The Fuzdrop model
![图片](https://user-images.githubusercontent.com/82629502/116549274-dc504980-a927-11eb-9020-f3fb3d235229.png)
### Explanations
* Disorder in the free state<br>
pD(Ai) is the probability for disorder in the free state; pD(Ai) contains an estimate of the conformational entropy in the unbound form<br>
pD was derived from the disorder score as computed using the ESpritz NMR algorithm<br>
http://old.protein.bio.unipd.it/espritz/<br>
* Espritz interface
![图片](https://user-images.githubusercontent.com/82629502/116549561-38b36900-a928-11eb-89dc-02fb335abf3b.png)
* Espritz results
![图片](https://user-images.githubusercontent.com/82629502/116549636-4ff25680-a928-11eb-8adf-459faf452be0.png)

## Disorder in the binding state<br>
pDD(Ai) is the probability for disordered binding; pDD(Ai) contains an estimate of the binding entropy<br>
The pDD values were predicted by the FuzPred method<br>
http://fuzpred.med.unideb.hu/fuzpred/upload_fasta.php<br>
* FuzPred interface
![图片](https://user-images.githubusercontent.com/82629502/116549755-77e1ba00-a928-11eb-8d4d-e2aff1907fd1.png)

## The Full Fuzdrop model
* median{pDP(Ai)} is the median of the residue droplet-promoting propensities
* nDPR is the number of long droplet-promoting regions (DPRs; ≥25 consecutive residues with pDP ≥ 0.6)
* H is a hydrophobic term (≥6-residue hydrophobic motifs within disordered regions)<br>
To distinguish between hydrophobic interactions driving structure formation and those in droplets, we used hydrophobic motifs (≥6 consecutive residues), which were located in disordered regions. The threshold was set to −1.3 based on the Kyte–Doolittle hydrophobicity scale, to include S, T, and Y capable of undergoing phosphorylation.

# PSAP
## PSAP Model
* Positive datasets (PPS Proteins): manually curated, 90 high-confidence human proteins
* Negative set: the rest of the human proteome
* 55 features from the aa sequence
* random forest classifier<br>
  * normalized by scaling using the StandardScaler from Scikit learn<br>
  * features with a Pearson correlation lower than 0.95 were removed<br>
  * hyperparameters: n_estimators = 1200 (number of trees), class_weight = ‘balanced’ and criterion = ‘entropy’<br>

![图片](https://user-images.githubusercontent.com/82629502/116550762-bb88f380-a929-11eb-9023-7988a5663844.png)
![图片](https://user-images.githubusercontent.com/82629502/116550779-bfb51100-a929-11eb-8016-0d6ae9fe92de.png)

# DeePhase
![图片](https://user-images.githubusercontent.com/82629502/116551047-13bff580-a92a-11eb-9512-57a41f757ba6.png)
![图片](https://user-images.githubusercontent.com/82629502/116551176-3a7e2c00-a92a-11eb-8a11-ef25e782442b.png)
![图片](https://user-images.githubusercontent.com/82629502/116551185-3ce08600-a92a-11eb-8c66-09c67db81b48.png)
![图片](https://user-images.githubusercontent.com/82629502/116551195-3f42e000-a92a-11eb-9034-10f7caee8d61.png)
![图片](https://user-images.githubusercontent.com/82629502/116551204-42d66700-a92a-11eb-8ec0-243dd0a2b143.png)
![图片](https://user-images.githubusercontent.com/82629502/116551213-45d15780-a92a-11eb-99af-d66c6b17180a.png)
![图片](https://user-images.githubusercontent.com/82629502/116551223-4964de80-a92a-11eb-93c5-2f39b93526ec.png)
![图片](https://user-images.githubusercontent.com/82629502/116551232-4bc73880-a92a-11eb-92cb-2b84f301ceea.png)
![图片](https://user-images.githubusercontent.com/82629502/116551255-508bec80-a92a-11eb-90e5-f024d88cb36e.png)
![图片](https://user-images.githubusercontent.com/82629502/116551267-5386dd00-a92a-11eb-8a40-1e6e894a786d.png)









