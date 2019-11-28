---
title: "Factorial design 101"
date: 2019-08-03
tags: [Experimental Design, A/B Testing]
excerpt: "A deep dive into an alternative to A/B testing "
mathjax: True
header:
  image: "/images/lab_experiment.jpg"
---

## Motivation & Simple Example:



A/B testing is the gold standard for quantifying the effect of a treatment. Some proportion of your sample is given one treatment and the remaining experimental units are given a different treatment. Often the second treatment is the control group where nothing is changed.



A/B testing is what we call a randomized controlled trial with one **factor** and two **levels**. That is a fancy way of saying that we are varying one aspect and have two different quantities which we are testing. For example, suppose one was interested in whether Aspirin helps to prevent heart attacks. We would give the test group a dose of Aspirin and the holdout group a placebo. In this example, the factor is Aspirin and the two levels are 325mg and 0mg.

| Experimental Group      | Treatment         | Control  |
| ------------- |:-------------:| -----:|
| 1      | Yes | No |
| 2     | No      |   Yes |


```

  Experimental_Group Treatment Control
                  1       Yes      No

                  2        No     Yes

```



However, what if we were interested in looking at the effect of not only Aspirin but also Lipitor on preventing heart attacks. What we could do is run two separate A/B tests each testing the drugs independently. However, this would require double the sample size of our original A/B test. A better solution is an experimental technique called a factorial design.


| Experimental Group      | Received Aspirin         | Received Lipitor  |
| ------------- |:-------------:| -----:|
| 1      | Yes | Yes |
| 2     | Yes      |   No |
| 3      | No | Yes |
| 4     | No      |   No |


```

##   Experimental_Group Received_Aspirin Received_Lipitor

## 1                  1              Yes              Yes

## 2                  2              Yes               No

## 3                  3               No              Yes

## 4                  4               No               No

```



Each of the experimental units would be randomly assigned to one of the four groups. This is known as a 2 x 2 factorial design because there are two **factors**(Aspirin & Lipitor) which each have 2 **levels** (either taking the drug or the placebo).



What we have essentially done is combined two unrelated experiments into one. The beauty of a factorial design is the ability to combine two unrelated experiments into one with only a slight increase in overall cost [1].  Additionally, in a factorial design one can test for the interaction between treatments, because you have one set of experimental units taking both Aspirin and Lipitor at the same time.



## Relevant Example



Lets say we are trying to evaluate five different outreach and incentive options in a consumer facing marketing campaign. For example, we want to evaluate Phone, direct mail, SMS, email and gift card incentives on a specific behavior change. We don't only want to see the **main** effects that each of the outreach options has on the outcome, but also the **interaction** effects between the different outreach options. In order to do so, we are going to need to use a **factorial design**!



This is what we call a $$ 2^5 $$ factorial design because it has five different **factors** with two **levels** each. The $$ 2^5 $$ notation is convenient because it quickly tells us how many different treatment combinations we are going to need. In this case we will need 32 distinct treatment combinations in order to evaluate all five main effects, ten 2-factor effects, ten 3-factor effects, five 4-factor effects and one 5-factor effect. We can illustrate the design in a table.



For example, experimental group #1 will receive Phone, Direct Mail, SMS, Email and a Gift Card. While group #8 will only receive Phone and Direct Mail.


| Experimental Group      | Phone     | Direct Mail  | SMS | Email | Gift Card|
| ------------- |:-------------:| -----:| -------:| -------:| -------:|
| 1      | Yes | Yes | Yes | Yes| Yes|
| 2      | Yes | Yes | Yes | Yes| No |
| 3      | Yes | Yes | Yes | No | Yes|
| 4      | Yes | Yes | Yes | No | No |
| 5      | Yes | Yes | No | Yes| Yes|
| 6      | Yes | Yes | No | Yes| No|
| 7      | Yes | Yes | No | No | Yes|
| 8      | Yes | Yes | No | No| No|
| 9       | Yes | No | Yes | Yes| Yes|
| 10      | Yes | No | Yes | Yes| No |
| 11      | Yes | No | Yes | No | Yes|
| 12      | Yes | No | Yes | No | No |
| 13      | Yes | No | No | Yes| Yes|
| 14      | Yes | No | No | Yes| Yes|
| 15      | Yes | No | No | No | Yes|
| 16      | Yes | No | No | No | No|
| 17      | No | Yes | Yes | Yes| Yes|
| 18      | No | Yes | Yes | Yes| No|
| 19      | No | Yes | Yes | No | Yes|
| 20      | No | Yes | Yes | No | No |
| 21      | No | Yes | No | Yes| Yes|
| 22      | No | Yes | No | Yes| No|
| 23      | No | Yes | No | No | Yes|
| 24      | No | Yes | No | No | No |
| 25      | No | No | Yes | Yes| Yes|
| 26      | No | No | Yes | Yes| No |
| 27      | No | No | Yes | No | Yes|
| 28      | No | No  | Yes | No | No |
| 29      | No | No | No | Yes| Yes|
| 30      | No | No | No | Yes| No|
| 31      | No | No | No | No | Yes|
| 32      | No | No | No | No | Yes|


```

##    Experimental_Group Phone Direct_Mail SMS Email Gift_Card

## 1                   1 Yes         Yes Yes   Yes       Yes

## 2                   2 Yes         Yes Yes   Yes        No

## 3                   3 Yes         Yes Yes    No       Yes

## 4                   4 Yes         Yes Yes    No        No

## 5                   5 Yes         Yes  No   Yes       Yes

## 6                   6 Yes         Yes  No   Yes        No

## 7                   7 Yes         Yes  No    No       Yes

## 8                   8 Yes         Yes  No    No        No

## 9                   9 Yes          No Yes   Yes       Yes

## 10                 10 Yes          No Yes   Yes        No

## 11                 11 Yes          No Yes    No       Yes

## 12                 12 Yes          No Yes    No        No

## 13                 13 Yes          No  No   Yes       Yes

## 14                 14 Yes          No  No   Yes        No

## 15                 15 Yes          No  No    No       Yes

## 16                 16 Yes          No  No    No        No

## 17                 17  No         Yes Yes   Yes       Yes

## 18                 18  No         Yes Yes   Yes        No

## 19                 19  No         Yes Yes    No       Yes

## 20                 20  No         Yes Yes    No        No

## 21                 21  No         Yes  No   Yes       Yes

## 22                 22  No         Yes  No   Yes        No

## 23                 23  No         Yes  No    No       Yes

## 24                 24  No         Yes  No    No        No

## 25                 25  No          No Yes   Yes       Yes

## 26                 26  No          No Yes   Yes        No

## 27                 27  No          No Yes    No       Yes

## 28                 28  No          No Yes    No        No

## 29                 29  No          No  No   Yes       Yes

## 30                 30  No          No  No   Yes        No

## 31                 31  No          No  No    No       Yes

## 32                 32  No          No  No    No        No

```





The table was designed in such a way to maintain a fundamental principle of experimental design, **orthogonality**. A design is orthogonal if the dot product between each combination of every factor is equal to 0. For example, the dot product between the Phone vector and the Direct Mail vector is equal to 0. You can check the arithmetic on your own by summing the product of each row between the Phone and Direct Mail columns. **Orthogonality** guarantees that the effect of one factor or interaction can be estimated separately from the effect of any other factor or interaction in the model [2].



Once we have created the design table, we are going to need to assign the members into each of the different combinations. When we do so, we need to make sure we are following another fundamental principle of experimental design, **balance**. Balance in this context is when each experimental group has the same number of members in it. One of the main benefits of a balanced design in comparison to an unbalanced design is that it will have a higher statistical power.



## Fractional Factorial Designs



In the previous example we had a $$ 2^5 $$ design with 32 different treatment combinations. We were able to measure all the **main** effects and every possible interaction effect. However, what if we weren't interested in measuring all the **interaction** effects? Or, what if we don't have the resources to conduct 32 different treatment combinations? We can solve these problems by using a modification of a factorial design called a fractional factorial design.



Lets say we only have the resources to have 16 different treatment combination in the previous example. We can use a $$ 2^{5-1} $$ design which will require the 16 different treatment combinations that we can do. In general, a $$ 2^{k-p} $$ design is a

$$ \frac{1}{2^p} $$ fraction of a $$ 2^k $$ design. Which in turn has $$ 2^{k-p} $$ treatment combinations. In our case, a $$ 2^{5-1} $$ design is $$ \frac{1}{2} $$ fraction of our $$ 2^5 $$ full factorial design. In order to build a fractional factorial design, we are going to have to sacrifice being able to observe one or more of our effects in order to reduce the number of experimental groups. We are going to set the Gift Card value = Phone x Direct Mail x SMS. For example, to calculate the value for Gift Card in the first experimental group we will multiply 1 x 1 x 1 to get 1. For the third experimental group we would multiply 1 x 1 x -1 to get -1.



We now say that effect of the gift card is **aliased** with the three-way interaction effect between Direct Mail, SMS and Emails. In this design we cannot distinguish between the **main** effect of a gift card incentive and the three-way **interaction** effect between Direct Mail, SMS and Emails.



In this design the **main** effects of Phone, Direct Mail, SMS and Gift Cards are able to be estimated if all combinations of three-way interaction effects out of Phone, Direct Mail, SMS and Gift Cards are negligible. In summary, we can now only observe the following 15 effects:



1. Phone

2. Direct Mail

3. SMS

4. Email

5. Gift Card

6. Phone x Direct Mail

7. Phone x SMS

8. Direct Mail x SMS

9. Phone x Email

10. Direct Mail x Email

11. SMS x Email

12. Gift Card x Email

13. Phone x Direct Mail x Email

14. Phone x SMS x Email

15. Direct Mail x SMS x Email


Lets illustrate the **fractional factorial design** in a similar table as the full factorial design:





```

##    Experimental_Group Phone Direct_Mail SMS Email Gift_Card

## 1                   1 Yes         Yes Yes   Yes       Yes

## 2                   2 Yes         Yes Yes    No       Yes

## 3                   3 Yes         Yes  No   Yes        No

## 4                   4 Yes         Yes  No    No        No

## 5                   5 Yes          No Yes   Yes        No

## 6                   6 Yes          No Yes    No        No

## 7                   7 Yes          No  No   Yes       Yes

## 8                   8 Yes          No  No    No       Yes

## 9                   9  No         Yes Yes   Yes        No

## 10                 10  No         Yes Yes    No        No

## 11                 11  No         Yes  No   Yes       Yes

## 12                 12  No         Yes  No    No       Yes

## 13                 13  No          No Yes   Yes       Yes

## 14                 14  No          No Yes    No       Yes

## 15                 15  No          No  No   Yes        No

## 16                16  No          No  No    No        No

```



It is important to note that we could also have a $$ 2^{5-2} $$ design if we only had the resources for eight treatment combinations. In general, the more you reduce your factorial design to the less affects you can observe. This technique can also be used when you have more than two **levels** per factor, I.e. a $$ 3^{5-2} $$ can also be done. This would reduce the number of treatment combinations from 243 down to 27 while simultaneously reducing the number of affects you are able to observe.



## Calculating Treatment Effects



Once we have run our experiment, we need to calculate the treatment effects. Remember, that is the whole reason why we are running an experiment in the first place! Lets use a simple example of a $$ 2^3 $$ fractional design. We will have three treatments and an outcome variable which will be behavior change percentage.





```

##   Experimental_Group Phone Email SMS Behavior_Change_Percent

## 1                  1 Yes   Yes Yes                      12

## 2                  2 Yes   Yes  No                       4

## 3                  3 Yes    No Yes                       9

## 4                  4 Yes    No  No                       5

## 5                  5  No   Yes Yes                       7

## 6                  6  No   Yes  No                       8

## 7                  7  No    No Yes                       6

## 8                  8  No    No  No                       1

```



From this table, how would we calculate the **main** effects of Phone, Email and SMS on behavior change? To calculate the effect of Phone we will compare each group that got an Phone with its counterpart that didn't but had the same Email and SMS levels. Then we will average all the of the difference between the pairs to get an overall main effect.



Lets look at how to calculate the main average **treatment** effect of Phone. Our first step will be to figure out which experimental groups will be paired together. In this case, the pairs will be: [1, 5], [2, 6], [3, 7], [4, 8]. The only treatment that differs within each of the pairs is whether they received Phone.  Now we will calculate the differences in our outcome variable within each of the pairs and then average the results.


```
Pair          Difference in Outcome

Groups 1 & 5   12% - 7% = 5%

Groups 2 & 6   4% - 8% = -4%

Groups 3 & 7   9% - 6% = 3%

Groups 4 & 8   5% - 1% = 4%

```



Thus, the **main** average treatment effect of Phone is mean(5% - 4% + 3% + 4%) = 2%. The process to calculate any of the other **main** average treatment effects is the same.



However, how would we calculate the interaction effect between Phone and email? First, we will look at the effect of emails when Phone is present. The average treatment effect of emails given Phone is present is: $$ \frac{12 + 4}{2} - \frac{9 + 5}{2} = 8 - 7 = 1% $$. Now we will look at the effect of emails when Phone isn't present. The average treatment effect of emails given Phone isn't present is: $$ \frac{7 + 8}{2} - \frac{6 + 1}{2} = 4% $$.



The interaction effect is half the difference between the two numbers we just calculated. Therefore, the interaction effect between Phone and Email is $$ \frac{1 - 4}{2} $$ = -1.5%. Calculating the other **interaction** effects is done in a similar fashion.



## Power Analysis for Factorial Designs



As mentioned earlier, a factorial design allows us to observe both main effects and interaction effects. In a $$ 2^3 $$ factorial design we have three main effects that we can observe. The question becomes, how do we determine which effect size to use for the experiment?



The first step is to determine the expected effect size of each of the main effects. For example, imagine a $$ 2^3 $$ design with expected effect sizes of 0.1, 0.3, and 0.8 for the **main** effects. When calculating the sample size required for the experiment, we would calculate it based on the smallest effect size. By doing this, we will be able to have adequate power across all the effects.



Now lets suppose we want to add a treatment to our experiment. Lets compare what would happen to the sample size required in an RCT vs a factorial design. Imagine after doing a power analysis we determine that an RCT with two treatments requires 500 subjects. If we wanted to add another treatment, we would need to add 250 more subjects to the experiment.



However, in a factorial design if the expected effect size of an added treatment is higher than the lowest expected effect size currently in the experiment then we would not need to increase the sample size. Lets take a step back here and truly appreciate the power of a factorial design (pun intended). In general, if we have an RCT with $$ P $$ individuals in each arm, when we add another treatment, we would have to add $$ P $$ individuals to the experiments. In contrast, seldom would we have to add subjects to a factorial experiment when adding a treatment.



## Advantages of Factorial Designs



* Can study interaction effects between different treatments.



* Is more efficient due to the smaller sample size required (up to one-half) compared with two separate multi-arm parallel trials [3].



* Potentially decreased costs due to smaller sample sizes required when compared to two separate multi-arm parallel trials [3].



## Downsides of Factorial Designs



* More complex experiment design which requires more time of a data scientist.



* More complex analysis which also requires more time as a data scientist.



* Potential for negative interaction effects.

  +  For example, we wouldn’t use a factorial design if we wanted to determine the effects of Potassium Chloride and Spironolactone because of their known negative interaction effects.



## Further Resources



* https://www.itl.nist.gov/div898/handbook/pri/section3/pri3332.htm



* https://www.methodology.psu.edu/ra/most/factorial/



## Special Thanks



Special thanks to Professor Mark Ebden who taught my experimental design course at the University of Toronto. A lot of this content was adapted from his lecture slides. Additionally, special thanks to Professor Nathan Taback who helped to develop a significant amount of the course's content.



## Bibliography



[1]- Hennekens, Charles H. A Randomized Trial of Aspirin and -Carotene among U.S. Physicians. Preventive Medicine, Academic Press, 9 Feb. 2004, www.sciencedirect.com/science/article/pii/0091743585900313.



[2] Orthogonal Designs. Minitab, support.minitab.com/en-us/minitab/18/help-and-how-to/modeling-statistics/doe/supporting-topics/basics/orthogonal-designs/.



[3] Nikolaos Pandis, Tanya Walsh, Argy Polychronopoulou, Christos Katsaros, Theodore Eliades, Factorial designs: an overview with applications to orthodontic clinical trials,European Journal of Orthodontics, Volume 36, Issue 3, June 2014, Pages 314320,https://doi.org/10.1093/ejo/cjt054



[4] Introduction to Factorial Experimental Designs. The Methodology Center, www.methodology.psu.edu/ra/most/factorial/.
