**Query:** On a city-wise basis, what is the analysis of returns?

**Query cost:** 116.2

```sql
select
	pa.CITY ,
	count(rcm.RETURN_ID)
from
	return_contact_mech rcm
join postal_address pa on
	pa.CONTACT_MECH_ID = rcm.CONTACT_MECH_ID
group by
	pa.CITY ;
;
```
