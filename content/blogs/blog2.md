---
categories:
- ""
- ""
date: "2017-10-31T22:26:09-05:00"
description: Take a look at what I have been doing in my Data Analytics course!
draft: false
image: bikes-data.png
keywords: ""
slug: my-portfolio
title: My Portfolio
---

The Data Analytics course has been beyond insightful at this point. Not only have we had the opportunity to explore and wrangle real datasets, but we have also been responsible for interpretation and understanding. Learning to analyse and present data effectively helps business students become exceptional professionals. 

# Bike Data

A dataset provided by Santander Bicycles rental shed insights into the changes in bicycles hired over the last five years. The historical data from 2016 to 2021 was compared to a 52-week average of bicycle hires from 2016 to 2019. The three main insights included the growth of the cycle hire industry over the past five years, the radical impact of COVID-19 lock-downs and re-opening, as well as the seasonal nature of bike hires. 

COVID-19 had a significant impact on bike rentals. In the 10th week of 2020, bike hires were at an all-time low, with lock-downs keeping people indoors for months and without a need to move from point A to B. A similar trend was observed in January and February 2021, when the United Kingdom was under a strict lock-down regime. However, the summer months in 2020 had some of the largest consecutive % changes in cycle hiring that the city had seen in years. 
Following is the code utilised to construct the above graph.

```{r Monthly_rental_graph, message = FALSE, error = FALSE}
# Plot the graph
ggplot(new_bike_data, aes(x=(month), group=1))+
  
#Add the ribbons to give colour to the Difference in actual vs expected  
  geom_ribbon(aes(ymin=expected_mean,
                  ymax=expected_mean+down),
                  fill="#CB454A",
                  alpha=0.4)+
  geom_ribbon(aes(ymin=expected_mean+up,
                  ymax=expected_mean),
                  fill="#7DCD85",
                  alpha=0.4)  +
  
#Add the actual and expected rental lines
  geom_line(aes(y = expected_mean), 
            colour ="blue", 
            size = 1, 
            alpha =0.5) + 
  geom_line(aes(y= monthly_mean), 
            size = 0.5, 
            alpha =0.5)+
  
#Create subplots by year  
  facet_wrap(~year)+
  
#Organise and label the graph  
  theme_minimal()+
  labs(x = "", y="Bike rentals", 
       title = "Monthly changes in TfL bike rentals", 
       subtitle="Change from monthly average shown in blue \n 
                  and calculated between 2016-2019", 
       caption = "Source: TfL, London Data Store") + 
  
#Adjust Axis labels to ensure they dont overlap
  theme (axis.text.x = element_text(size=6), 
         axis.text.y = element_text(size=6))
```

