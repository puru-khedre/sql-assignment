**Query:** Fetch the following columns for created orders. These should be sales orders.

- ORDER_ID
- TOTAL_AMOUNT
- PAYMENT_METHOD
- SHOPIFY_ORDER_NAME

NOTE:

1. The total amount represents the total amount of the order.
2. The payment method is the method by which payment was made, like Cash, mastercard, visa, paypal, etc.

**Query cost**: 5591.60

```sql
select
	oh.ORDER_ID ORDER_ID,
	oh.GRAND_TOTAL TOTAL_AMOUNT,
	pmt.DESCRIPTION PAYMENT_METHOD,
	oi.ORDER_IDENTIFICATION_TYPE_ID,
	oi.ID_VALUE
from
	order_header oh
join order_identification oi
	on
	oi.ORDER_ID = oh.ORDER_ID
	and oi.ORDER_IDENTIFICATION_TYPE_ID = "SHOPIFY_ORD_NAME"
	and oh.ORDER_TYPE_ID = 'SALES_ORDER'
	and oh.STATUS_ID = "ORDER_CREATED"
join order_payment_preference opp,
	payment_method_type pmt
where
	opp.ORDER_ID = oh.ORDER_ID
	and opp.PAYMENT_METHOD_TYPE_ID = pmt.PAYMENT_METHOD_TYPE_ID
	and (oi.THRU_DATE is null
		or oi.THRU_DATE > curdate())
;
```

![alt text](image.png)

| ORDER_ID | TOTAL_AMOUNT | PAYMENT_METHOD | ORDER_IDENTIFICATION_TYPE_ID | ID_VALUE   |
| -------- | ------------ | -------------- | ---------------------------- | ---------- |
| 37140    | 109.03       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10575 |
| 37141    | 218.05       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10577 |
| 37142    | 109.03       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10576 |
| 37143    | 108.84       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10578 |
| 37143    | 108.84       | Ext Gift Card  | SHOPIFY_ORD_NAME             | SMUS#10578 |
| 37146    | 298.02       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10582 |
| 37147    | 23.94        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10581 |
| 37151    | 11.97        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10584 |
| 37152    | 11.97        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#10583 |
| 38810    | 179.73       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11509 |
| 38811    | 41.97        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11508 |
| 38812    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11507 |
| 38813    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11506 |
| 38814    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11505 |
| 38815    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11504 |
| 38816    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11503 |
| 38817    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11502 |
| 38818    | 59.91        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11501 |
| 38819    | 74.88        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11510 |
| 38820    | 207.06       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11511 |
| 38821    | 74.88        | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#11512 |
| 42911    | 150.95       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#13258 |
| 42920    | 384.50       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#13259 |
| 42921    | 399.90       | Ext VISA       | SHOPIFY_ORD_NAME             | SMUS#13257 |
