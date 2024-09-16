**Query:** In the past month, which store has the highest number of one-day shipped orders?

**Query cost:** 25969

**Solution:**

```sql
select
	f.FACILITY_ID,
	f.FACILITY_NAME,
	count(oisg.ORDER_ID) TOTAL_ORDERS
from
	order_item_ship_group oisg
join facility f
	on f.FACILITY_ID = oisg.FACILITY_ID
	and f.FACILITY_TYPE_ID in ("RETAIL_STORE", "OUTLET_STORE")
	and oisg.SHIPMENT_METHOD_TYPE_ID = "NEXT_DAY"
	and oisg.ORDER_ID in (
	select
		oh.ORDER_ID
	from
		order_header oh
	join order_status os
		on os.ORDER_ID = oh.ORDER_ID
		and oh.STATUS_ID = "ORDER_COMPLETED"
		and oh.STATUS_ID = os.STATUS_ID
		and (datediff(date_sub(curdate(), interval day(curdate()) day ), os.STATUS_DATETIME) between 0 and 30)
	)
order by
	TOTAL_ORDERS
;
```

| FACILITY_ID | FACILITY_NAME | TOTAL_ORDERS |
| ----------- | ------------- | ------------ |
| 1           | 1 - Store 1   | 1            |

![alt text](image.png)
