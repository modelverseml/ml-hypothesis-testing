# ML Hypothesis Testing

Have you ever come across p-values, t-statistics, or F-values while building regression or logistic models and wondered what they actually mean? Do they impact the model’s performance? Why do people often suggest removing features with a p-value greater than 5%?

All of these questions tie back to hypothesis testing. In this discussion, we’ll break down these concepts step by step and explore them in depth.

## What is Hypothesis Testing?

In statistics and machine learning, we often estimate population parameters (like means, variances, or regression coefficients) using sample data. But how do we know whether these estimates truly reflect the population? Can we trust them?

That’s where hypothesis testing comes in—it provides a structured way to test assumptions, validate results, and decide whether our findings are statistically significant or just due to random chance.


## Steps in Hypothesis Testing  

The basic steps in hypothesis testing begin with two statements:  

- **H<sub>0</sub> (Null Hypothesis):** The starting assumption  
  *(always written with =, ≤, or ≥)*  

- **H<sub>1</sub> (Alternative Hypothesis):** The opposite of the initial assumption  
  *(always written with ≠, >, or <)*  


### Example  

Let’s say Amazon sales in **July 2025** were claimed to be **is $10 billion**.  

- **H<sub>0</sub> :** Total sales = $10 billion  
- **H<sub>1</sub> :** Total sales ≠ $10 billion  

Here, we have set up a hypothesis about our claim.

When testing hypotheses, there are only two possible outcomes:  

- **Reject the Null Hypothesis (H<sub>0</sub>)**  
- **Fail to Reject the Null Hypothesis (H<sub>0</sub>)**  

**Important**: There is **no such thing as “accepting” the null hypothesis**.  
We can only say that we **do not have enough evidence to reject it**.  

--- 
### Critical Values and Test Types  

Let’s say our **sample valuation** comes out to be **$9 billion**.  
Since it’s based on a sample, there’s always some error. Assume the error margin is **± $1 billion**.  

That means our possible **population range** could be between **$7 billion and $10 billion**.  

### Critical Values  

When we test a claim, we define **critical values**:  

- **LCV (Lower Critical Value)**  
- **UCV (Upper Critical Value)**  

These values act as **boundaries** that help us decide whether to reject the null hypothesis.  


### Two-Tailed Test (≠ case)  

If our claim is an **equation or equality** (e.g., *H<sub>0</sub>: Sales = $10B*),  
we are interested in **both directions** (greater or smaller than the claim).  

- **Reject H<sub>0</sub>** if the observed value lies **below LCV** or **above UCV**.  

### One-Tailed Test (≤ or ≥ case)  

If our claim is **one-sided**, then we only care about **one direction**.  

- **Left-tailed test (≤)** → Reject H<sub>0</sub> if observed value < LCV.  
- **Right-tailed test (≥)** → Reject H<sub>0</sub> if observed value > UCV.  

![Critical Values](images/critical_values.webp)
---

