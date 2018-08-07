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
Welcome to our chapter on data frames and tibbbles, where we move to visualizing data that is  in a data frame or a tibble, which is another name for a data frame that you will hear in the R community. If data frames and tibbles are new to you, I recommend having a quick look at the "Data Frames" lesson from "Introduction to R".  We will start by looking at the tibble that holds data for one of our ETFs, the price history of SPY.


---
## Tibble of SPY Price History
  
```yaml
type: "FullImageSlide"
key: "9004953abf"
```


`@part1`
![](https://assets.datacamp.com/production/repositories/3344/datasets/c8c1bb21452433a983ceca40a296d8657fb09075/Screen Shot 2018-08-07 at 1.15.04 PM.png)


`@script`



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
Have a look at the tibble and notice it has 3 columns: a column called date that holds the date of each observation, a column called 'ETF' that holds the name of the ETF, a column called price that holds the price. When we visualize this tibble with highcharter (or indeed any data vis library), we need to explicitly tell highcharter which column is our x axis data and which is our y axis data. It won't 'just know' that date goes on the x-axis because sometimes it won't.  If, for example, this weren't a time series, there might not be a column called date. Recall the previous chapter when we passed the xts object to highcharter. It has no date column - the dates are held in the index and we did NOT tell highcharter that the index went on the x-axis. Highcharter just knew to use the index. This is a huge difference between xts financial time series and tibble financial time series. With xts, we pass in the object and highcharter knows to put the index on the x-axis. With tibbles we have to tell highcharter to put the 'date' column on the x-axis. [xts v. tibble: The data structure drives the visualization code logic].  So, how do we tell highcharter this information about the x and y axis?  [JKR: so, need an image of both an xts and tibble with price history]


---
## X and Y data with `hcaes()` =  highcharter + aesthetic
  
```yaml
type: "FullCodeSlide"
key: "0d7cf18ad3"
```


`@part1`
1. `hchart()` starts the highcharter flow
2. pass it our tibble: `hchart(etf_tibble...)`
3. use `hcaes` to set x and y axis data
4. `hchart(etf_tibble, hcaes(x = date, y = price))`
5. wait, how does hchart know we want a line chart? `hchart(etf_tibble, type = "line", hcaes(x = date, y = price))`


`@script`
The way to tell highcharter which column to use for the x-axis and y-axis is with `hcaes`, which is similar to the `aes` function from `ggplot`.  We first call the `hchart()` function to start the highcharter code flow. Then we pass it `etf_tibble`. Now highcharter  knows what data object to work with, but it doesn't know which column is the x-axis data and which is the y-axis data. We communicate that with hcaes(x = date, y = price).  Now highcharter is aware that date goes on the x-axis and price goes on the y-axis. How does it know we want a line chart? We use type = "line", and we will see later how that let's construct different types of charts. Note that this hchart-hcaes code flow requires us to be more explicit than we were with the xts object, but we will see how it can be more flexible and efficient for charting tidy tibbles that has for example all 3 ETFs price data. First though, let's practice the tibble to hchart to hcaes code flow.


---
## Final Slide
  
```yaml
type: "FinalSlide"
key: "b8219c4582"
```


`@script`


