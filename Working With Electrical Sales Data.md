```python
import project
project.init("car_sales_data.csv")
```

**Highest Number of Sales in an Given Year Function**


```python
def year_max(year):

    
    model_s_sales = project.get_sales(project.get_id('Tesla Model S'), year)
    volt_sales = project.get_sales(project.get_id('Chevy Volt'), year)
    leaf_sales = project.get_sales(project.get_id('Nissan Leaf'), year)
    prius_sales = project.get_sales(project.get_id('Toyota Prius PHEV'), year)
    fusion_sales = project.get_sales(project.get_id('Ford Fusion Energi'), year)
    model_x_sales = project.get_sales(project.get_id('Tesla Model X'), year)

    return max(model_s_sales, volt_sales, leaf_sales, prius_sales, fusion_sales, model_x_sales)
```

**Question 1**: What was the highest number of sales for any model in the year 2017?


```python
max_sales_2017 = year_max(2017)

max_sales_2017
```




    26500



**Lowest Sales in Given Year for Given Model Function**


```python
def sales_min(model):
    model_id = project.get_id(model)    
    sales_2017 = project.get_sales(model_id, 2017)
    sales_2018 = project.get_sales(model_id, 2018)
    # get the sales from other years
    sales_2019 = project.get_sales(model_id, 2019)
    sales_2020 = project.get_sales(model_id, 2020)
    sales_2021 = project.get_sales(model_id, 2021)
    min_sales_2017_to_2021 = min(sales_2017, sales_2018, sales_2019, sales_2020, sales_2021)
    return min_sales_2017_to_2021
```

**Question 2**: What was the lowest sales number in a single year between the Chevy Volt, Ford Fusion Energi, and the Nissan Leaf?


```python
min_sales_CV_FFE_NL = min(sales_min('Chevy Volt'), sales_min('Ford Fusion Energi'), sales_min('Nissan Leaf'))

min_sales_CV_FFE_NL
```




    16



**Average Yearly Sales for Given Model across five years (2017-2021)**


```python
def sales_avg(model):

    model_id = project.get_id(model)    
    sales_2017 = project.get_sales(model_id, 2017)
    sales_2018 = project.get_sales(model_id, 2018)
    sales_2019 = project.get_sales(model_id, 2019)
    sales_2020 = project.get_sales(model_id, 2020)
    sales_2021 = project.get_sales(model_id, 2021)
    
    avg_sales_2017_to_2021 = ((sales_2017 + sales_2018 + sales_2019 + sales_2020 + sales_2021)/5)
    return avg_sales_2017_to_2021
```

**Question 3**: What was the average number of Chevy Volt cars sold per year between 2017 and 2021?


```python
sales_avg_volt_2017_to_2021 = sales_avg('Chevy Volt')
sales_avg_volt_2017_to_2021
```




    8730.6



**Sales of All models for Given Year**


```python
def year_sum(year=2021): # DO NOT EDIT THIS LINE
    model_s_sales = project.get_sales(project.get_id('Tesla Model S'), year)
    volt_sales = project.get_sales(project.get_id('Chevy Volt'), year)
    leaf_sales = project.get_sales(project.get_id('Nissan Leaf'), year)
    prius_sales = project.get_sales(project.get_id('Toyota Prius PHEV'), year)
    fusion_sales = project.get_sales(project.get_id('Ford Fusion Energi'), year)
    model_x_sales = project.get_sales(project.get_id('Tesla Model X'), year)
    
    total_sales_2017_to_2021 = model_s_sales+ volt_sales + leaf_sales + prius_sales + fusion_sales+ model_x_sales
    return total_sales_2017_to_2021
```

**Question 4**: What was the total number of vehicles sold between 2019 and 2021?


```python
sales_sum_2019_to_2021 = year_sum(2019)+year_sum(2020)+year_sum()
sales_sum_2019_to_2021
```




    289765



**Average Increase/Decrease in Sales over Sepcified Period for Given Model**


```python
def change_per_year(model, start_year=2017, end_year=2021): # DO NOT EDIT THIS LINE
    model_id = project.get_id(model)    
    sales_2017 = project.get_sales(model_id, 2017)
    sales_2018 = project.get_sales(model_id, 2018)
    sales_2019 = project.get_sales(model_id, 2019)
    sales_2020 = project.get_sales(model_id, 2020)
    sales_2021 = project.get_sales(model_id, 2021)
    sales_start_year = project.get_sales(model_id, start_year) 
    sales_end_year = project.get_sales(model_id, end_year)
    sales_difference = sales_end_year - sales_start_year
    change_per_year = sales_difference/(end_year-start_year)
    return change_per_year
```

**Question 5**: How much have the sales of the Tesla Model X changed per year (on average) from 2017 to 2020?


```python
model_x_average_change = change_per_year('Tesla Model X', end_year= 2020)
model_x_average_change
```




    2389.0



**Estimate Target Sales in Specificed Year Function**

def estimate_sales(model, target_year, start_year=2017, end_year=2021):
    avg_sales = change_per_year(model, start_year, end_year)
    num_year = (target_year-start_year)
    model_id = project.get_id(model)
    sales_start_year = project.get_sales(model_id, start_year)
    estimate_sales= (avg_sales*num_year) + sales_start_year
    return estimate_sales

**Question 6:** What are the estimated sales for the Toyota Prius PHEV in 2026 based on the average change in sales per year for it between 2018 and 2020?


```python
prius_sales_in_2026 = estimate_sales('Toyota Prius PHEV', 2026, 2018,2020)
prius_sales_in_2026
```




    91315.0



**Question 7**: What is, for the Toyota Prius PHEV sales, the ratio of the change per year between 2019 and 2020 to the change per year between 2017 and 2021?


```python
prius_change_per_year_ratio = change_per_year('Toyota Prius PHEV', start_year=2019, end_year=2020)/change_per_year('Toyota Prius PHEV')
prius_change_per_year_ratio
```




    2.090140253191154


