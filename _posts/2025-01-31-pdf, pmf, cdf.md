---
title: "pdf, pmf, cdf <-> derivative and integral"
date: 2025-01-31 21:14:00 +0800
categories: [Data Science]
tags: [Math]
mathjax: true
---

The relationship between the **probability density function (PDF)**, **probability mass function (PMF)**, and **cumulative distribution function (CDF)** can indeed be understood in terms of **derivatives** and **integrals**, similar to the relationship between these mathematical operations. Here's a breakdown:

---

### **1. Concepts:**

#### **PDF (Probability Density Function)**:
- Used for continuous random variables.
- Represents the likelihood of a random variable taking on a specific value.
- The area under the PDF curve over an interval gives the probability that the random variable falls within that interval.

#### **PMF (Probability Mass Function)**:
- Used for discrete random variables.
- Represents the probability of a random variable taking on a specific value directly.

#### **CDF (Cumulative Distribution Function)**:
- Used for both discrete and continuous random variables.
- Represents the probability that a random variable is less than or equal to a certain value.

---

### **2. Relationships:**

#### For Continuous Random Variables:
- The **PDF** is the derivative of the **CDF**:  
  \begin{equation}f_X(x) = \frac{d}{dx} F_X(x),\end{equation}
  where $$F_X(x)$$ is the CDF, and $$f_X(x)$$ is the PDF.  

- The **CDF** is the integral of the **PDF**:
  \begin{equation}F_X(x) = \int_{-\infty}^x f_X(t) \, dt\end{equation}

---

#### For Discrete Random Variables:
- The **PMF** is analogous to the derivative (in a discrete sense):
  \begin{equation}P(X = x_i) = F_X(x_i) - F_X(x_{i-1}),\end{equation}
  where $$x_i$$ is a discrete value of the random variable, and $$F_X(x_i)$$ is the CDF.

- The **CDF** is the summation (analogous to an integral) of the **PMF**:
  \begin{equation}F_X(x_k) = \sum_{x_i \leq x_k} P(X = x_i)\end{equation}

---

### **3. Comparison with Derivatives and Integrals:**

| Concept                | Derivative/Integral Analogy         | Explanation                                              |
|------------------------|--------------------------------------|----------------------------------------------------------|
| **PDF or PMF**         | Derivative                         | Represents the rate of change (density or mass at a point). |
| **CDF**                | Integral (or summation for PMF)     | Accumulates probability up to a certain point.           |
| **PMF to CDF (Discrete)** | Summation                         | Like the integral for continuous, sums probabilities.    |
| **PDF to CDF (Continuous)** | Integral                        | Integrates density over a range to get probability.       |

### **4. Practical Insight:**
- The **PDF/PMF** is more detailed, focusing on specific points or small intervals of the random variable.
- The **CDF** gives a broader cumulative view, showing probabilities up to a certain threshold.
- differentiation (continuous case) or differences (discrete case) and integration (continuous case) or summation (discrete case).