## Choppies Stores Summary

The growth of Choppies supermarket from 1999 to 2021


```R
#Choppies.csv
choppies <- read.csv("choppies.csv")
```


```R
str(choppies)
```

    'data.frame':	108 obs. of  8 variables:
     $ Name     : chr  "Choppies Bobonong" "Choppies Letlhakane" "Choppies Mahalapye" "Choppies Mahalapye" ...
     $ District : chr  "Central" "Central" "Central" "Central" ...
     $ Town     : chr  "Bobonong" "Letlhakane" "Mahalapye" "Mahalapye" ...
     $ Address  : chr  "Moilamba Ward,Cash Bazaar building" "Nkosho Ward,Letlhakane" "Plot 6042, Main Mall, Mahalapye" "Watershed Mall, A1,  Mahalapye" ...
     $ latitude : num  -22 -21.4 -23.1 -23.1 NA ...
     $ longitude: num  28.4 25.6 26.8 26.8 NA ...
     $ Date     : chr  "12/09/2012" "12/10/2007" "13/01/2012" "" ...
     $ Registred: chr  "Y" "Y" "Y" "Y" ...
    


```R
choppies$Name <- as.character(choppies$Name )
choppies$Address <- as.character(choppies$Address)
choppies$Date <- as.Date(choppies$Date, "%d/%m/%Y")
```

Converting variables to lowercase makes them easy to work with...


```R
names(choppies) <- tolower(names(choppies))
```


```R
str(choppies)
```

    'data.frame':	108 obs. of  8 variables:
     $ name     : chr  "Choppies Bobonong" "Choppies Letlhakane" "Choppies Mahalapye" "Choppies Mahalapye" ...
     $ district : chr  "Central" "Central" "Central" "Central" ...
     $ town     : chr  "Bobonong" "Letlhakane" "Mahalapye" "Mahalapye" ...
     $ address  : chr  "Moilamba Ward,Cash Bazaar building" "Nkosho Ward,Letlhakane" "Plot 6042, Main Mall, Mahalapye" "Watershed Mall, A1,  Mahalapye" ...
     $ latitude : num  -22 -21.4 -23.1 -23.1 NA ...
     $ longitude: num  28.4 25.6 26.8 26.8 NA ...
     $ date     : Date, format: "2012-09-12" "2007-10-12" ...
     $ registred: chr  "Y" "Y" "Y" "Y" ...
    


```R
summary(choppies)
```


         name             district             town             address         
     Length:108         Length:108         Length:108         Length:108        
     Class :character   Class :character   Class :character   Class :character  
     Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                                
                                                                                
                                                                                
                                                                                
        latitude        longitude          date             registred        
     Min.   :-26.02   Min.   :21.64   Min.   :1999-11-02   Length:108        
     1st Qu.:-24.66   1st Qu.:25.55   1st Qu.:2006-03-16   Class :character  
     Median :-24.61   Median :25.87   Median :2012-06-22   Mode  :character  
     Mean   :-23.48   Mean   :25.81   Mean   :2011-09-14                     
     3rd Qu.:-21.98   3rd Qu.:26.11   3rd Qu.:2014-10-28                     
     Max.   :-17.80   Max.   :28.42   Max.   :2021-10-28                     
     NA's   :29       NA's   :29      NA's   :10                             



```R
library(dplyr)
```

    
    Attaching package: 'dplyr'
    
    
    The following objects are masked from 'package:stats':
    
        filter, lag
    
    
    The following objects are masked from 'package:base':
    
        intersect, setdiff, setequal, union
    
    
    


```R
choppies %>% group_by(district) %>% summarise(n = n()) %>% arrange(desc(n))
```


<table class="dataframe">
<caption>A tibble: 12 × 2</caption>
<thead>
	<tr><th scope=col>district</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>South-East</td><td>42</td></tr>
	<tr><td>Kweneng   </td><td>18</td></tr>
	<tr><td>Central   </td><td>17</td></tr>
	<tr><td>Southern  </td><td> 9</td></tr>
	<tr><td>North-East</td><td> 8</td></tr>
	<tr><td>North-West</td><td> 4</td></tr>
	<tr><td>Chobe     </td><td> 2</td></tr>
	<tr><td>Ghanzi    </td><td> 2</td></tr>
	<tr><td>Kgalagadi </td><td> 2</td></tr>
	<tr><td>Kgatleng  </td><td> 2</td></tr>
	<tr><td>kgatleng  </td><td> 1</td></tr>
	<tr><td>south-East</td><td> 1</td></tr>
</tbody>
</table>




```R
choppies %>% group_by(town) %>% 
summarise(n = n()) %>% 
arrange(desc(n)) %>%
top_n(10) 
```

    [1m[22mSelecting by n
    


<table class="dataframe">
<caption>A tibble: 10 × 2</caption>
<thead>
	<tr><th scope=col>town</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Gaborone    </td><td>28</td></tr>
	<tr><td>Mogoditshane</td><td> 9</td></tr>
	<tr><td>Francistown </td><td> 7</td></tr>
	<tr><td>Lobatse     </td><td> 7</td></tr>
	<tr><td>Mahalapye   </td><td> 3</td></tr>
	<tr><td>Maun        </td><td> 3</td></tr>
	<tr><td>Molepolole  </td><td> 3</td></tr>
	<tr><td>Palapye     </td><td> 3</td></tr>
	<tr><td>Ramotswa    </td><td> 3</td></tr>
	<tr><td>Tlokweng    </td><td> 3</td></tr>
</tbody>
</table>




```R
choppies$month <- months(choppies$date)
choppies$year <- as.numeric(format(choppies$date, "%Y"))
```


```R
str(choppies)
```

    'data.frame':	108 obs. of  10 variables:
     $ name     : chr  "Choppies Bobonong" "Choppies Letlhakane" "Choppies Mahalapye" "Choppies Mahalapye" ...
     $ district : chr  "Central" "Central" "Central" "Central" ...
     $ town     : chr  "Bobonong" "Letlhakane" "Mahalapye" "Mahalapye" ...
     $ address  : chr  "Moilamba Ward,Cash Bazaar building" "Nkosho Ward,Letlhakane" "Plot 6042, Main Mall, Mahalapye" "Watershed Mall, A1,  Mahalapye" ...
     $ latitude : num  -22 -21.4 -23.1 -23.1 NA ...
     $ longitude: num  28.4 25.6 26.8 26.8 NA ...
     $ date     : Date, format: "2012-09-12" "2007-10-12" ...
     $ registred: chr  "Y" "Y" "Y" "Y" ...
     $ month    : chr  "September" "October" "January" NA ...
     $ year     : num  2012 2007 2012 NA 2012 ...
    


```R
choppies %>% na.omit %>%
group_by(year) %>%
summarise(n = n()) %>%
arrange(desc(n)) %>% head()
```


<table class="dataframe">
<caption>A tibble: 6 × 2</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2005</td><td>10</td></tr>
	<tr><td>2012</td><td> 9</td></tr>
	<tr><td>2010</td><td> 8</td></tr>
	<tr><td>2003</td><td> 7</td></tr>
	<tr><td>2013</td><td> 7</td></tr>
	<tr><td>2018</td><td> 7</td></tr>
</tbody>
</table>




```R
choppies %>% filter(!is.na(year)) %>%
group_by(year, district) %>%
summarise(n = n()) %>%
arrange(desc(n)) %>%
ungroup() %>%
top_n(10)

```

    [1m[22m`summarise()` has grouped output by 'year'. You can override using the
    `.groups` argument.
    [1m[22mSelecting by n
    


<table class="dataframe">
<caption>A tibble: 18 × 3</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>district</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2005</td><td>South-East</td><td>6</td></tr>
	<tr><td>2010</td><td>South-East</td><td>6</td></tr>
	<tr><td>2012</td><td>South-East</td><td>6</td></tr>
	<tr><td>2018</td><td>South-East</td><td>6</td></tr>
	<tr><td>2012</td><td>Central   </td><td>5</td></tr>
	<tr><td>2013</td><td>Kweneng   </td><td>4</td></tr>
	<tr><td>2003</td><td>Southern  </td><td>3</td></tr>
	<tr><td>2006</td><td>Kweneng   </td><td>3</td></tr>
	<tr><td>2013</td><td>South-East</td><td>3</td></tr>
	<tr><td>1999</td><td>South-East</td><td>2</td></tr>
	<tr><td>2003</td><td>South-East</td><td>2</td></tr>
	<tr><td>2005</td><td>Central   </td><td>2</td></tr>
	<tr><td>2010</td><td>Central   </td><td>2</td></tr>
	<tr><td>2010</td><td>North-East</td><td>2</td></tr>
	<tr><td>2011</td><td>Kweneng   </td><td>2</td></tr>
	<tr><td>2011</td><td>South-East</td><td>2</td></tr>
	<tr><td>2015</td><td>Kweneng   </td><td>2</td></tr>
	<tr><td>2018</td><td>Kweneng   </td><td>2</td></tr>
</tbody>
</table>




```R
library(ggplot2)
library(viridis)
```

    Loading required package: viridisLite
    
    


```R
c <- choppies %>% 
filter(!is.na(year)) %>%
select(district,year) 

df <- data.frame(c)
df$district <- factor(df$district)
str(df)

```

    'data.frame':	98 obs. of  2 variables:
     $ district: Factor w/ 11 levels "Central","Chobe",..: 1 1 1 1 1 1 1 1 1 1 ...
     $ year    : num  2012 2007 2012 2012 2005 ...
    


```R
ggplot(df, aes(year, fill=district)) + 
geom_bar() +
ggtitle("Stores registered between 1999 and 2022") +
theme(plot.title = element_text(hjust = 0.5)) +
scale_fill_viridis(discrete = TRUE)
```


    
![png](output_12_0.png)
    

