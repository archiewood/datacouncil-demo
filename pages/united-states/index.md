```states
select 'CA' as state, 'united-states/CA' as link, 'California' as name, 39.5 as population, 163694 as area, 2.4 as density union all
select 'TX' as state, 'united-states/TX' as link, 'Texas' as name, 28.7 as population, 268596 as area, 1.1 as density union all
select 'FL' as state, 'united-states/FL' as link, 'Florida' as name, 21.3 as population, 65758 as area, 3.2 as density union all
select 'NY' as state, 'united-states/NY' as link, 'New York' as name, 19.5 as population, 54555 as area, 3.6 as density union all
select 'PA' as state, 'united-states/PA' as link, 'Pennsylvania' as name, 12.8 as population, 46054 as area, 2.8 as density
```

<DataTable data={states} link=link rows=all/>