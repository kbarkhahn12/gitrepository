> 20/20

## Problem Set I

1) How many unique genera are in the Miocene, Early Jurassic, Late Cretaceous, and Pennsylvanian epochs (not total, each)? What code did you use to find out?

a. apply(PresencePBDB,1,sum)
b. Miocene: 602
c. Early Jurassic: 169
d. Late Cretaceous: 375
e. Pennsylvanian: 133

2) How many geologic epochs in general are in this dataset? What code did you use to find out?

a) dim(PresencePBDB)
b) 29

3) Which epochs contain specimens of the genus Mytilus? What code did you find out?

a) PresencePBDB[,”Mytilus”]
b) Pridoli, Early Devonian, Cisuralian, Early Triassic, Middle Triassic, Late Triassic, Early Jurassic, Middle Jurassic, Late Jurassic, Early Cretaceous, Late Cretaceous, Paleocene, Eocene, Oligocene, Miocene, Pliocene, Pleistocene

4) Look at the epochs in the geologic timescale. Using your answer to question 3, in which epochs can we infer that Mytilus was present, even though we have no record of them in the Paleobiology Database? How did you deduce this?

a) Middle Devonian, Late Devonian, Early Mississippian, Middle Mississippian, Late Mississippian, Early Pennsylvanian, Middle Pennsylvanian, Late Pennsylvanian,  Guadalupian, Lopingain
b) These are all the epochs in between the known epochs

## Problem Set II
The Jaccard index is the simplest Similarity index. It is the intersection of two samples divided by the union of two samples. In other words, the number of genera shared between two samples, divided by the total number of (unique) genera in both samples.

1) Using your own custom R code, find the Jaccard similarity of the Pleistocene and Miocene "samples" in your PresencePBDB matrix. It is possible to code this entirely using only functions discussed in the R Tutorial, but here are some additional functions that may be helpful.

a. Vector1<-PresencePBDB[“Miocene”,]
b. Vector2<-PresencePBDB[“Pleistocene”,]
c. Resultantvector<-Vector1+Vector2
d. Table(Resultantvector)
i. 0	1	2
ii. 287	106	510
e. 510/(106+510) = .8279221

2) How can you convert your similarity index into a distance?
a. A dissimilarity index – so 1-.8279221=0.1720779

3) Install and load the vegan package into R. Read the help file for the vegdist function - ?vegdist or help(vegdist). Again, calculate the jaccard distance of the "Miocene" and "Pleistocene" samples of PresencePBDB, but this time use the vegdist( ) function. This should be an identical answer to what you got in question 2.

a. Library(“vegan”)
b. vegdist(PresencePBDB,method = "jaccard",binary=FALSE,diag=FALSE,upper=FALSE,na.rm=FALSE)
c. Pleistocene, Miocene = 0.17207792

4) Using the vegdist( ) function. Calculate the Jaccard distances of all the following epochs in PresencePBDB - the "Pleistocene", "Pliocene", "Miocene", "Oligocene", "Eocene", "Paleocene". What code did you use? Which two epochs are the most dissimilar?

a. Pleistocenevector<-PresencePBDB[“Plesistocene”,]
b. Pliocenevector<-PresencePBDB[“Pliocene”,]
c. Miocenevector<-PresencePBDB[“Miocene”,]
d. Oligocenevector<-PresencePBDB[“Oliocene”,]
e. Eocenevector<-PresencePBDB[“Eocene”,]
f. Paleocene<-PresencePBDB[“Paleocene”,]
g. PBDBmatrix<-rbind(Pleistocenevector,Pliocenevector,Miocenevector,Oligocenevector,Eocenevector,Paleocenevector)
h. Vegdist(PBDBmatrix,method”jaccard”,binary=FALSE,diag=FALSE,upper=FALSE,na.rm=FALSE)
i. Most dissimilar=Pleistocene and Paleocene at .444444444

		Pleistocenevector Pliocenevector Miocenevector Oligocenevector Eocenevector
Pliocenevector         0.12692967                                                          
Miocenevector          0.17207792     0.08496732                                           
Oligocenevector        0.26910299     0.18968386    0.16065574                             
Eocenevector           0.21870048     0.13397129    0.08585056      0.19063005             
Paleocenevector        0.44444444     0.37914692    0.33333333      0.41042345   0.33385827

## Problem Set III
1) Create a subset of the PresencePBDB matrix which contains just the following rows - "Pliocene", "Oligocene", "Paleocene", "Early Cretaceous", "Late Jurassic", and "Middle Jurassic". Name this subset RandomEpochs. Show your code.

a. RandomEpochs<-rbind(PresencePBDB["Pliocene",],PresencePBDB["Oligocene",],PresencePBDB["Paleocene",],PresencePBDB["Early Cretaceous",],PresencePBDB["Late Jurassic",],PresencePBDB["Middle Jurassic",])

2) Using vegdist( ) find the dissimilarities of all the epochs in Random Epochs. Show your code.
a. vegdist(RandomEpochs,method=”jaccard”,bindary)
b. Bob<- Vegdist(RandomEpochs,method=”jaccard”,bindary)
c. max(Bob) 
i. 0.8852459

          1         2         3         4         5
2 0.1896839                                        
3 0.3791469 0.4104235                              
4 0.7462908 0.7480315 0.6400742                    
5 0.8652695 0.8653846 0.7902622 0.4703947          
6 0.8852459 0.8814103 0.7931689 0.4883721 0.2962963


3) Find the two epochs that are the most dissimilar and make them the poles. Now, using the dissimilarities, order (ordinate) the remaining epochs based on their similarity to the poles. State the order of your inferred gradient.
a. Most dissimilar are epochs 1 and 6 ->Pliocene and Middle Jurassic
b. 1, 2, 3, 4, 5, 6 – Pliocene, Oligocene, Paleocene, Early Cretaceous, Late Jurassic, Middle Jurassic

4) Can you deduce what "variable" is controlling this gradient (e.g., temperature, water depth, geographic distance)? [Hint: Check the geologic timescale]. State your reasoning.

a. Decreasing temp from Middle Jurassic to Pliocene, which implies lowering of sea level, complete break up of Pangea

> We know that they are in chornological order, so the clearest pattern is a separation in time. Do you remember discussing "complex" and "indirect" gradients in class?

5). There is a relatively high dissimilarity between the Early Cretaceous and Paleocene epochs. Can you hypothesize why this is? Google these epochs if you need to.

a. K/Pg mass extinction - asteroid impact

## Problem Set IV
1) Download a dataset from the paleobioogy database of all Ordovician aged animals into R, and name the object Ordovician. This may take a few minutes. What R code did you use?

a. Ordovician<-downloadPBDB(Taxa=c(“Animalia”),StartInterval="Ordovician",StopInterval="Ordovician")

2) Clean up the poorly resolved genus names. What function/code did you use?
a. cleanGenus(Ordovician)
3) Turn your object Ordovician into a community matrix of samples by genera, where the samples are different geoplate codes. Geoplate codes denote different ancient paleocontinents - i.e., your community matrix will list which genera were present in which ancient paleocontinent. Cull this matrix so that each sample has a minimum of 25 taxa and each taxon occurs in at least two samples. Show your code.

a. Ordo<-presenceMatrix(Ordovician,SampleDefinition = "geoplate")
b. Ordo<-cullMatrix(Ordo,minOccurrences = 2,minDiversity = 25)

4) Perform a DCA on your new community matrix. Analyze your new DCA with a plot. Do you think that the orientation of samples along either axis 1 or axis 2 is related to the average latitude or longitude of each plate in question? Explain how you figured this out. Show your code.

a. OrdoDCA<-decorana(Ordo)
b. Plot(OrdoDCA,display=”sites”)
c. tapply(Ordovician[,"paleolat"],Ordovician[,"geoplate"],mean)
i. probs not, points on plot are not close in lat and long according to original data
