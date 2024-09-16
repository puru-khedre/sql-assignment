**Query:** Find all the orders whose two or more items are canceled but the orders are still in the approved status.

**Query cost**: 5380

```sql
select
	oi.ORDER_ID,
	oh.STATUS_ID ORDER_STATUS,
	count(oh.ORDER_ID) ITEMS_COUNT
from order_header oh
join order_item oi
	on oi.ORDER_ID = oh.ORDER_ID
	and oh.STATUS_ID = "ORDER_APPROVED"
	and oi.STATUS_ID = "ITEM_CANCELLED"
group by oh.ORDER_ID
having ITEMS_COUNT>=2
;

```
