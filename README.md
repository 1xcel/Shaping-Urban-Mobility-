# Shaping-Urban-Mobility
Slide Deck : [MOD 4 - Stakeholder Deck ](https://docs.google.com/presentation/d/1fbciP_dsYTke7rEbwejWjaPBts6c21NEGuzIeJIIJkM/edit?usp=sharing)

## **Business Framing and Stakeholders**

There are currently over 500 bike-sharing programs worldwide. These systems allow users to rent bikes at one station and return them to another. \
My analysis focuses on the daily rental counts from 2011–2012 in the Capital Bikeshare system. The goal is to understand patterns of demand based on user behavior and provide insights for:



* **Inventory rebalancing windows** – scheduling bike redistribution and maintenance during low-impact hours. \

* **Promotional timing** – identifying the best times (season, month, day) for marketing campaigns. \

* **User segmentation** – maintaining transparency regarding which groups are targeted across different time intervals in the dataset. \



---


## **Methods Summary (EDA, Hypothesis Tests, A/B Design)**

**Exploratory Data Analysis (EDA) & Cleaning**

<img width="887" height="641" alt="EDA" src="https://github.com/user-attachments/assets/ce9415c5-3705-402c-b7e6-c6cb709fb676" />

* Renamed and dropped columns for easier readability. \

* Added derived columns to improve interpretability 
    * Categorizing hourly rentals 
    * Changing dteday into pd.to_datetime for easier aggregating 
    * Making dataset easier to readability 


---


## **Top 3 Trends/Insights and Business Impact**



1. **Low-Impact Maintenance Windows**

<img width="537" height="318" alt="Screenshot 2025-09-29 at 5 24 54 PM" src="https://github.com/user-attachments/assets/14704c56-b1e3-4948-ba38-354bf1150dea" />


    * Bike rentals are lowest between **2–4 AM**, making this the optimal time for maintenance and redistribution. \

    * Minimizes disruption to riders while keeping fleet availability high. \

2. **Seasonal Promotional Opportunities**

<img width="669" height="194" alt="Screenshot 2025-09-29 at 1 19 30 PM" src="https://github.com/user-attachments/assets/b00384c1-e516-4a0d-9f12-97287856daed" />


    * Rentals increase significantly in spring and summer (May–August), with a slight plateau in June–July. \

    * Marketing campaigns during these months could maximize ridership growth. \

4. **Demand Variability by Day Type**

<img width="634" height="301" alt="Screenshot 2025-09-29 at 2 45 23 PM" src="https://github.com/user-attachments/assets/cc482424-bd58-459e-8180-ac6a2dab218a" />


    * This insight helps stakeholders view the differences in registered and casual riderships throughout the years of 2011-2012 
     
    * Can provide insight on maintenance windows for bike rental spots inventory 


---

**Statistical Testing (Hypothesis questions) :**

**Commuter pattern**


* Do average hourly rides (remember each row in the data is a ride) differ

between working days and non-working days?

**Multi-group comparison**


* Do mean hourly rides differ across categories of multi-level categorical variables such

as season or weather condition (choose one)?


## **Hypothesis Testing Results**



1. **Working Days vs. Non-Working Days**

    <img width="946" height="749" alt="Screenshot 2025-09-29 at 2 55 02 AM" src="https://github.com/user-attachments/assets/294c6fc1-c770-476a-b002-95ebc5923487" />


I Filtered the dataset into working days (weekdays excluding holidays) and non-working days (weekends + holidays). Then a Welch’s two-sample t-test is used since we are comparing the means of two independent groups with unequal variances. Lastly we calculated the 95% confidence interval (CI) for the difference in means.

Results: 


    * **Null Hypothesis (H₀):** No difference in average hourly rides.
    * **Alternative Hypothesis (H₁):** A difference exists in average hourly rides.
    * **Test Result:** Welch’s two-sample t-test → *t* = 4.095, *p* &lt; 0.001.
    * **Decision:** Reject H₀ at α = 0.05.
    * **Practical Significance:** Working days see ~12 more rides per hour on average, showing a meaningful commuter effect. \

2. **Seasonal Differences **

We first grouped data by season using the dataset’s seasonal column to categorize rides into descriptive statistics, finding the mean hourly rides per season to observe overall patterns.** \
**

<img width="944" height="383" alt="Screenshot 2025-09-29 at 2 32 29 AM" src="https://github.com/user-attachments/assets/0a1199cf-dc8c-405a-b00e-041172fca00e" />


* **Null Hypothesis **= All seasonal average hourly rides are equal
* **Alternative Hypothesis** = One seasonal mean has a difference.
* **Test results** = F = 409.181 → Very high test statistic, p = 0.0000 → Well below α = 0.05.
* **Result:** Reject H₀, meaning average rentals are significantly different across at least one pair of seasons

**A/B Testing**

PM’s objective: Does ridership increase on working days during the early evening after launching a small app feature change

<img width="623" height="435" alt="Screenshot 2025-09-29 at 2 32 16 PM" src="https://github.com/user-attachments/assets/25cc6a68-c64b-4c3e-8749-afb5f8f9a6fe" />


Simulated A/B testing framework: Conducted a one-sample t-test on group means.



* **Group A (control)**: pre_stats
* **Group B (treatment)**: post_stats(subset of riders/time periods).
* **Null Hypothesis **: (no increase after launch)
* **Alternative Hypothesis **: ( Increase after launch ) 
* The effect is both statistically and practically meaningful, especially during high-demand months.
* Guardrails ensured no major biases, but the results are observationally simulated.


---


## **Ethics & Limitations**

* **Bias Risks:** Weather, local events, and infrastructure changes may affect these results. 
* **Equity Concerns:** Promotions or rebalancing strategies should ensure equitable access across neighborhoods, avoiding bias toward only high-demand areas. Also ,due to registered having more rentals, this could cause a disproportionate advantage to casual riders having bikes accessible for them to use, so we should focus on where we should increase the amount of bikes available.
* **Observational Data:** Not randomized — causation cannot be claimed.


---


## **Repository Structure**


```
.
├── data/  
│   ├── days.csv  
│   ├── hours.csv  
│   └── modified_hours_dataset.csv  
├── insights/  
│   ├── EDA_Notebook.ipynb  
│   ├── Hypothesis_testing.ipynb  
│   └── Simulated_A/B_Testing.ipynb  
├── visuals/  
│   ├── Stakeholder_Dashboard.xlsx  
│   └── README.md  
└── slides/  
    └── final_presentation 
