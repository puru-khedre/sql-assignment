**Query:** In New York, which product has the highest sales?

**Query cost:** 14,565.85

**Solution:**
```sql
select oi.PRODUCT_ID, sum(oi.QUANTITY) TOTAL_QTT
from order_item oi 
join order_contact_mech ocm 
	on ocm.CONTACT_MECH_PURPOSE_TYPE_ID = "SHIPPING_LOCATION"
	and oi.ORDER_ID = ocm.ORDER_ID
join postal_address pa 
	on ocm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID 
	and pa.CITY = "New York"
group by oi.PRODUCT_ID 
order by TOTAL_QTT desc
;
```
