---
Title: "Waiting in Airport Security Checkpoint: A Perspective from Queueing Theory"
Author: "Chuan (Sophie) Du, Yuan Shen, Fan Wu"
Categories: Contest Project
Date: "1/23/2017"
---

This is the Problem D in **2017 Interdisciplinary Contest In Modeling®**, with original problem title "Optimizing the Passenger Throughput at an Airport Security Checkpoint". My team was finally designted as *Meritorious Winner* (top 10%).

## Summary
- Waiting in airport security checkpoint is a tradition queueing problem in real life. We reflect classical queueing theory, and model passenger flow in security checkpoint based on its main ideas. From reliable data about passenger amount in security checkpoint in each time period, we conduct empirical analysis, and reach the conclusion that passengers’ arrival rate exhibits exponential distribution, and amount of passengers arriving over time in a day shows a bell shape. We incorporate element of incoming passengers, efficiency in checkpoint, and remaining passengers from previous time period, we establish a series of functions, and come up with feasible method in estimating number of passengers demanding service in security checkpoint at each time period of a day.

- Depending on our knowledge of passenger flow, we re-examine current passenger security checking procedure applied by TSA. While guaranteeing the security, we develop two modifications to current procedural model, in order to improve passenger throughout and reduce variance in wait time: the first incorporating into a Bifurcation System, and the second designing a Circular Line-up System. We then compare efficiency of these procedures, and also discuss impact of certain typical cultural norms on their performance.


## 1 Introduction of Airport Security Checkpoint

- Airport security has been significantly enhanced throughout the world nowadays, aiming to keep all passengers safe. However, the long waiting lines at the security checkpoints add much inconvenience to passengers. The high variance in checkpoint lines can be extremely costly to passengers as they waste much time arriving unnecessarily early or wait too long for the unexpectedly long lines, potentially missing their scheduled flights. In order to keep a positive flying experience for passengers by reducing waiting times while guaranteeing the security, we are interested in making several modifications to the current checkpoint equipment and procedures. We need to explore the flow of current checkpoint process and identify the bottlenecks, and also need to figure out the factors which would affect each step of the procedures. Moreover, with the increase quality of security checking procedure, passengers feel their privacy get violated too much. For example, American may sacrifice their waiting time for individual privacy. And a great proportion of the security screening is actually a waste of time for many citizens. Therefore, to analysis the balance between security quality and convenience of passengers are what we are going to analysis below.

## 2 Model for Exploring Passengers Flow

- Monitoring and predicting the flow of passengers in security checkpoint in an airport is the key element assisting in evaluating design of current security check procedure and its modifications. To establish a reliable and referential model for exploring passenger flow, we introduce Queueing theory, the most classical mathematical model in analyzing waiting lines and congestion, and append several important adjustments to this model in order to better simulate virtual scenario in current airport security checkpoints.

### 2.1 Introduction of Queueing Theory

- Originated by research of Agner Krarup Erlang, Queueing Theory has been in prevailing use in telecommunication, transportation, and computing. Basic queueing model consists of several independent yet interplaying parts: 1) the arrival process of customers; 2) the behavior of customers; 3) the service efficiency; 4) the service discipline; 5) the service capacity; 6) the waiting room. In dealing with any single topic, we have to specify these elements according to situation in reality.

- In this theory, the performance measure is flexible, and could be designed with reference to aim of research project. The distribution of waiting time and sojourn time --- the waiting time plus the service time --- of a customer is one of significant guages in judging efficiency of queueing procedure. The distribution of number of customers in the system, both including and excluding the one or those in service, could play a crucial role in exhibiting utilization of queueing system. The distribution of busy period of the server can shed inspiring light on the effectiveness of queueing system in ameliorating congestion and coping with rush-hours.

- The fundamental theoretical rule guiding queueing theories is Little's Law, which was established by John Little, stating that the long-term average number of customers in a stable queueing system ***L***, is equal to the long-term average effective arrival rate, **λ**, multiplied by average(arithmetic meaning) time a customer spends in system, ***W***; or, in mathematical expression ***L = λW***.

- The remarkable characteristic of this rule is that, it doesn't depend on specific distribution of arrival distribution, service distribution, service order, or almost everything else in this system. This intuitive law could provide suggestive information about average customer flow in a long run.

### 2.2 Queueing Theory for Airport Security Checkpoint Passenger Flow

- Security Checkpoint Passenger Flow}
With basic knowledge of queueing theory, we need to specify characteristics of queues in airport security checkpoint to establish concrete model for our project. In this attempt, we mainly depend on data of waiting point in Chicago O'hare Airport Terminal 5, from 2016.1.1 to 2016.12.31, and come up with following several important traits of our queueing system.

#### 2.2.1 Rate of Passenger Arrival

- The first and foremost issue that we tackle with is the arrival process of passengers into airport security checkpoint, and we want to estimate the arrival rate of of certain number of passengers --- the ratio number of occurrences of arrival of certain range of passengers in a given period, to the total number of occurrences. 

- Defining time period as One Hour, partitioning range of passengers in the merit of 0-100, 100-200, 200-300... and so on, and regarding rate of arrival as ratio of number of passengers arriving in a certain periods to total passengers in one day, we analyzed data collected and reach following distribution of arrival rate:

---`R version 3.4.2` Programming---
  
```{r}
#Load Data
range = read.csv('Range.csv', header=TRUE)
rate = read.csv('Rate.csv', header=TRUE)
```

```{r}
x = range$Range
y = rate$Rate
```

```{r}
plot(x , y, col = 1, pch = 16,
     xlab = "Number of Passengers", ylab="Rate of Occurence",
     main="Distribution of Passengers Flow in O'hare Airport",
     xlim=c(0,2800), ylim=c(0,0.12))     
lines(lowess(x,y), col = "blue")
```

---**Output**---
![]({{ "/images/Rplot.png" | "https://github.com/chuandu2/chuandu2.github.io/blob/master/images/Rplot.png"}})






#### 2.2.2 Distribution of Passenger Arrival Over Time
#### 2.2.3 Service Efficiency
#### 2.2.4 Service Discipline

### 2.3 Modeling

## 3 Procedural Model and Modifications
### 3.1 Analysis of Current TSA Airport Security Checking Procedure
#### 3.1.1 Generalization and Simplification
#### 3.1.2 Main Reason for Procrastination

### 3.2 Modifications on Current TSA Airport Security Checking Procedure
#### 3.2.1 Modification 1: Bifurcation System
#### 3.2.2 Modification 2: Circular Line-up System
### 3.3 Comparison of Procedural Models
#### 3.3.1 Theoretical Comparison
#### 3.3.2 Empirical Comparison

## 4 Examination on Impact of Cultural Norms
### 4.1 Chinese Cultural Norm —Emphasis on Family
### 4.2 American Cultural Norm — Emphasis on Private Space
### 4.3 Japanese Cultural Norm — Emphasis on Condition of Minorities

## 5 Conclusion

## References
