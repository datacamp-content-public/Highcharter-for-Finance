---
title: Insert title here
key: cc9767f391d9266e7fb9b1e7fbe28dc0

---
## Data Frames / Tibbles

```yaml
type: "TitleSlide"
key: "8d2840d66f"
```

`@lower_third`

name: Jonathan Regenstein
title: Director Finance Services RStudio


`@script`
Welcome to our chapter on data frames and tibbbles, which is another name for a data frame that you will hear in the R community. If data frames and tibbles are new to you, I recommend having a quick look at the "Data Frames" lesson from "Introduction to R".  Tibbles have a different structure than XTS objects such as the one we visualized in the last chapter and we will use a different highcharter code flow to chart them.  Before we do that, though, let's review the tibble that holds data for one  ETF, the price history of SPY.


---
## Tibble of SPY Price History

```yaml
type: "FullImageSlide"
key: "9004953abf"
```

`@part1`
![etf_tibble](https://assets.datacamp.com/production/repositories/3344/datasets/c8c1bb21452433a983ceca40a296d8657fb09075/Screen Shot 2018-08-07 at 1.15.04 PM.png)


`@script`
Have a look at the tibble and notice it has 3 columns: a column called date that holds the date of each observation, a column called 'ETF' that holds the name of the ETF, a column called price that holds the price.  When we visualize this tibble with highcharter (or indeed any data vis library), we need to explicitly tell highcharter which column to use for our x axis data and which for our y axis data. It won't 'just know' that date goes on the x-axis because sometimes it won't.  If, for example, this weren't a time series, there might not be a column called date.


---
## Tibble v. XTS

```yaml
type: "TwoColumns"
key: "ac8a678a7c"
```

`@part1`
ETF Tibble data

![etf_tibble](https://assets.datacamp.com/production/repositories/3344/datasets/c8c1bb21452433a983ceca40a296d8657fb09075/Screen Shot 2018-08-07 at 1.15.04 PM.png)

- Has a date column

How will we tell highcharter to put date on the x axis?


`@part2`
ETF XTS data

![](https://assets.datacamp.com/production/repositories/3344/datasets/104030b8229d54aca04b50b951fdea19eaceda45/Screen Shot 2018-08-07 at 1.25.37 PM.png)

 - No date column


`@script`
Here we are looking at the tibble of price data and the xts of price data. Recall the previous chapter when we passed the xts object to highcharter. It has no date column - the dates are held in the index and we did NOT tell highcharter that the index went on the x-axis. Highcharter just knew to use the index. This is a huge difference between xts financial time series and tibble financial time series. With xts, we pass in the object and highcharter knows to put the index on the x-axis. With tibbles we have to tell highcharter to put the 'date' column on the x-axis.  So, how do we tell highcharter this information about the x and y axis?


---
## hchart () and `hcaes()` steps

```yaml
type: "FullCodeSlide"
key: "0d7cf18ad3"
```

`@part1`
1. `hchart()` starts the highcharter flow
2. pass it our tibble: `hchart(spy_tibble...)`
3. use `hcaes` to set x and y axis data
4. hcaes = highcharter + aesthetic
5. 
`hchart(etf_tibble, hcaes(x = date, y = price))`
6. How does hchart know we want a line chart? `type = "line"`


`@script`
The way to tell highcharter which column to use for the x-axis and y-axis is with the `hcaes()` function, which is similar to the `aes` function from `ggplot`.  Let's look at the code flow. We first call the `hchart()` function to start the highcharter code flow. Then we pass it `spy_tibble`. Now highcharter  knows what data object to work with, but it doesn't know which column to use for the x-axis data and which for the y-axis data. We communicate that with hcaes(x = date, y = price).  Now highcharter is aware that date goes on the x-axis and price goes on the y-axis. How does it know we want a line chart? We use type = "line", and we will see later how that let's us construct different types of charts. Note that this hchart-hcaes code flow requires us to be more explicit than we were with the xts object, but we will see how it can be more flexible and efficient for charting tidy tibbles that has for example all 3 ETFs price data. First though, let's look at the tibble to hchart to hcaes code flow and results.


---
## hchart() example

```yaml
type: "TwoColumns"
key: "744163bf3d"
```

`@part1`
```
hchart(spy_tibble,    
       hcaes(x = date, 
             y = price)
       type =  "line")
```


`@part2`
![](https://assets.datacamp.com/production/repositories/3344/datasets/0c63e89d24243d8eb06db8c3da0cc7f31d8b7c72/Screen Shot 2018-08-07 at 2.12.05 PM.png)


`@script`
Again, we start with hchart, pass in our tibble, type="line", and call hcaes(x=date, y =price)). Look closely at the x and y axis, notice that date is on the x-axis.


---
## Title, subtitle, axis labels: same as xts

```yaml
type: "TwoColumns"
key: "678d3df8db"
```

`@part1`
```
hchart(spy_tibble,
       hcaes(x = date, 
             y = price),
       type = "line",
       color = "green") %>% 
  hc_title(text = "SPY ETF") %>% 
  hc_subtitle(text = "price") %>% 
  hc_yAxis(labels = 
           list(format = "${value}"))
```


`@part2`
![](https://assets.datacamp.com/production/repositories/3344/datasets/e6502d80a9b5943d40292489473421e464b5f821/Screen Shot 2018-08-07 at 5.44.02 PM.png
)


`@script`
We can change the color with color = "green", and add a title, subtitle, and dollar sign label the same way as we did in the previous chapter.


---
## Let's visualize a tibble!

```yaml
type: "FinalSlide"
key: "b8219c4582"
```

`@script`
Alright, let's put this into practice and visualize a tibble.

