# Project 3

**You may want to delete this file at the end, and substitute it with your own `readme.rmd` file (see [below](#readme)).**

Tree growth provides essential information about forest ecology. One common method to estimate tree growth is based on repeated tape measurements of the diameter of the same tree, and the diameter increment is the difference between the current and previous measurement.

Each group is expected to gain experience on
- data wrangling
- developing, validating, and interpreting hierarchical model based on real world data
- dealing with spatio temporal data and models

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

## Description

- Explore and analyze the above data to infer about the pattern of tree growth. In this regard, we may be interested in learning about both stand (population) level growth and individual level growth.

- Spatial information is provided and is encouraged (not required) to be used in the analysis. If you can’t run a model with spatial information, at least explain how (e.g. models) one would potential incorporate that information into the analysis.

--------

## Tips on data wrangling and modeling

- Many of the NA’s in the data are not real NA’s; they are created due to the format of data input, which uses a regular grid of time but the actual observations are made on irregular grids. Consider transforming the data to the so-called long format, where observation of each subject at each time point makes up a row.

- Tree diameters are measured with errors. When building a model, consider whether to directly model the raw observations or the underlying “true” value. For example, we can assume Y_{i,t} = μ_{i,t} + ϵ_{i,t}, where Y_{i,t} and μ_{i,t} are the observed and true value of the tree diameter, respectively, and ϵ_{i,t} is a random error. Shall we build growth models on Y_{i,t} or μ_{i,t}?

- How to scale? Different species of trees can significantly differ in their size. Consider if we should directly model the increment or rate of increment? Should the scale be linear or exponential?

- The spatial information here is encoded in coordinates. Can we still think of “neighboring” information? Is there alternative way of measuring the spatial information?

-------

## Deliverables

### Project

Prepare a report, not to exceed 5 pages and accompanied by useful visualizations, regarding tree growth based on your analysis that is understandable and useful to ecologists. Details of key statistical methods or models and validation should be given. All results should be fully reproducible. Due on October 10 (Sunday) 11pm.



------

## ReadMe

You are required to post a `readme.md` file at the root of your repository, including your title, team members, project abstract and a contribution statement. (Feel free to delete this markdown file then.)

Below are two samples of contribution statements.

> All team members contributed equally in all stages of this project. All team members approve our work presented in this GitHub repository including this contributions statement.

> AB, CD, EF and GH designed the study. AB and CD developed baseline classification model for evaluation. EF and GH explored feature engineering for improving the baseline model. AB, EF and GH discussed and designed the model evaluation protocol. CD carried out the computation for model evaluation. All team members contributed to the GitHub repository and prepared the presentation. All team members approve our work presented in our GitHub repository including this contribution statement.
