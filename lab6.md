Problem Set 1

> great job! 19/20

1) As part of our matching procedure between the Macrostrat database and the Paleobiology database, we lost some data - i.e., there was some Paleobiology Database occurrences that could not be matched to the Macrostrat database. How many occurrences were lost? Show your code.

````R
> dim(DataPBDB)
[1] 34166    26
> dim(MacroPBDB)
[1] 9013   13
> 34166-9013
[1] 25153
````

2) Using what you know about the Macrostrat database can you speculate as to why so much data was lost?

Only information for North America is currently in the Macrostrat database, unlike the Paleobiology Database which is worldwide. 

## Problem Set 2

1) A good candidate for classification as a lagerstätten should have high diversity of different taxnomic orders. Calculate the order-level richness of each stratigraphic formation. Find the top 10 candidate units by this criteria. State them and give the code you used. Also, create a character vector( ) listing the names of these stratigraphic units. Name this vector CandidateUnits.
Hints

1. Remember how to calculate the richness of a sample, and apply this to each sample of the OrderMatrix.
2. If you do not remember how to calculate richness, consult the previous lab.
3. Use the sort( ) function to put your richnesses in order.
sort(specnumber(OrderMatrix))


````R
         			 Forteau Fm 
                                      14 
                            Parker Slate 
                                      16 
                          Snowy Range Fm 
                                      16 
                             Weymouth Fm 
                                      16 
                             Langston Fm 
                                      17 
                           Wheeler Shale 
                                      18 
                        Marjum Limestone 
                                      19 
                              Stephen Fm 
                                      23 
                              Kinzers Fm 
                                      24 
                              Chancellor 
                                      27 
````

2) A good candidate for classification as a lagerstätten should have a large number of genera that are relatively rare. Using the GenusMatrix column to find out how many samples each genus occurs in. Show the code you used. Name your output GenusFrequencies.

````R
> GenusFrequencies<-colSums(GenusMatrix)
````

3) What is the necessary code to make a frequency barplot of the GenusFrequencies?

````R
barplot(table(GenusFrequencies))
````

4) After looking at this barplot, you should see a familiar paleobiological pattern. What do we call this type of curved distribution in paleobiology and ecology. [Hint: Think back to the lectures]

Hollow Curve!

5) Subset your new vector GenusFrequences so that only those genera from the lower 50% of the distribution are present. In other words genera with occurrences <= to the median( ). Show your code. Name this new subset vector as RareGenera.

````R
RareGenera<-subset(GenusFrequencies,GenusFrequencies<=median(GenusFrequencies))
````

##### Problem Set 3
We will now take the list of rare genera you just made, RareGenera and see what percentage of genera in our top 10 candidate stratigraphic units CandiateUnits come from this list. We will then decide which of our 10 candidate units is the most likely to be a Lagerstätte.

1) Subset GenusMatrix so that it only shows the 10 stratigraphic units we determined were potential candidates. Show your code and name your new matrix, CandidateMatrix.
Load in the following code that I wrote for you. It will find the percentage of genera in each sample (stratigraphic unit) that occur in our vector of RareGenera.

````R
CandidateMatrix<-subset(GenusMatrix[Candidateunits,])
````

> -1 Points

2) Based on the output of PercentShared and your answer to Problem Set 2 - Question 1 - i.e., the ranking of candidate units based on the number of orders represented, which four units do you think are most likely to qualify as Lagerstätten? Explain your reasoning.

````R
> sort(PercentShared)
     Langston Fm 
       0.1632653 
  Snowy Range Fm 
       0.1951220 
   Wheeler Shale 
       0.2307692 
      Kinzers Fm 
       0.2586207 
    Parker Slate 
       0.2812500 
      Stephen Fm 
       0.3055556 
Marjum Limestone 
       0.3559322 
      Forteau Fm 
       0.5652174 
      Chancellor 
       0.5714286 
     Weymouth Fm 
       0.6764706 
````

We would want a high percentage of rare genera in a Lagerstaetten, so our top qualifiers are: Weymouth Fm, Chancellor Fm, Forteau Fm, and Marjum Limestone

3) Look closer into the four units you chose - using Google and information in the Paleobiology Database. One of these should be a very famous Lagerstätten. Which one? What is famous about it? What is its significance to Paleobiology?

Chancellor Group – it’s the Burgess Shale Formation, it has high preservation of soft body parts, and it was the first glimpse of the Cambrian Explosion 
