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

- The fundamental theoretical rule guiding queueing theories is Little's Law, which was established by John Little, stating that the long-term average number of customers in a stable queueing system ***L***, is equal to the long-term average effective arrival rate, **λ**, multiplied by average(arithmetic meaning) time a customer spends in system, ***W***; or, in mathematical expression 

<p align="center">
L = λW.
<p/>

- The remarkable characteristic of this rule is that, it doesn't depend on specific distribution of arrival distribution, service distribution, service order, or almost everything else in this system. This intuitive law could provide suggestive information about average customer flow in a long run.

### 2.2 Queueing Theory for Airport Security Checkpoint Passenger Flow

- With basic knowledge of queueing theory, we need to specify characteristics of queues in airport security checkpoint to establish concrete model for our project. In this attempt, we mainly depend on data of waiting point in Chicago O'hare Airport Terminal 5, from 2016.1.1 to 2016.12.31, and come up with following several important traits of our queueing system.

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

<p align="center">
<img src="/images/Rplot.png" width = "500">
</p>

- Disregarding the outlier of extremely low number of passengers arriving — which usually occurs near the beginning of operation of airport at 4AM or closing of airport operation at 1AM — we can witness an Exponential Distribution of arrival rate, with arrival of passengers around 200-300 in one hour happening most, and number of occurrences deteriorating as range of passengers gradually increasing until 2500+.

- For further analysis, we establish the expression for exponential distribution as

<p align="center">
<img src="/images/exp.png" width = "180">
<p/>
  
- Then we run a non-linear least squares regression, getting following result:

<p align="center">
<img src="/images/R output.png" width = "600">
</p>

- Based on information resulted from regression, we figure out that rate of occurrence of
arriving every x thousands people is λexp^(-λx), with rate of arrival **λ = 0.03404**.

#### 2.2.2 Distribution of Passenger Arrival Over Time

- Even though in traditional queueing theory, only certain merit of distribution, such as Exponential Distribution or Erlang Distribution, is assumed and there is basically no conscription of distribution of passengers’ arrival across time, in our scenario, time plays a significantly important role in describing certain passengers’ coming to airport.

- The reason for time’s importance falls on the fact that, unlike in other scenario where customers generally make their choice of participating in a certain service arbitrarily, passengers in airport usually decide when and whether to go to airport depending on their flight information. Since the arrangement of flights in an airport follows certain pattern, the arrival of passengers also exhibits certain trend over time in a day, as shown in following graph:

<p align="center">
<img src="/images/Average number of passengers.png" width = "500">
</p>

- The conspicuous bell-shape graph tells us that, the number of passengers arriving airport security checkpoint reaches the peak around 14pm-15pm and 17pm-18pm every day, and that relatively less people coming to airport early in the morning or late in the evening.

- In spite of lesson about distribution of passengers in a day, which guides us in data generating later for our examination of model, this bell-shape graph also precludes us from utilizing Little’s Law in predicting passengers flow in airport security checkpoint. The reason is that, one underlying presumption of Little’s Law is that every single customer makes decision of joining the queue for service or not based merely on current length of waiting line and assumed efficiency of server, and once a customer face the situation where waiting queue is too long or servers act in an exceedingly dilatory characteristic, he/she will generally choose come later of not participate in the service at all.


- However, this graph shows that, due to passengers seldom give up their booked flights or endorse tickets because of long security line, even though in some rush hours security checkpoints are extremely crowded, people will still flow into waiting lines and deteriorate the condition in checkpoints. Based on this realization, we have to deviate from Little’s Law, and construct some other approaches in estimating passengers flow.

#### 2.2.3 Service Efficiency

- The service capacity is another crucial element in determining length of waiting lines in airport security checkpoint. We utilize rate of passengers waiting for extremely long time (over 45 minutes) in a certain time interval as the indicator of efficiency of service in airport security checkpoint. Based on same data resource, we construct following graphs:

<p align="center">
<img src="/images/flow vs extreme.png" width = "300"><img src="/images/rate vs time.png" width = "300">
</p>

- According to information stated above, we could come up with the idea that efficiency of service in airport security checkpoint is basically exogenous to queueing system. So in our modeling, we grant an arbitrary value to service efficiency, which is generated from analysis on data collected.

#### 2.2.4 Service Discipline

- Despite occasional situation where some passengers who are rushing for their flights that will take off in several minutes, and other passengers allow them to jump into first place in a queue, the service discipline in airport security checkpoint is generally "First In First Out" (FIFO).

- Another special situation is that, when one passenger is suspicious of carrying certain dangerous items, either in his/her carried-on baggage or in his/her own body, he/she will undergo second-round examination and re-pass machine scanner. In our model, to simplify this scenario, we just double the time needed for suspicious passengers to pass security checkpoint, and do not change service discipline for these specific cases.

### 2.3 Modeling

- Relying on knowledge of characteristics of queueing system in airport security checkpoint, we construct a mathematical model in estimating passengers flow in any given time period. We mainly focus on estimating number of passengers that security checkpoint has to serve in each time interval, and predicting number of passengers waiting extremely long time in every period. The process is as following:

  - Separate a day into several equal time periods (100 in our case), generate arrival rate of passengers for every single period and make sure distribution of arrival rate following Exponential Rate, and then rearrange these rate across time periods to simulate bell-shape distribution of passengers over time in a day. Number of passenger flowing into airport in period t is denoted as I(t).

  - Denote P(t) as number of passengers that security checkpoint needs to serve, and S(t) as efficiency of checkpoint in period t, where each S(t) is randomly generated within a certain range. Let R(t) represent number of passengers waiting in line for extremely long time in each period, and establish the relationship as following: 
  
<p align="center">
<img src="/images/R(t).png" width = "180">
</p>

   - The amount of passengers that security checkpoint has to check equals to the sum of incoming passengers in this period, and passenger experiencing long waiting in last period (due to their extremely long waiting time in line, we could assume that these passengers have to wait until another period before getting safety checking). Thus, we can come up with following series of equations:



  


<p align="center">
<img src="/images/1.png" width = "300">     <img src="/images/2.png" width = "300">
</p>

<p align="center">
<img src="/images/3.png" width = "300">     <img src="/images/4.png" width = "300">
</p>

## 3 Procedural Model and Modifications
### 3.1 Analysis of Current TSA Airport Security Checking Procedure
#### 3.1.1 Generalization and Simplification

<p align="center">
<img src="/images/model1.png" width = "350">     <img src="/images/process1.png" width = "350">
</p>

#### 3.1.2 Main Reason for Procrastination

### 3.2 Modifications on Current TSA Airport Security Checking Procedure
#### 3.2.1 Modification 1: Bifurcation System

<p align="center">
<img src="/images/model2.png" width = "350">      <img src="/images/process2.png" width = "350">
</p>

#### 3.2.2 Modification 2: Circular Line-up System

<p align="center">
<img src="/images/model3.png" width = "350">      <img src="/images/Process3.JPG" width = "350">
</p>

### 3.3 Comparison of Procedural Models
#### 3.3.1 Theoretical Comparison

<p align="center">
<img src="/images/proc1.png" width = "210"> <img src="/images/proc2.png" width = "210"> <img src="/images/proc3.png" width = "210">
</p>


#### 3.3.2 Empirical Comparison
<p align="center">
<img src="/images/procedure comparison.png" width = "500">
</p>


## 4 Examination on Impact of Cultural Norms
### 4.1 Chinese Cultural Norm —Emphasis on Family
<p align="center">
<img src="/images/Chinese norm.png" width = "500">
</p>

### 4.2 American Cultural Norm — Emphasis on Private Space
<p align="center">
<img src="/images/American norm.png" width = "500">
</p>

### 4.3 Japanese Cultural Norm — Emphasis on Condition of Minorities
<p align="center">
<img src="/images/Japanese norm.png" width = "500">
</p>

## 5 Conclusion

## References
