<script>
    import Name from '$lib/Name.svelte';
    let country_gdp_data=gdp.filter(d => d.country_code === $page.params.country.toLowerCase())
    let country = countries.filter(d => d.country_code === $page.params.country.toLowerCase())
</script>


# Hey there <Name/> 👋🏼

Hope you're enjoying Data Council!

## You've come in from <Value data={country} />




```countries
SELECT
    country_name,
    lower(country_code)
FROM 'sources/world.csv'
group by country_name, country_code
```

```gdp
SELECT
    year,
    (year || '-01-01')::timestamp as date,
    country_name,
    country_code,
    gdp_per_person_employed as gdp_per_person_employed_usd,
    gdp_per_capita_ppp as gdp_per_capita_ppp_usd,
    gdp_ppp_2017 as gdp_ppp_2017_usd,
    gdp_ppp_current::float as gdp_ppp_current_usd0b,
    -- abs change since previous year
    gdp_ppp_current::float - lag(gdp_ppp_current::float) over (partition by country_code order by year) as gdp_ppp_current_change_usd0b,
    -- abs change since 5 years ago
    gdp_ppp_current::float - lag(gdp_ppp_current::float, 5) over (partition by country_code order by year) as gdp_ppp_current_change_5y_usd0b
FROM 'sources/world.csv'
where year > 2001
and gdp_ppp_2017 is not null
order by year desc
```

```latest_year_gdp_rank
SELECT
    country_name,
    country_code,
    year,
    gdp_ppp_current::float as gdp_ppp_current_usd0b,
    rank() over (order by gdp_ppp_current::float desc) as gdp_ppp_current_rank

FROM 'sources/world.csv'
WHERE year = (SELECT max(year) FROM 'sources/world.csv')
AND gdp_ppp_current is not null
ORDER BY gdp_ppp_current_usd0b desc
```

{#if country_gdp_data.length > 0}

A couple of facts about <Value data={country} />

<BigValue data={country_gdp_data} value=gdp_per_capita_ppp_usd title="GDP per Capita, PPP ($)"/>

<BigValue data={country_gdp_data} value=gdp_per_person_employed_usd title="GDP per person Employed, PPP ($)"/>


## Economic Snapshot

<Value data={country} />'s economy was worth <Value data={country_gdp_data} column=gdp_ppp_current_usd0b row=0/> in <Value data={country_gdp_data} column=year row=0/> at PPP, which was 

- {#if country_gdp_data[0].gdp_ppp_current_change_usd0b > 0}an increase of <Value data={country_gdp_data} column=gdp_ppp_current_change_usd0b/> from {country_gdp_data[1].year}{:else}a decrease of <Value data={country_gdp_data} column=gdp_ppp_current_change_usd0b/> from {country_gdp_data[1].year}{/if}
- {#if country_gdp_data[0].gdp_ppp_current_change_5y_usd0b > 0}an increase of <Value data={country_gdp_data} column=gdp_ppp_current_change_5y_usd0b/> from {country_gdp_data[5].year}{:else}a decrease of <Value data={country_gdp_data} column=gdp_ppp_current_change_5y_usd0b/> from {country_gdp_data[5].year}{/if}


This puts it at <Value data={latest_year_gdp_rank.filter(d=>d.country_code===$page.params.country)} column=gdp_ppp_current_rank/>/{latest_year_gdp_rank.length} in the world for GDP per capita, PPP (for.toLowerCase() countries with data).

<BarChart
  data={country_gdp_data}
  x=date
  y=gdp_ppp_current_usd0b
  title="GDP for {country_gdp_data[0].country_name}"
  subtitle= "(PPP, Current USD)"
/>

Look at [another country?](../)


<!-- <DataTable data={country_gdp_data} rows=all/> -->

{:else}

Unfortunately the world bank does not publish data for <Value data={country} />.

Why not try [another country?](../)

{/if}


## What is Evidence?

Evidence is a web framework for data analysts. It’s an open source, code-based alternative to drag-and-drop business intelligence tools.

## Like what you see?

- Sign up for our [Cloud Waitlist](https://du3tapwtcbi.typeform.com/to/kwp7ZD3q)
- [Book a demo](https://calendly.com/d/dxf-2t4-fq8/chat-with-adam-archie?month=2023-03) to find out more
- Check out the [source code](https://github.com/archiewood/datacouncil-demo) for this app.

