**Query:** Get all the appeasements in July month.

1. **How do we differentiate between returns and appeasements?**
	The key difference between them is that the return has some return items and in appeasements only return_header, and return_adjustment are present and the count of return items is zero. Basically, We use the return_adjustment entity to handle appeasements, nothing is actually returned so no return items are present.
1. **Get all the below fields**
	- RETURN_ID
	- ENTRY_DATE 
	- RETURN_ADJUSTMENT_TYPE_ID
	- AMOUNT
	- COMMENTS 
	- ORDER_ID
	- ORDER_DATE 
	- RETURN_DATE
	- PRODUCT_STORE_ID

**Query cost**: 973.80

```sql
select
	ra.RETURN_ID,
	rh.ENTRY_DATE,
	ra.RETURN_ADJUSTMENT_TYPE_ID,
	ra.AMOUNT,
	ra.COMMENTS,
	ra.ORDER_ID,
	oh.ORDER_DATE,
	rh.RETURN_DATE,
	oh.PRODUCT_STORE_ID
from return_adjustment ra
join return_header rh
on
	rh.RETURN_ID = ra.RETURN_ID
	and ra.RETURN_ADJUSTMENT_TYPE_ID = "APPEASEMENT"
join order_header oh
on
	oh.ORDER_ID = ra.ORDER_ID
where
	extract(month from rh.RETURN_DATE) = 7
	and extract(year from rh.RETURN_DATE) = 2023
;
```
