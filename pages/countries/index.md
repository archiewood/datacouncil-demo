```countries
SELECT
    country_name,
    country_code
FROM read_csv('sources/world.csv')
group by country_name, country_code
```


<DataTable data={countries} link=country_code rows=all showLinkCol/>