```countries
SELECT
    country_name,
    country_code,
    '/countries/' || country_code  as link
FROM 'sources/world.csv'
group by country_name, country_code
```

<DataTable data={countries} link=link rows=all/>