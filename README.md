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
  
<p align="center">
<img src="images/critical_values.webp" alt="Critical Value" width="50%"/>
</p>

---

### Making Decisions:

There are different methods to make a decision for the given claims.

#### a) Critical Value Method:

 - First, we need to assume an error margin, which we call the significance level (α).
 - Let’s take α = 5%. Based on this α and the type of test, we calculate the Lower Critical Value (LCV) and Upper Critical Value (UCV).
 - Finally, we make a decision by comparing the sample mean (x̄) with the calculated critical values.

<p align="center">
<img src="images/critical_value_method.png" alt="Critical Values" width="50%"/>
</p>

Example : 
- **H<sub>0</sub> :** Total sales = $10 billion
- **H<sub>1</sub> :** Total sales ≠ $10 billion
- α=0.05 , x̄ = 9, σ=2, n=40

Formula

  LCV = μ<sub>0</sub>​ − z<sub>α/2</sub>​⋅(σ / √n)

  ​UCV = μ<sub>0</sub>​ + z<sub>α/2</sub>​⋅(σ / √n)

  We need the z-score that cuts off the upper 2.5% of the distribution.

  - The cumulative probability at that point is 1 − 0.025 = 0.975

  - Looking up in the z-table: 𝑧 = 1.96

    Steps
     - Standard Error (SE) = (σ / √n) = 2 /√40 ≈0.316
     - Critical values
       - Margin of error = z<sub>α/2</sub>​⋅(σ / √n) = 1.96 × 0.316 ≈ 0.619
       - 𝐿𝐶𝑉 = 10 − 0.619 = 9.381
       - UCV=10+0.619=10.619

So, the acceptance region is: [9.381, 10.619]

   - Compare sample mean
     - Since  9<9.381, it falls outside the acceptance region.
     - Decision: Reject H<sub>0</sub>
  

---
 #### b) P-Value Method:

The p-value is the probability of obtaining a test statistic at least as extreme as the one observed, assuming the null hypothesis is true.

- A high p-value indicates strong evidence to fail to reject H<sub>0</sub>.

- A low p-value (less than the chosen significance level α) provides evidence to reject H<sub>0</sub>.

Steps
- Calculate the Z-score for the sample mean.
- Find the p-value from the cumulative probability of the given Z-score using the Z-table.
- For a two-tailed test, multiply the p-value by 2.
- Decision rule: If  p≤α, reject H<sub>0</sub>; otherwise, fail to reject H<sub>0</sub>.
  
<p align="center">
<img src="images/p_value_method.png" alt="P-Value Method" width="50%"/>
</p>


Example : 
- **H<sub>0</sub> :** Total sales ≤ $10 billion
- **H<sub>1</sub> :** Total sales > $10 billion
- α=0.05 , x̄ = 9, σ=2, n=40

Formula

  Z-Score  = (x̄ -  μ<sub>0</sub>​) / (σ / √n)
  
  Steps
  
   - Standard Error (SE) = (σ / √n) = 2 /√40 ≈0.316
   - Z -Score : (9 - 10) / (0.316) ≈−3.16
   - Find cumulative probability (From the Z-table):
     - P(Z<−3.16)≈0.0008
   - Since it’s a two-tailed test:
     - p-value=2×0.0008=0.0016
   - Compare with α
     - p=0.0016<0.05
   - Decision: Reject H<sub>0</sub>
   ​
---
 #### b) T - Distribution:
 
It is also referred to as the Student’s t-distribution.

The t-distribution is generally used when the population standard deviation is unknown, and we estimate it using the sample standard deviation. It is especially useful for small sample sizes, as it accounts for the extra uncertainty introduced by estimating σ

- Use Z-test / P - Value : when population σ is known.

- Use T-test: when population σ is unknown, and you estimate it with the sample standard deviation s

Formula
t = (x̄ -  μ<sub>0</sub>​) / (S / √n)

Steps:
- Calculate the test statistic (t-score)
- Find degrees of freedom (df) = (n-1)
- Determine the critical value(s) from the t-table (based on α, one-tailed or two-tailed, and df)
- Decision rule

 - If ∣t∣>t <sub>critical</sub>, reject H <sub>0</sub>.
 - Otherwise, fail to reject H <sub>0</sub>.

<p align="center">
  <img src="images/t-distribution.png" alt="T - Distribution" width="45%"/>
  <img src="images/T-table.png" alt="T - Table" width="45%"/>
</p>

Example:

A company claims the average delivery time is 30 minutes. You take a random sample of 25 deliveries, and the results show:

- Sample mean (x̄) = 32 minutes

- Sample standard deviation (s) = 4 minutes

- Significance level (α) = 0.05

Steps : 
H<sub>0</sub>​:μ=30
H<sub>1</sub>​:μ=30
- Test statistic (t-score)
  - t =   (x̄ -  μ<sub>0</sub>​) / (S / √n) = (32−30)/(4 / √25) = 2.5
- df : n-1 = 24
- Critical value from t-table
  - At α=0.05 (two-tailed) and df=24:
     - t<sub>0.025,24</sub>​≈2.064
- Decision : Since t=2.5>2.064, we reject H<sub>0</sub>
