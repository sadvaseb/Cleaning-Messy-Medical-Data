# Cleaning-Messy-Medical-Data

The dataset is a messy medical data with all types of dates and time formats. The goal is to find dates in each row of data and sort them ascendingly. There are multiple numbers and date-like elements in each row, but there is only one date in each row (i.e., avoid extracting all numbers or date-like elements). 

The dates are in different formats and shapes. Some of these formats are as below. The dataset also contains misspellings that should be identified and cleaned. 


04/10/2001; 04/10/19; 4/10/08; 4/30/10; 04-10-2001;
Mar-10-2019; Mar 22, 2019; May 22, 2002; Mar. 29, 2004; Jun 23 2018;
20 Jun 2011; 20 Jun 2011; 20 Jun. 2011; 20 Mar, 2011
Jun 17th, 2009; Jun 11st, 2009; Jun 12nd, 2009
Jun 2019; Sep 2009; Dec 2015
6/2017; 11/2018; 10-1967
2018; 1910



```python
def date_sorter():

	t2 = df.str.extract(r'(\\d{1,2} ?(?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)[a-z,.]* \\d{2,4})')   # handles 20 Mar 2009; 20 March 2009; 20 Mar. 2009; 20 March, 2009
	t3 = df.str.extract(r'((?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)[a-z.,]* \\d{2,4})')   # handles Feb 2009; Sep 2009; Oct 2010
	t4 = df.str.extract(r'((?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)[a-z\\.,-]*(?:\\s|-|\\.|,)\\d{1,2}[a-z,-.]*(?:\\s|-|\\.|,)\\d{2,4})')   # handles Mar 20th, 2009; Mar 21st, 2009; Mar 22nd, 2009; Mar-20-2009
	t1 = df.str.extract(r'((?:\\d{1,2}[/-])(?:\\d{1,2}[/-])\\d{2,4})') # handles 04/20/2009; 04-20-2009
	t5 = df.str.extract(r'((?:\\d{1,2}[/-]*)\\d{4})') # handles 12/2009; 12-2009
	t6 = df.str.extract(r'(\\d{4})') # handles 2008
	output = t4.fillna(t2).fillna(t3).fillna(t1).fillna(t5).fillna(t6)
	dates = pd.to_datetime(output.replace('Decemeber','December',regex=True).replace('Janaury','January',regex=True).replace('2June','June',regex=True))
	return pd.Series(data =(dates.sort_values()).index)

date_sorter()

```

 
This is a mini data cleaning project which is posted at Applied Data Science with Python Specialization program at the University of Michigan. The program available from [here](https://www.coursera.org/learn/python-text-mining) .


This project is only for education purpose and it should not be used for submitting for the course. 