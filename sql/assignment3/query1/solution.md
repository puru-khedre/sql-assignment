**Query:** How many single-item orders were fulfilled from warehouses in the last month?

**Query cost:** 23113.99

**Solution:**
```sql
select
	count(*)
from
	order_item oi
join order_item_ship_group_assoc oisga
	on oi.ORDER_ID in (
	select
		oi.ORDER_ID
	from
		order_item oi
	group by
		oi.ORDER_ID
	having
		count(oi.ORDER_ITEM_SEQ_ID)= 1
	)
	and oi.ORDER_ID = oisga.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg
	on oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
	and oisg.ORDER_ID = oisga.ORDER_ID
join facility f
	on oisg.FACILITY_ID = f.FACILITY_ID
	and f.FACILITY_TYPE_ID = "WAREHOUSE"
join order_status os
	on os.STATUS_ID = "ORDER_COMPLETED"
	and os.ORDER_ID = oi.ORDER_ID
where
	datediff(curdate(), os.STATUS_DATETIME) <=30
;
```