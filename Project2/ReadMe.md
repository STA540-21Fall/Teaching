# Project 2

**You may want to delete this file at the end, and substitute it with your own `readme.rmd` file (see [below](#readme)).**

Prediction of Covid-19 cases are of great importance in many aspects. In this project, we focus on forecasting state-level Covid-19 case and fatality numbers in United States.

Each group should:
- build statistical models for forecasting
- collect additional data as needed
- fit the model and forecase the numbers for the coming seven days
- (Important) keep track of the whole process with reproducible documentation.

**For forecasting problems, please avoid utilizing any data that cannot be collected when you do forecasting. For example, it does not make sense to forecast death tolls from the number of cases on the same day.**

--------------
## Repository structure

Following [suggestions](https://nicercode.github.io/blog/2013-04-05-projects/) by RICH FITZJOHN, the repository is organized as follows.

```
proj/
├── lib/
├── data/
├── doc/
└── output/
```

- The `data` directory contains data used in the analysis. This is treated as read only; in paricular the R/python files are never allowed to write to the files in here. Depending on the project, these might be csv files, a database, and the directory itself may have subdirectories.

- The `doc` directory contains the report or presentation files. It can have subfolders.

- The `lib` directory contains files with function definitions. If you might need to write a helper function that is used through your analysis, this is a good place where the function should go. However, no functions should be called and executed here - they should only be defined here.

- The `output` directory contains analysis output, processed datasets, logs, or other processed things.

-------

## Evaluation Criterion:

- Root Mean Square of Log Error (RMSLE):
  $$\mathrm{RMSLE} = \sqrt{\frac{1}{N_f}\sum_f [\log (\hat{y}_i + 1) - \log(y_i + 1)]^2},$$
  where $y_i$ and $\hat{y}_i$ are the true and predicted number respectively. $N_f = 7 \times 51$ is the total number of predictions, _i.e._, predictions for 7 days of 51 states including D.C.
- Weighted Pinball Loss (WPL):
  $$\mathrm{WPL} = \frac{1}{N_f}\sum_f w_f \frac{1}{N_\tau}\sum_\tau L_\tau(y_i, \hat{y}_i),$$
  where 
  $$L_\tau (y, \hat{y}) = \left\{
    \begin{aligned}
    & (y - \hat{y})\tau, & & \text{if $y\geq \hat{y}$,}\\
    & (y - \hat{y})(1 - \tau), & & \text{if $y< \hat{y}$.}\\
  \end{aligned}
  \right.$$
  and $\tau\in \{0.05, 0.50, 0.95\}$  is the quantile to be predicted. $N_\tau = 3$ is the number of quantiles to be predicted. $w_f$ is a weighting factor, defined as 
  $$w = 10 / \log(1 + \text{population}).$$

-------

## Suggested Workflow & Timeline

- Week 1 & 2: Classic Regression Models
  - Freely choose any model (including non-classic models) to seek accurate prediction.
  - Only focus on RMSLE.
- Week 3 & 4: Exploration of Predictive Models
  - Build a vanilla model. Feel free to incorporate any other data such as temporal information.
  - Build a temporal or spatial or spatio-temporal model, e.g. a CAR model, a Bayesian state-space model, etc. The point is to implement some classical statistical model to incorporate spatial temporal information.
  - Your prediction should be leveraging both RMSLE and WPL.

------

## Deliverables

### Prediction

Each week, you should submit data which contain your prediction for the next 7 days. The format of submission files are as follows.

- Mean Prediction: Files named `case_m.csv` and `death_m.csv`, including the predicted mean value of number of cases and deaths of each day in a given seven-day period.

```
State,  Y1,   Y2,   Y3,   Y4,   Y5,   Y6,   Y7
   AL,   x,    x,    x,    x,    x,    x,    x
   AK,   x,    x,    x,    x,    x,    x,    x
...
```

- Quantile Prediction: Files named `case_q.csv` and `death_q.csv`, including the predicted quantiles of number of cases and deaths of each day in a given seven-day period.

```
State, Quantile,  Y1,   Y2,   Y3,   Y4,   Y5,   Y6,   Y7
   AL,     0.05,   x,    x,    x,    x,    x,    x,    x
   AL,     0.50,   x,    x,    x,    x,    x,    x,    x
   AL,     0.95,   x,    x,    x,    x,    x,    x,    x
   AK,     0.05,   x,    x,    x,    x,    x,    x,    x
   AK,     0.50,   x,    x,    x,    x,    x,    x,    x
   AK,     0.95,   x,    x,    x,    x,    x,    x,    x
...
```

For the first two weeks, you are only required to submit files for mean prediction. For the next two weeks, you should submit files for both mean and quantile prediction.

| Due Date 	| Prediction Start 	| Prediction End 	| Mean Prediction 	| Quantile Prediction 	|
|----------	|------------------	|----------------	|-----------------	|---------------------	|
| 09/23    	| 09/23           	| 09/29          	| Yes             	| No                  	|
| 09/30    	| 09/30            	| 10/06          	| Yes             	| No                  	|
| 10/12    	| 10/12            	| 10/18          	| Yes             	| Yes                 	|
| 10/19    	| 10/19            	| 10/25          	| Yes             	| Yes                 	|

  
### Reports

- Interim report (Due 09/30): prepare a report, not to exceed 7 pages. It describes your development of the “classic” statistical model, including data cleaning, feature engineering, model comparisons. Pay special emphasis on the process of improving your model, e.g. what features help the most or the least. Be critical, e.g. ask if the classical models are really as good as advised. All results should be fully reproducible.

- Final report (Due 10/17): prepare a report, not to exceed 10 pages and accompanied by useful visualizations, describing your data cleaning, feature engineering, model/algorithm development and comparisons. All results should be fully reproducible.



------

## ReadMe

You are required to post a `readme.md` file at the root of your repository, including your title, team members, project abstract and a contribution statement. (Feel free to delete this markdown file then.)

Below are two samples of contribution statements.

> All team members contributed equally in all stages of this project. All team members approve our work presented in this GitHub repository including this contributions statement.

> AB, CD, EF and GH designed the study. AB and CD developed baseline classification model for evaluation. EF and GH explored feature engineering for improving the baseline model. AB, EF and GH discussed and designed the model evaluation protocol. CD carried out the computation for model evaluation. All team members contributed to the GitHub repository and prepared the presentation. All team members approve our work presented in our GitHub repository including this contribution statement.
