> 20/20

## Problem Set 1
There is a longstanding story that Triassic Diapsids outcompeted Triassic Syanpsids. Let's see if Triassic Diapsids were more likley to survive the Traissic/Jurassic extinction than Synapsids.

Question 1

Download four data sets from the paleobiology database. First, a dataset of Anisian-Rhaetian Synapsids, name it TriassicSynapsids. Second, a dataset of Anisian-Rhaetian Diapsids, name it TriassicDiapsids. Third, a dataset of post-Triassic Diapsids, name it JurassicDiapsids. Fourth, a dataset of post-Triassic Synapsids, name it JurassicSynapsids. Show your code.
Hint:
* Use the formal terms Diapsida and Synapsida when downloading the data.

````R
> TriassicSynapsids<-downloadPBDB("Synapsida","Anisian","Rhaetian")
> JurassicSynapsids<-downloadPBDB("Synapsida","Jurassic","Neogene")
> TriassicDiapsids<-downloadPBDB("Diapsida","Anisian","Rhaetian")
> JurassicDiapsids<-downloadPBDB("Diapsida","Jurassic","Neogene")
> TriassicSynapsids<-cleanRank(TriassicSynapsids,"genus")
> JurassicSynapsids<-cleanRank(JurassicSynapsids,"genus")
> TriassicDiapsids<-cleanRank(TriassicDiapsids,"genus")
> JurassicDiapsids<-cleanRank(JurassicDiapsids,"genus")
````

Question 2

How many Diapsid genera were there in the Triassic dataset? How many Synapsid genera? Show your code.
Hint:
* Remember, there is a difference between the number of genera and the number of occurrences.
* Don't forget to clean up the genus names!

````R
> TriassicDiapsidGenera<-unique(TriassicDiapsids[,"genus"])
389 total genera
> TriassicSynapsidsGenera<-unique(TriassicSynapsids[,"genus"])
116 total genera

> JurassicSynapsidGenera<-unique(JurassicSynapsids[,"genus"])
> JurassicDiapsidGenera<-unique(JurassicDiapsids[,"genus"])
````

Question 3

How many Triassic Diapsid genera survived the Triassic/Jurassic transition? How many were victims? How many Triassic Synapsid genera survived the Triassic/Jurassic Transition? How many were victims? Show your code.

````R
> TriassicDiapsidSurvivors<-intersect(TriassicDiapsidGenera,unique(JurassicDiapsidGenera))
37 diapsid survivors
> TriassicSynapsidSurvivors<-intersect(TriassicSynapsidsGenera,unique(JurassicSynapsidGenera))
9 Synapsid survivors 
> SynapsidVictims<-setdiff(TriassicSynapsidsGenera,JurassicSynapsidGenera)
107 Synapsid Victims 
> DiapsidVictims<-setdiff(TriassicDiapsidGenera,JurassicDiapsidGenera)
352 Diapsid Survivors

Question 4
Calculate the odds ratio and log-odds that Diapsid genera were more likely to survive the T/J transition than Synapsids

````R
> DiapsidOdds<-(length(TriassicDiapsidSurvivors)/length(TriassicDiapsidGenera))/(length(DiapsidVictims)/length(TriassicDiapsidGenera))
> SynapsidOdds<-(length(TriassicSynapsidSurvivors)/length(TriassicSynapsidsGenera))/(length(SynapsidVictims)/length(TriassicSynapsidsGenera))
> OddsRatio<-DiapsidOdds/SynapsidOdds
> OddsRatio
[1] 1.249684
> log(OddsRatio)
[1] 0.222891
````

Question 5
Using a 95% confidence interval, can you say that this odds/ratio is "statistically significant"? Show your code.
````R
> StandardError<-sqrt(1/length(TriassicDiapsidSurvivors)+ 1/length(DiapsidVictims) + 1/length(TriassicSynapsidSurvivors)+ 1/length(SynapsidVictims))
> StandardError
[1] 0.3877175
> UpperLimit<-log(OddsRatio) + (StandardError*1.96)
> UpperLimit
[1] 0.9828172
> LowerLimit<-log(OddsRatio) - (StandardError*1.96)
> LowerLimit
[1] -0.5370353
````
No, this is not significantly significant because the lower limit is negative. 

## Problem Set 2
Let's apply the technique that you just learned the Triassic and Jurassic Diapsids and Synapsids.
Queston 1
Download a dataset of Anisian-Rhaetian Diapsids and Synapsids, and a dataset of post-Triassic Diapsids and Synapsids. Show your code.
````R
> TriassicSynapandDiap<-downloadPBDB(c("Synapsida","Diapsida"),"Anisian","Rhaetian")

> JurassicSynapandDiap<-downloadPBDB(c("Synapsida","Diapsida"),"Jurassic","Neogene")
> TriassicSynapandDiap<-cleanRank(TriassicSynapandDiap,"genus")
> JurassicSynapandDiap<-cleanRank(JurassicSynapandDiap,"genus")
````

Question 2
Find the mean latitude of each genus's occurrences in your Triassic dataset. Show your code.

````R
> MeanLatitudes<-tapply(TriassicSynapandDiap[,"paleolat"],TriassicSynapandDiap[,"genus"],mean)
> head(MeanLatitudes)
Acaenasuchus  10.116
Acallosuchus 10.430
Acompsosaurus   10.740
Actiosaurus 32.120
Adamanasuchus 10.145
Adelobasileus 10.170
```` 

Question 3
Find which Triassic genera were survivors and which were victims of the Triassic/Jurassic event. Show your code.
````R
> SynapandDiapSurvivors<-subset(TriassicSynapandDiap,TriassicSynapandDiap[,"genus"]%in%unique(JurassicSynapandDiap[,"genus"])==TRUE)
> SynapandDiapSurvivors<-unique(SynapandDiapSurvivors[,"genus"])
> head(SynapandDiapSurvivors)
[1] "Clevosaurus"        "Grallator"          "Rhynchosauroides"   "Rotodactylus"      
[5] "Brachychirotherium" "Coelurosaurichnus" 

> SynapandDiapVictims<-subset(TriassicSynapandDiap,TriassicSynapandDiap[,"genus"]%in%unique(JurassicSynapandDiap[,"genus"])!=TRUE)
> SynapandDiapVictims<-unique(SynapandDiapVictims[,"genus"])
> head(SynapandDiapVictims)
[1] "Icarosaurus"      "Rutiodon"         "Kuehneosuchus"    "Kuehneosaurus"   
[5] "Trilophosaurus"   "Diphydontosaurus"
````

Question 4
Find which genera of your Triassic dataset were Diapsids and which were Synapsids. Show your code.
````R
> Vector<-subset(TriassicSynapandDiap,TriassicSynapandDiap[,"genus"]%in%TriassicSynapsids[,"genus"]==TRUE)
> SynapVector<-unique(Vector[,"genus"])
> SynapVector
116 Synapsid genera
> Vector2<-subset(TriassicSynapandDiap,TriassicSynapandDiap[,"genus"]%in%TriassicDiapsids[,"genus"]==TRUE)
> DiapVector<-unique(Vector2[,"genus"])
389 Diapsid genera
````

Question 5

Perform a logistic regression where the outcome variable is Survivor/Victim and the input variable is the mean latitude of each genus. Show your code. Was the mean latitude of a Triassic genus a good predictor of its survival across the T/J extinction?
````R
> Victims<-array(0,dim=length(SynapandDiapVictims),dimnames=list(SynapandDiapVictims))
> head(Victims)
     Icarosaurus         Rutiodon    Kuehneosuchus    Kuehneosaurus   Trilophosaurus 
               0                0                0                0                0 
Diphydontosaurus 
               0 
> FinalMatrix<-merge(MeanLatitudes,Victims,all=TRUE,by="row.names")
> head(FinalMatrix)
      Row.names      x y
1  Acaenasuchus 10.116 0
2  Acallosuchus 10.430 0
3 Acompsosaurus 10.740 0
4   Actiosaurus 32.120 0
5 Adamanasuchus 10.145 0
6 Adelobasileus 10.170 0
> FinalMatrix<-transform(FinalMatrix,row.names=Row.names,Row.names=NULL)
> colnames(FinalMatrix)<-c("MeanLatitudes","Survivor/Victim")
> head(FinalMatrix)
              MeanLatitudes Survivor/Victim
Acaenasuchus         10.116               0
Acallosuchus         10.430               0
Acompsosaurus        10.740               0
Actiosaurus          32.120               0
Adamanasuchus        10.145               0
Adelobasileus        10.170               0
> FinalMatrix[is.na(FinalMatrix[,"Survivor/Victim"]),]<-1
> head(FinalMatrix)
              MeanLatitudes Survivor/Victim
Acaenasuchus         10.116               0
Acallosuchus         10.430               0
Acompsosaurus        10.740               0
Actiosaurus          32.120               0
Adamanasuchus        10.145               0
Adelobasileus        10.170               0
> Regression<-glm(FinalMatrix[,"Survivor/Victim"]~FinalMatrix[,"MeanLatitudes"],family="binomial")
> summary(Regression)

Call:
glm(formula = FinalMatrix[, "Survivor/Victim"] ~ FinalMatrix[, 
    "MeanLatitudes"], family = "binomial")

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-0.4474  -0.4411  -0.4385  -0.4308   2.1889  

Coefficients:
                                 Estimate Std. Error z value Pr(>|z|)    
(Intercept)                    -2.3009122  0.1547326  -14.87   <2e-16 ***
FinalMatrix[, "MeanLatitudes"]  0.0007725  0.0051555    0.15    0.881    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 308.10  on 504  degrees of freedom
Residual deviance: 308.08  on 503  degrees of freedom
AIC: 312.08

Number of Fisher Scoring iterations: 5
````

NO.
