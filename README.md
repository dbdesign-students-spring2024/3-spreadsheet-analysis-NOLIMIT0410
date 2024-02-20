# Analysis on citywide payroll in NewYork

## Data set details:

- As a Junior student, I'm interested in how the City’s budget is being spent on salary and overtime pay for all municipal employees. This is the primary reason why I pick this dataset:**Citywide Payroll Data (Fiscal Year)**,from NYC OpenData [link to dataset](https://data.cityofnewyork.us/resource/k397-673e.json?). Due to my own capacity, I only chose the first 5000 rows as a sample.
- To make it clear , the original data was in Json file, and later turned into a csv file. The website only provides me API of the dataset, so I have to do a few steps to turn it into a Json file, using code below:
>- url = "https://data.cityofnewyork.us/resource/k397-673e.json?$limit=5000"
>- response = requests.get(url)
>- data = json.loads(response.content)

## Some examplary rows are displayed below:
**only a few part of the date are displayed here because the dataset is a little too complicated**
| fiscal_year | payroll_number | agency_name | last_name | first_name | mid_init | agency_start_date | work_location_borough | title_description | leave_status_as_of_june_30 | base_salary | pay_basis | regular_hours | regular_gross_paid | ot_hours | total_ot_paid | total_other_pay | 
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS | GARY  | TAWANA | N | 1996-06-23T00:00:00.000 | QUEENS | CHILD PROTECTIVE SPECIALIST SUPERVISOR | ACTIVE | 103483 | per Annum | 1820 | 98392.13 | 0 | 0 | 11314.99 |
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS | MANNO | SAMANTHA | J | 2018-06-25T00:00:00.000 | BROOKLYN | AGENCY ATTORNEY | Active | 109977 | per Annum | 1330 | 79025.39 | 0 | 0.5 | 3908.69 |  
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS |CURRIE | YASCHEN | T | 2022-05-23T00:00:00.000 | RICHMOND | CHILD PROTECTIVE SPECIALIST | CEASED | 53848 | per Annum | 210 | 6416.15 | 0 | 0 | 152.79 |   
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS | GARY | CASSAND | P | 2009-06-15T00:00:00.000 | MANHATTAN | CHILD PROTECTIVE SPECIALIST | CEASED | 62161 | per Annum | 0 | 291.28 | 0 | 0 | 14165.51 |    
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS | JACKSON | SABRA | E | 2019-04-29T00:00:00.000 | MANHATTAN | COMMUNITY COORDINATOR | ACTIVE | 74781 | per Annum | 1820 | 72443.96 | 16.5 | 714.43 | 3048/15 |   
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS | MANNING | TRILANE | N | 2007-06-04T00:00:00.000 | QUEENS | CHILD PROTECTIVE SPECIALIST | ACTIVE | 65921 | per ANNUM | 1820 | 65998.3 | 21.75 | 896.05 | 8149.47 |    
| 2023 | 67 | ADMIN FOR CHILDREN'S SVCS | BREWER | HENRY |  | 1996-06-23T00:00:00.000 | MANHATTAN | CHILD WELFARE SPECIALIST SUPERVISOR | ACTIVE | 92926 | per Annum | 1820 | 93037.26 | 0 | 0 | 8053.83 | 

As you can from the table, there are few columns that do absolutely no help to our data analysis, such as last name, first name, midinit. Because it is very unlikely that a person's name has an influence on his or her wage. Beisdes, for this data I would focus more on working location instead of specific position, so I delete columns related to that as well. Codes are listed below:

>- column_to_delete = ['payroll_number','last_name','first_name','mid_init','agency_start_date','agency_name','leave_status_as_of_june_30','title_description']
>- df2.drop(column_to_delete, axis=1, inplace=True)

Another thing I notice, is that some of the workers are paid annualy, while some others are paid hourly. If that happens there is no point compare two workers as they are paid in different ways. So I choose to delete those that are paid hourly. Code is listed below:
>- df2.drop(df2[df2['pay_basis'] != 'per Annum'].index, axis=0, inplace=True)

Links to each file are listed below:
- [original_data_file]()
- [clean_data]()
- [Modified_data]()




