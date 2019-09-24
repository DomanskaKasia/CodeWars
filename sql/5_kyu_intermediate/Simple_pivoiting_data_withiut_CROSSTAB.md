# Using LATERAL JOIN To Get Top N per Group

Description

Given the schema presented below write a query, which uses a LATERAL join, that returns two most viewed posts for every category.

Order the result set by:

1. category name alphabetically
2. number of post views largest to lowest
3. post id lowest to largest

Note:

- Some categories may have less than two or no posts at all.
- Two or more posts within the category can be tied by (have the same) the number of views. Use post id as a tie breaker - a post with a lower id gets a higher rank.

Schema

categories

|Column|Type|Modifiers|
|------------|-----------------------------|----------|
|id |integer |not null|
|category |character varying(255)|not null|

posts

|Column|Type|Modifiers|
|------------|-----------------------------|----------|
|id |integer |not null|
|category_id |integer |not null|
|title |character varying(255) |not null|
|views |integer |not null|

Desired Output

The desired output should look like this:

|category_id|category|title|views|post_id|
|------------|----------|-----------------------------------|-------|--------|
|5 |art |Most viewed post about Art |9234 |234|
|5 |art |Second most viewed post about Art |9234 |712|
|2 |business |NULL |NULL |NULL|
|7 |sport |Most viewed post about Sport |10 |126|
...

- category_id - category id
- category - category name
- title - post title
- views - the number of post views
- post_id - post id

```sql
--PostgreSQL 9.6
select c.id as "category_id"
	,c.category
	,p.title
	,p.views
	,p.id as "post_id"
from categories c
	left join lateral
	(
		select title
			,category_id
			,views
			,id
		from posts
		where category_id = c.id
		order by views desc
		limit 2
	) p on c.id = p.category_id
order by c.category, p.views desc, p.id
```