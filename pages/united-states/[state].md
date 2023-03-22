

# Hey there 👋🏼

Hope you are enjoying Data Council!

This report was generated just for you at {new Date().toLocaleString()}

## You live in <Value data={states.filter(d=>d.state===$page.params.state)} column=name/>

```states
select 'CA' as state, 'united-states/CA' as link, 'California' as name, 39.5 as population, 163694 as area, 2.4 as density union all
select 'TX' as state, 'united-states/TX' as link, 'Texas' as name, 28.7 as population, 268596 as area, 1.1 as density union all
select 'FL' as state, 'united-states/FL' as link, 'Florida' as name, 21.3 as population, 65758 as area, 3.2 as density union all
select 'NY' as state, 'united-states/NY' as link, 'New York' as name, 19.5 as population, 54555 as area, 3.6 as density union all
select 'PA' as state, 'united-states/PA' as link, 'Pennsylvania' as name, 12.8 as population, 46054 as area, 2.8 as density
```

Here are some facts about <Value data={states.filter(d=>d.state===$page.params.state)} column=name/>:

- The population is <Value data={states.filter(d=>d.state===$page.params.state)} column=population/>m

See [data on more states](../united-states) or [other countries](../countries).

## Evidence

Evidence is a web framework for data analysts. It’s an open source, code-based alternative to drag-and-drop business intelligence tools.

## Like what you see?

- Sign up for our [Cloud Waitlist](https://du3tapwtcbi.typeform.com/to/kwp7ZD3q)
- [Book a demo](https://calendly.com/d/dxf-2t4-fq8/chat-with-adam-archie?month=2023-03) to find out more
- We made this app in an hour. Check out the [source code](https://github.com/archiewood/datacouncil-demo)

