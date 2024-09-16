**Query:** Fetch all the physical items ordered in the month of September 2023.

**Query cost**: 21262.20

```sql
select
	oi.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	os.STATUS_ID,
	p.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	os.STATUS_DATETIME ITEM_STATUS
from order_item oi
join order_status os
	on os.ORDER_ID = oi.ORDER_ID
	and os.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
	and os.STATUS_ID = "ITEM_CREATED"
join product p
	on p.PRODUCT_ID = oi.PRODUCT_ID
join product_type pt
	on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
	and pt.IS_PHYSICAL = "Y"
where
	extract(MONTH from os.STATUS_DATETIME) = 9
	and extract(YEAR from os.STATUS_DATETIME) = 2023
;
```
