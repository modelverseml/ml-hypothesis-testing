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
<img src="images/critical_value_method.png" alt="Critical Values" height = "350" width="45%"/>
<img src="images/z-table.png" alt="Standard Deviation Values" height="350" width="45%"/>
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
<img src="images/p_value_method.png" alt="P-Value Method" height="350" width="45%"/>
 <img src="images/z-table.png" alt="Standard Deviation Values" height="350" width="45%"/>
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
 #### c) T - Distribution:
 
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
  <img src="images/t-distribution.png" alt="T - Distribution" height="350" width="45%"/>
  <img src="images/T-table.png" alt="T - Table" height="350" width="45%"/>
 
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

---
d) Chi-Square Test (Goodness-of-Fit / Categorical counts) :

compare observed counts in categories to expected counts , if observed counts are much different from expected, reject the assumed distribution.

Formula

χ<sup>2</sup> = ∑( (O−E)<sup>2</sup>/E​ )
- E → Expected
- O → Observed

<p align="center">
<img src="images/Chi-square.webp" alt="Chi Square Distribution" height="350" width="45%"/>
 <img src="images/Chi-square_distribution_table.webp" alt="Chi Squared Values" height="350" width="45%"/>
</p>


Example : 
claim : We want to test if a coin is fair (i.e., probability of heads = 0.5)

Number of times coin flipped = 100

Steps : 

H<sub>0</sub> : p = 0.5
H<sub>1</sub> : p ≠ 0.5

Let say after fliping 100 times observed is 60 heads , 40 tails

 - Observed Heads (O<sub>1</sub>) = 60

 - Observed Tails (O<sub>2</sub>) = 40

Expected :
 - Expected Heads (E<sub>1</sub>) = 50
 - Expected Heads (E<sub>2</sub>) = 50


Steps : 
- χ<sup>2</sup> = ∑( (O−E)<sup>2</sup>/E​ ) = (60 - 50)<sup>2</sup> / 50 + (40 - 50)<sup>2</sup> / 50 = 4
- Degrees of Freedom : k(Number of categories)−1=2−1=1
- For α = 0.05 and df = 1:
   - Critical value (χ<sup>2</sup><sub>0.05</sub>,1) ≈ 3.841

- Since χ² (4) > 3.841 → reject H<sub>0</sub> .

---
f) ANOVA (Analysis of Variance) / F- Statistics :

→ If we only had 2 groups, we’d just use a t-test. But for 3 or more, doing multiple t-tests increases the chance of error.

ANOVA solves this by comparing:

- Variation between groups (how far group means are from the overall mean).

- Variation within groups (how spread out the data is inside each group).

Formula:

 F = Variance between Groups / Variance within Group 
   = Mean squared between groups / Mean squared within groups 
   = ​MS<sub>between</sub> / MS<sub>within</sub>
   
 - MS<sub>between</sub> =  SS<sub>between</sub> / df<sub>between</sub>
   - SS<sub>between</sub> : Sum of squares between groups (differences of group means from overall mean)
      - SSB= Σ<sub>g=1</sub><sup>k</sup> n<sub>g</sub> (x̄<sub>g</sub> − x̄<sub>..</sub>)²
   - df<sub>between</sub> : k−1 (k = number of groups)
 - MS<sub>within</sub>=  SS<sub>within</sub> / df<sub>within</sub>
   - SS<sub>within</sub> : Sum of squares within groups (variation inside each group).
      - SSW = Σ<sub>g=1</sub><sup>k</sup> Σ<sub>i=1</sub><sup>n<sub>g</sub></sup> (x<sub>ig</sub> − x̄<sub>g</sub>)²
   - df<sub>within</sub> : N−k (N = total sample size)
	
	​​
<p align="center">
<img src="images/F-distribution.png" alt="F Distribution" height="350" width="45%"/>
 <img src="images/F-table.png" alt="F - Statistics Values" height="350" width="45%"/>
</p>

Example : 
Data (scores by teaching method)
- Group A: 85, 90, 88
- Group B: 75, 78, 94
- Group C: 92, 94, 96

Steps :

- Hypothesis :
  - H <sub>0</sub> : μ<sub>A</sub> ​= μ<sub>B</sub> ​= μ<sub>C</sub>
  - H <sub>1</sub> : At least one group mean is different
- Parameters
  - n<sub>A</sub> = 3 , n<sub>B</sub> = 3, n<sub>C</sub> = 3
  - Number of groups k=3.
  - Grouped means
    - x̄<sub>A</sub> = (85+90+88)/3 = 87.67
    - x̄<sub>B</sub> = 75.67
    - x̄<sub>C</sub> = 94
  - x̄ = 85.78 (overall mean)

 - SSB = n<sub>A</sub> × ((x̄<sub>A</sub> - x̄ )<sup>2</sup>) + n<sub>B</sub> × ((x̄<sub>B</sub> - x̄ )<sup>2</sup>) + n<sub>C</sub> × ((x̄<sub>C</sub> - x̄ )<sup>2</sup>) = 521.37
 - SSW
   - Group A = Σ<sub>i=1</sub><sup>n<sub>A</sub></sup> (x<sub>iA</sub> − x̄<sub>A</sub>)² = (85 - 87.6)<sup>2</sup> + (90 - 87.6)<sup>2</sup> + (88 - 87.6)<sup>2</sup> = 7.11
   - Group B = Σ<sub>i=1</sub><sup>n<sub>B</sub></sup> (x<sub>iB</sub> − x̄<sub>B</sub>)² = 10.66
   - Group C = Σ<sub>i=1</sub><sup>n<sub>C</sub></sup> (x<sub>iC</sub> − x̄<sub>C</sub>)² = 8
   - SSW = Σ Groups = 7.11 + 10.66 + 8 = 25.77
 - df<sub>between</sub> =  k−1 (k = number of groups) = 3 - 1 = 2 (df<sub>1</sub>)
 - df<sub>within</sub> : N−k (N = total sample size) = 9 - 3 = 6 (df<sub>2</sub>)
- MS<sub>between</sub> =  SS<sub>between</sub> / df<sub>between</sub> = 521.37 / 2 = 260.68
- MS<sub>within</sub>=  SS<sub>within</sub> / df<sub>within</sub> = 25.77 / 6 = 4.3
- F = ​MS<sub>between</sub> / MS<sub>within</sub> = 260.68 / 4.3 = 60.62
- From f-table df<sub>1</sub> = 2,df<sub>2</sub> = 2, α=0.05
  -  F - critical = 5.14
 
- F - statistic (60.62) > F - critical (5.14)  → reject H<sub>0</sub> 
  
 
      
	​

 ​​
