**Query:** What is the total number of orders originating from New York?

**Query cost:** 7,942.97

**Solution:**
```sql
select
	count(distinct ORDER_ID)
from
	order_contact_mech ocm
join postal_address pa 
	on
	ocm.CONTACT_MECH_PURPOSE_TYPE_ID = "BILLING_LOCATION"
	and ocm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
where
	pa.CITY = "New York"
;
```