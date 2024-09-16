**Query:** In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?

**Query cost:** 9,562.56

**Solution:**
```sql
select
	count(distinct os.ORDER_ID)
from
	order_status os
where
	os.ORDER_ID in (
	select
		distinct oisg.ORDER_ID
	from
		order_item_ship_group oisg
	join facility f
		on
		oisg.FACILITY_ID = f.FACILITY_ID
		and f.FACILITY_TYPE_ID in ("RETAIL_STORE", "OUTLET_STORE")
	)
	and os.STATUS_ID = "ORDER_COMPLETED"
	and os.STATUS_DATETIME 
		between "2023-01-01 00:00:00" 
		and date_add("2023-01-01 00:00:00", interval 25 day)
;
```