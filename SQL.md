# SQL

SQL Scripts and complex querying

## Complex Sub-Queries

Sub-queries can be used to gather information from a different source that can be attached within the SELECT part of the query, this can enhance the speed if request by combining queries into one query.

**Example**

```
	SELECT t.xxx, t.xxx, t.xxx, t.xxx, t.xxx, t.xxx, d.xxx AS xxx,
	###################### First sub query from table 
	(	SELECT 	JSON_ARRAYAGG(ts.jsonObjects)
		FROM 	(SELECT 	t1.trailerTimesheetID, JSON_OBJECT('tableIndexId', t1.tableIndexId) AS jsonObjects
			FROM 		tabelOneSubQuery AS t1						
			LEFT JOIN 	leftJoinTable AS ljt ON ljt.tableIndexId = t1.tableIndexId
			WHERE 		1=1
			AND 		((ljt.date >= DATE_FORMAT(CURDATE(), '%Y-%m-01') AND ljt.date <= LAST_DAY(CURDATE())) OR (ljt.date >= DATE_FORMAT(DATE_SUB(CURDATE(), INTERVAL 1 MONTH), '%Y-%m-01') AND ljt.date <= LAST_DAY(DATE_SUB(CURDATE(), INTERVAL 1 MONTH))) OR (ljt.date >= DATE_FORMAT(DATE_ADD(CURDATE(), INTERVAL 1 MONTH), '%Y-%m-01') AND ljt.date <= LAST_DAY(DATE_ADD(CURDATE(), INTERVAL 1 MONTH))) OR (WEEKDAY(CURDATE()) > 5 AND ljt.date BETWEEN DATE_SUB(CURDATE(), INTERVAL WEEKDAY(CURDATE()) + 12 DAY) AND DATE_SUB(CURDATE(), INTERVAL WEEKDAY(CURDATE()) + 13 DAY)))
			AND 		t1.isDeleted = 0
			AND 		t1.id = mt.id
			GROUP BY 	t1.id) AS ts
	) AS 'jsonObjects',
	################################
	FROM 				    mianTable AS mt
	LEFT JOIN 			dev_tmshire.OtherLeftJoinTable AS ot ON ot.id = mt.id
	WHERE 1=1
	AND mt.isDeleted = 0
	AND mt.id IN (51,47,32,35)

```

In the example above, the first sub-query has been gathered by relating its data in the `WHERE` clause to the main query (e.g. `AND  t1.id = mt.id`), this gives us a connection between the subquery and the main query so we can condition out what we actually need in relations to the main query. The following `AND` statements are more conditions around what results we want from the sub-query.

Using the `GROUP BY` clause (e.g. `GROUP BY 	t1.id) AS ts`) allows us to keep related results from the sub-query together by grouping them by the main queries `id` so that all related information stays together.

The use of `JSON_OBJECT` function allows us to get our sub-query results within objects, this allows us to gather more than one result from the sub-query and allows us to keep together the related information within objects, scoping them makes the results easier to read and access when using the information within your operations.
