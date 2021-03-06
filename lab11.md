> 19/20

## Problem Set 1
1) You first mission is to download a list of all Triassic units in the Macrostrat Database using the /units route into R. Name this object TriassicUnits. As always, show your code.
Hints:
* You will want to use the read.csv( ) function, similarly to how we have loaded in Paleobiology Database data. Review previous labs if you do not remember how to use this function.
* You will want to make sure that you set the output format to csv.
* You should use the interval name Triassic rather than the numerical ages to define your search.


`> TriassicUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Triassic&format=csv")`

2) How many Triassic units did you download? What code did you use to find out?
838

````R
> dim(TriassicUnits)
[1] 838  17
````

3) Look at the first 10 units that you downloaded. Are they mostly Igneous, Metamorphic, or Sedimentary rocks? Do you believe that these units are relevant for an investigation of fossil preservation? Show your code and explain your reasoning.
Mainly igneous rocks. These rocks would not preserve any fossils, and therefore quite unhelpful in Paleobiology. 

`> TriassicUnits[1:10,]`

4) Which columns of your TriassicUnits data.frame denote the starting age and ending age of each unit, respectively?
t_age : termination age
b_age : beginning age

> (top age and bottom age!)

5) Considering the bottom and top ages of the first 10 units, are these units constrained to only the Triassic or do some range through the Triassic?

Most range through the Triassic, and last much longer than the Triassic 
````R
> TriassicUnits[1:10,"t_age"]
 [1]  67.037  74.975  92.875  92.875  92.875  92.875  93.900  95.550 100.500 103.625
> TriassicUnits[1:10,"b_age"]
 [1] 259.9000 396.8750 203.1000 203.1000 203.1000 203.1000 261.9667 203.1000 396.8750 249.1750
````

## Problem Set 2
1) Re-download TriassicUnits, however, this time restrict the data to only sedimentary rocks. Show your code.
Hints:
* /units documentation may provide some hepful information.
* /defs/lithologies may provide some helpful information.
* As before, use the read.csv( ) function and set the output format to csv.


`> TriassicUnitsSed<-read.csv("https://macrostrat.org/api/units?interval_name=Triassic&format=csv&lith_class=sedimentary")`

2) Restrict TriassicUnits to only units that with starting ages <= start of the Triassic and ending ages >= to the end of the Triassic. As always, show your code.
Hints:
* You will want to use either the which( ) or subset( ) functions.
* You will have to make use of logical operators >=, <=, and &. For a review of these, see the logical operators andsubsetting with logical operators sections of the R Tutorial.

`> Subset<-subset(TriassicUnitsSed,TriassicUnitsSed[,"b_age"]<=251&TriassicUnitsSed[,"t_age"]>=199)`

3) Repeat the above processes (download and subset) for the following geologic periods. The Cretaceous, Jurassic, Triassic (you don't have to download it twice), Permian, Carboniferous, Devonian, Silurian, and Ordovician. Show your code, but do not show me the downloaded data.

````R
> CretaceousUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Cretaceous&format=csv&lith_class=sedimentary")
> Cretaceous<-subset(CretaceousUnits,CretaceousUnits[,"b_age"]<=145.5&CretaceousUnits[,"t_age"]>=65.5)

> JurassicUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Jurassic&format=csv&lith_class=sedimentary")
> Jurassic<-subset(JurassicUnits,JurassicUnits[,"b_age"]<=199.6&JurassicUnits[,"t_age"]>=145.5)

> TriassicUnitsSed<-read.csv("https://macrostrat.org/api/units?interval_name=Triassic&format=csv&lith_class=sedimentary")
> Triassic<-subset(TriassicUnitsSed,TriassicUnitsSed[,"b_age"]<=251&TriassicUnitsSed[,"t_age"]>=199)

> PermianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Permian&format=csv&lith_class=sedimentary")
> Permian<-subset(PermianUnits,PermianUnits[,"b_age"]<=298.9&PermianUnits[,"t_age"]>=252.17)

> CarboniferousUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Carboniferous&format=csv&lith_class=sedimentary")
> Carboniferous<-subset(CarboniferousUnits,CarboniferousUnits[,"b_age"]<=359.2&CarboniferousUnits[,"t_age"]>=299)

> DevonianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Devonian&format=csv&lith_class=sedimentary")
> Devonian<-subset(DevonianUnits,DevonianUnits[,"b_age"]<=419.2&DevonianUnits[,"t_age"]>=358.9)

> SilurianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Silurian&format=csv&lith_class=sedimentary")
> Silurian<-subset(SilurianUnits,SilurianUnits[,"b_age"]<=443.8&SilurianUnits[,"t_age"]>=419.2)

> OrdovicianUnits<-read.csv("https://macrostrat.org/api/units?interval_name=Ordovician&format=csv&lith_class=sedimentary")
> Ordovician<-subset(OrdovicianUnits,OrdovicianUnits[,"b_age"]<=485.4&OrdovicianUnits[,"t_age"]>=443.8)
````

4) Make a vector named UnitFreqs that records the number of units present in each period. Show your code.

`> UnitFreqs<-c(nrow(Cretaceous),nrow(Jurassic),nrow(Triassic),nrow(Permian),nrow(Carboniferous),nrow(Devonian),nrow(Silurian),nrow(Ordovician))`
	

5) Find the mean and standard deviation of UnitFreqs not counting the Triassic. How many standard deviations above or below the mean is the number of Triassic Units? Show your code.

````R
> Vector<-UnitFreqs[-3]
> mean(Vector)
[1] 2105.714
> sd(Vector)
[1] 1339.846
> nrow(Triassic)
[1] 517
> mean(Vector)-nrow(Triassic)
[1] 1588.714
> 1588.714 / sd(Vector)
[1] 1.185744
````

The number of Triassic units is 1.185 standard deviations below the mean.

6) Given your answer to the above, do you believe that the Triassic has a statistically lower number of units than the other periods? Why?
No. If it was at least two standard deviations below the mean, it would be statistically significant. 

7) What if you consider both the Triassic and Jurassic as potential outliers? Explain (show your code) how you arrived at your answer.
````R
> Vectortwo<-Vector[-2]
> mean(Vectortwo)
[1] 2314.333
> sd(Vectortwo)
[1] 1337.401
> nrow(Jurassic)
[1] 854
> mean(Vectortwo) - nrow(Jurassic)
[1] 1460.333
> 1460.333 / sd(Vectortwo)
[1] 1.091919
````

Nope. Still under two standard deviations. 

## Problem Set 3
1) Download and plot a map of all North American geologic columns (no color). Show your code.
````R
> URL<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
> GotURL<-getURL(URL)
> NorthAmericanMap<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
> plot(NorthAmericanMap)
````

2) On top of your map from Question 1, plot a map of all North American columns with Induan-Anisian sedimentary units. Use the Olenekian hexcode color for this map. You can look up the Olenekian hexcode through the /defs/intervals route.

````R
> Induan<-"https://macrostrat.org/api/columns?age_top=242&age_bottom=252&lith_class=sedimentary&format=geojson_bare&project_id=1"
> InduanURL<-getURL(Induan)
> InduanMap<-readOGR(GotURL,"OGRGeoJSON",verbose = FALSE)
> plot(InduanMap,col="#A4469F",add=TRUE)
````

3) Using the downloadPBDB( ) function from previous labs. Download all occurrences of animal fossils in the Paleobiology Database of Induan-Anisian age. Using the points( ) function, plot all of these occurrences on the map you made in question 2 as solid circles. If you do not remember how to use points, you can consult previous labs or use help(points). Show your code. Save this map for later questions.

````R
> DataPBDB<-downloadPBDB(Taxa="Animalia",StartInterval="Induan-Anisian",StopInterval="Induan-Anisian")
> points(x=DataPBDB[,"paleolng"],y=DataPBDB[,"paleolat"],pch=19)
````

4) You can open a new plot window using quartz( ) if you are on a mac or `windows( ) if you are on a windows machine. Download and plot a map of all North American geologic columns (no color) - i.e., repeat Question 1 in this new plot window. On top of this map, plot a map of all North American columns with Lopingian aged sedimentary units. Use the appropriate Lopingian hexcode color for this new map. Show your code.

````R
> plot(NorthAmericanMap)
> Logpinian<-"https://macrostrat.org/api/columns?age_top=252&age_bottom=259&lith_class=sedimentary&format=geojson_bare&project_id=1"

> LopingianURL<-getURL(Lopingian)
> LopingianMap<-readOGR(GotURL,"OGRGeoJSON",verbose = FALSE)
> plot(LopingianMap,col="#FBA794",add=TRUE)
````

5) Download all occurrences of animal fossils in the Paleobiology Database of Lopingian age. Plot all of these occurrences on the map you made in question 2 as solid circles. Show your code.

````R
> DataPBDB<-downloadPBDB(Taxa="Animalia",StartInterval="Lopingian",StopInterval="Lopingian")
> points(x=DataPBDB[,"paleolng"],y=DataPBDB[,"paleolat"],pch=19)
````

6) Compare and contrast your Induan-Anisian map versus your Lopingian map. Does it seem based on these maps that...
* There was a substantial drop in the areal extent of North American sedimentary units across the P/T boundary.
no
* There was a substantial drop in the percentage of sedimentary units with reported fossils in them aross the P/T boundary?
no
* Overall, do you think there is sufficient evidence from these maps to reject or accept the hypothesis that lower diversity in the Early Triassic is an artefact of either poor fossil sampling of the available sedimentary rock or a low availablility of sedimentary rock.
no


> Hey! You didn't exlain your reasoning. -1 Points
