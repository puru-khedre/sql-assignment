**Query:** Fetch the following columns for completed return items of SM_STORE for ecom return channel.
- RETURN_ID 
- ORDER_ID
- PRODUCT_STORE_ID 
- STATUS_DATETIME
- ORDER_NAME 
- FROM_PARTY_ID 
- RETURN_DATE 
- ENTRY_DATE
- RETURN_CHANNEL_ENUM_ID

**Query cost**: 2113.72

```sql
select
   rh.RETURN_ID,
   ri.RETURN_ITEM_SEQ_ID,
   oh.ORDER_ID,
   oh.PRODUCT_STORE_ID,
   rs.STATUS_DATETIME,
   oh.ORDER_NAME,
   rh.FROM_PARTY_ID,
   rh.RETURN_DATE,
   rh.ENTRY_DATE,
   rh.RETURN_CHANNEL_ENUM_ID
from return_header rh
join return_item ri
   on rh.RETURN_ID = ri.RETURN_ID
   and rh.RETURN_CHANNEL_ENUM_ID = 'ECOM_RTN_CHANNEL'
join  order_header oh
   on ri.ORDER_ID = oh.ORDER_ID
   and oh.PRODUCT_STORE_ID ="SM_STORE"
join return_status rs
   on ri.RETURN_ID = rs.RETURN_ID
   and ri.RETURN_ITEM_SEQ_ID = rs.RETURN_ITEM_SEQ_ID
   and rs.STATUS_ID = "RETURN_COMPLETED";
```
