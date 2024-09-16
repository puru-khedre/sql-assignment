**Query:** How many orders with a single return were recorded in the last month?

**Query cost:** 511

**Solution:**
```sql
select
	count(*)
from (
	select
		ri.ORDER_ID
	from
		return_header rh
	join return_item ri 
	on
		ri.RETURN_ID = rh.RETURN_ID
		and datediff(curdate(), rh.ENTRY_DATE)<= 30
	group by
		ri.ORDER_ID,
		ri.RETURN_ID
	having
		count(*)= 1
) ORDERS;
```
