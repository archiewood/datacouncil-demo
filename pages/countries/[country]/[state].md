<script>
    import Name from '$lib/Name.svelte';
    import Outro from '$lib/Outro.svelte';
    let state = states.filter(d => d.state_code === $page.params.state)
    let state_gdp=bea_gdp.filter(d => d.state_code === $page.params.state)
    let state_income_per_capita= bea_income_per_capita.filter(d => d.state_code === $page.params.state)
    let state_employment=bea_total_employment.filter(d => d.state_code === $page.params.state)
    
</script>

# Hey there <Name/> 👋🏼

Hope you're enjoying Data Council!

## You've come in from <Value data={state} column=state_name/>

```states
select 
state_name,
lower(state_code) as state_code,
sum(value) as gdp_usd,
rank() over (order by sum(value) desc) as gdp_rank
from 'sources/states.csv'
where measure = 'Gross domestic product (GDP)'

group by state_name, state_code
order by state_name
```

```bea_gdp
select 
state_name,
lower(state_code) as state_code,
year,
(year || '-01-01')::timestamp as date_yyyy,
sum(value)* 1000000 as gdp_usd0b,
-- abs change since previous year
sum(value*1000000) - lag(sum(value*1000000)) over (partition by state_code order by year) as gdp_change_usd0b,
-- abs change since 5 years ago
sum(value*1000000) - lag(sum(value*1000000), 5) over (partition by state_code order by year) as gdp_change_5y_usd0b

from 'sources/states.csv'
where measure = 'Gross domestic product (GDP)'
group by state_name, state_code, year
order by state_name, year desc
```

```bea_income_per_capita
select
state_name,
lower(state_code) as state_code,
year,
sum(value) as income_per_capita_usd
from 'sources/states.csv'
where measure = 'Per capita personal income'
group by state_name, state_code, year
order by state_name, year desc
```

```bea_total_employment
select
state_name,
lower(state_code) as state_code,
year,
sum(value) as total_employment_num0
from 'sources/states.csv'
where measure = 'Total employment'
group by state_name, state_code, year
order by state_name, year desc
```




Here are some facts about <Value data={state} value=state_name/>:

<BigValue data={state_gdp} value=gdp_usd0b title="GDP"/>

<BigValue data={state_income_per_capita} value=income_per_capita_usd title="Income per capita"/>

<BigValue data={state_employment} value=total_employment_num0 title="Total employment"/>

## Economic Snapshot


<Value data={state} />'s economy was worth <Value data={state_gdp} column=gdp_usd0b/> in 2021, which was:

- {#if state_gdp[0].gdp_change_usd0b > 0}an increase of <Value data={state_gdp} column=gdp_change_usd0b/> from {state_gdp[1].year}{:else}a decrease of <Value data={state_gdp} column=gdp_change_usd0b/> from {state_gdp[1].year}{/if}
- {#if state_gdp[0].gdp_change_5y_usd0b > 0}an increase of <Value data={state_gdp} column=gdp_change_5y_usd0b/> from 2016{:else}a decrease of <Value data={state_gdp} column=gdp_change_5y_usd0b/> from 2016{/if}

That puts it at <Value data={state} column=gdp_rank/>/{states.length} among US states.

<BarChart 
    data={state_gdp} 
    x=date_yyyy 
    y=gdp_usd0b
    title="GDP for {state[0].state_name}"
/>




See [data on more states](/countries/usa)

<Outro/>