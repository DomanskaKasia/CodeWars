# SQL Bug Fixing: Fix the QUERY - Totaling

Oh no! Timmys been moved into the database divison of his software company but as we know Timmy loves making mistakes. Help Timmy keep his job by fixing his query...

Timmy works for a statistical analysis company and has been given a task of totaling the number of sales on a given day grouped by each department name and then each day.

Resultant table:

- day (type: date) {group by} [order by asc]
- department (type: text) {group by} [In a real world situation it is bad practice to name a column after a table]
- sale_count (type: int)

Tables and relationship below:

```sql
--PostgreSQL 9.6
select
	date(s.transaction_date) as "day"
	,d.name as "department"
	,count(*) as "sale_count"
from department d
	join sale s on d.id = s.department_id
group by day, department
order by day
```

Output

day	department	sale_count
2019-09-02	Clothing	45
2019-09-02	Home	52
2019-09-02	Jewelry	33
2019-09-02	Shoes	46
2019-09-02	Tools	39
2019-09-03	Clothing	38
2019-09-03	Home	65
2019-09-03	Jewelry	22
2019-09-03	Shoes	11
2019-09-03	Tools	51
2019-09-04	Clothing	40
2019-09-04	Home	21
2019-09-04	Jewelry	27
2019-09-04	Shoes	10
2019-09-04	Tools	33
2019-09-05	Clothing	40
2019-09-05	Home	11
2019-09-05	Jewelry	42
2019-09-05	Shoes	36
2019-09-05	Tools	70
2019-09-06	Clothing	16
2019-09-06	Home	38
2019-09-06	Jewelry	19
2019-09-06	Shoes	58
2019-09-06	Tools	19
2019-09-07	Clothing	33
2019-09-07	Home	48
2019-09-07	Jewelry	21
2019-09-07	Shoes	44
2019-09-07	Tools	44
2019-09-08	Clothing	33
2019-09-08	Home	45
2019-09-08	Jewelry	68
2019-09-08	Shoes	54
2019-09-08	Tools	24
2019-09-09	Clothing	31
2019-09-09	Home	37
2019-09-09	Jewelry	29
2019-09-09	Shoes	66
2019-09-09	Tools	71
2019-09-10	Clothing	40
2019-09-10	Home	36
2019-09-10	Jewelry	46
2019-09-10	Shoes	46
2019-09-10	Tools	21
2019-09-11	Clothing	52
2019-09-11	Home	44
2019-09-11	Jewelry	43
2019-09-11	Shoes	45
2019-09-11	Tools	47
2019-09-12	Clothing	38
2019-09-12	Home	27
2019-09-12	Jewelry	27
2019-09-12	Shoes	18
2019-09-12	Tools	14