# US State Economic Data

Select a state to find out more.    

```states
select 
state_name,
sum(value)*1000000 as GDP_usd,
lower(state_code) as state_code
from 'sources/states.csv'
where measure = 'Gross domestic product (GDP)'
and year=2021

group by state_name, state_code
order by state_name
```


<DataTable 
    data={states} 
    link=state_code 
    rows=all
>
<Column id=state_name/>
<Column id=GDP_usd title="GDP"/>
</DataTable>