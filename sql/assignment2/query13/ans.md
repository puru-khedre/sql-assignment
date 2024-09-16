**Query:** Fetch the following details for orders completed in August of 2023.

- PRODUCT_ID
- PRODUCT_TYPE_ID
- PRODUCT_STORE_ID
- TOTAL_QUANTITY
- INTERNAL_NAME
- FACILITY_ID
- EXTERNAL_ID
- FACILITY_TYPE_ID
- ORDER_HISTORY_ID
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- SHIP_GROUP_SEQ_ID

**Query cost**: 11878.60

```sql
select
	p.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	oh.PRODUCT_STORE_ID,
	oi.QUANTITY TOTAL_QUANTITY,
	p.INTERNAL_NAME,
	f.FACILITY_ID,
	oh.EXTERNAL_ID,
	f.FACILITY_TYPE_ID,
	oh2.ORDER_HISTORY_ID,
	oh.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	oi.SHIP_GROUP_SEQ_ID
from
	order_header oh
join order_status os
on
	os.ORDER_ID = oh.ORDER_ID
	and os.STATUS_ID = "ORDER_COMPLETED"
	and year(os.STATUS_DATETIME) = 2023
	and month(os.STATUS_DATETIME) = 8
join order_item oi
on
	oh.ORDER_ID = oi.ORDER_ID
join product p
on
	p.PRODUCT_ID = oi.PRODUCT_ID
join order_item_ship_group_assoc oisga
on
	oisga.ORDER_ID = oi.ORDER_ID
	and oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg
on
	oisg.ORDER_ID = oisga.ORDER_ID
	and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
join facility f
on
	oisg.FACILITY_ID = f.FACILITY_ID
join order_history oh2
on
	oh2.ORDER_ID = oh.ORDER_ID
	and oh2.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
	and oh2.SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID
;
```
