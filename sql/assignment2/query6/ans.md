**Query:** Fetch all the physical items completed from Warehouse in September of 2023.

**Query cost**: 9809

```sql
select
	os.STATUS_ID ITEM_STATUS,
	oi.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	oi.SHIP_GROUP_SEQ_ID,
	f.FACILITY_ID,
	f.FACILITY_TYPE_ID,
	p.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	pt.IS_PHYSICAL
from
	order_item oi
join order_status os
	on os.ORDER_ID = oi.ORDER_ID
	and os.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
	and os.STATUS_ID = "ITEM_COMPLETED"
join order_item_ship_group_assoc oisga
	on oi.ORDER_ID = oisga.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg
	on oisga.SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID
	and oisga.ORDER_ID = oisg.ORDER_ID
join facility f
	on oisg.FACILITY_ID = f.FACILITY_ID
	and f.FACILITY_TYPE_ID in (
	select
		ft.FACILITY_TYPE_ID
	from
		facility_type ft
	where
		ft.PARENT_TYPE_ID = "DISTRIBUTION_CENTER"
	)
join product p
	on p.PRODUCT_ID = oi.PRODUCT_ID
join product_type pt
	on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
	and pt.IS_PHYSICAL = "Y"
where
	os.STATUS_DATETIME between "2023-09-01" and "2023-09-29";
```
