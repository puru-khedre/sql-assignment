**Query:** Leading up to the New Year, what is the count of orders shipped from stores in the 25 days preceding the New Year?

**Query cost:** 21,603.31

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
	and DATEDIFF("2023-01-01 00:00:00", os.STATUS_DATETIME) between 0 and 25
;
```