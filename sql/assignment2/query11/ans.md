**Query:** Fetch all the customers created in June 2023.

**Query cost**: 4641796

```sql
select
	p.PARTY_ID,
	p.PARTY_TYPE_ID,
	p.CREATED_DATE,
	pr.ROLE_TYPE_ID
from party p
join party_role pr
on pr.ROLE_TYPE_ID = "CUSTOMER"
where p.CREATED_DATE between "2023-06-01" and "2023-06-30"
;
```
