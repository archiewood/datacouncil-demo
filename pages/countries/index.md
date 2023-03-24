# World Economic Data

```countries
SELECT
    country_name,
    lower(country_code) as country_code
FROM 'sources/world.csv'
group by country_name, country_code
```

Select a country to find out more.

<DataTable data={countries} link=country_code rows=all/>