The following code was presented as two different methods to achieve the **same** output:
```sql
-- 4) LIST ALL INVOICE INFORMATION WHERE BALANCE DUE IS > 0

-- AND LESS THAN THE AVERAGE BALANCE DUE
SELECT
	invoices.invoice_number,
	invoices.invoice_date,
	invoices.invoice_total - payment_total - credit_total AS balance_due
FROM
	invoices
WHERE
	(invoice_total - payment_total - credit_total) > 0 AND
	(invoice_total - payment_total - credit_total) <
		(SELECT AVG(invoice_total - payment_total - credit_total)
FROM 
	invoices
WHERE 
	invoice_total - payment_total - credit_total > 0 )
ORDER BY 
	invoice_total DESC;
  
-- OR THIS WAY:
  
SELECT
	invoice_number,
	invoice_date,
	invoice_total - payment_total - credit_total AS balance_due
FROM
	invoices
HAVING
	balance_due > 0 AND
	balance_due <
	(
		SELECT AVG(invoice_total - payment_total - credit_total)
		FROM invoices
		WHERE invoice_total - payment_total - credit_total > 0
	)
ORDER BY 
	invoice_total DESC;
```

The premise was that `HAVING` and `WHERE` are functionally **identical**. That is incorrect.

Consider the following code:
```sql {11} title="figure-1"
SELECT
	invoices.invoice_id,
	invoices.invoice_date,
	(invoice_total - credit_total - payment_total) AS balance_due
FROM
	invoices
HAVING
	balance_due > 0
	AND
	balance_due <
		(SELECT AVG(invoice_total - payment_total - credit_total) AS AVERAGE FROM invoices HAVING AVERAGE > 0)
ORDER BY
	invoice_total DESC;
```
We receive the following output:
```txt
"invoice_id" "invoice_date" "balance_due"
"113" "2014-08-01" "224.00"
"110" "2014-07-28" "90.36"
"89"  "2014-07-10" "85.31"
"100" "2014-07-22" "67.92"
"99"  "2014-07-21" "59.97"
"94"  "2014-07-18" "52.25"
"101" "2014-07-22" "30.75"
```
`HAVING` is executed near the very end of the query. Because of this, `aliases` defined in the respective `SELECT` statements can be used in `HAVING` clauses, as opposed to `WHERE` clauses. However, because of this, every operation of every preceding clause has been completed by the time `HAVING` comes to pass. In `figure-1`, the subquery is effectively executed first. So, for the subquery, the table exists in this state, right before `HAVING` is computed:

```sql title="figure-1-1"
(SELECT AVG(invoice_total - payment_total - credit_total) AS AVERAGE FROM invoices)
```

`Figure-1-1` is executed on the invoices table, using three columns to calculate the `AVG`. We can see the invoices table exists as such, via the statement `figure-1-2`:

```sql title="figure-1-2"
(SELECT invoice_total, payment_total, credit_total FROM invoices)
```
```txt
"invoice_total" "payment_total" "credit_total"
"3813.33" "3813.33" "0.00"
"40.20" "40.20" "0.00"
"138.75" "138.75" "0.00"
"144.70" "144.70" "0.00"
"15.50" "15.50" "0.00"
"42.75" "42.75" "0.00"
"172.50" "172.50" "0.00"
"95.00" "95.00" "0.00"
"601.95" "601.95" "0.00"
"42.67" "42.67" "0.00"
"42.50" "42.50" "0.00"
"662.00" "662.00" "0.00"
"16.33" "16.33" "0.00"
"6.00" "6.00" "0.00"
"856.92" "856.92" "0.00"
"9.95" "9.95" "0.00"
"10.00" "10.00" "0.00"
"104.00" "104.00" "0.00"
"116.54" "116.54" "0.00"
"6.00" "6.00" "0.00"
"4901.26" "4901.26" "0.00"
"108.25" "108.25" "0.00"
"9.95" "9.95" "0.00"
"1750.00" "1750.00" "0.00"
"129.00" "129.00" "0.00"
"10.00" "10.00" "0.00"
"207.78" "207.78" "0.00"
"109.50" "109.50" "0.00"
"450.00" "450.00" "0.00"
"63.40" "63.40" "0.00"
"7125.34" "7125.34" "0.00"
"953.10" "953.10" "0.00"
"220.00" "220.00" "0.00"
"127.75" "127.75" "0.00"
"1600.00" "1600.00" "0.00"
"565.15" "565.15" "0.00"
"36.00" "36.00" "0.00"
"61.50" "61.50" "0.00"
"37966.19" "37966.19" "0.00"
"639.77" "639.77" "0.00"
"53.75" "53.75" "0.00"
"400.00" "400.00" "0.00"
"21842.00" "21842.00" "0.00"
"19.67" "19.67" "0.00"
"2765.36" "2765.36" "0.00"
"224.00" "224.00" "0.00"
"1575.00" "1575.00" "0.00"
"33.00" "33.00" "0.00"
"16.33"    "16.33" "0.00"
"116.00"   "116.00" "0.00"
"2184.11"  "2184.11" "0.00"
"1083.58"  "1083.58" "0.00"
"46.21"    "46.21" "0.00"
"313.55"   "313.55" "0.00"
"40.75"    "40.75" "0.00"
"2433.00"  "2433.00" "0.00"
"1367.50"  "1367.50" "0.00"
"53.25"    "53.25" "0.00"
"13.75"    "13.75" "0.00"
"2312.20"  "2312.20" "0.00"
"25.67"    "25.67" "0.00"
"26.75"    "26.75" "0.00"
"2115.81"  "2115.81" "0.00"
"23.50"    "23.50" "0.00"
"6940.25"  "6940.25" "0.00"
"31.95"    "31.95" "0.00"
"1927.54"  "1927.54" "0.00"
"936.93"   "936.93" "0.00"
"175.00"   "175.00" "0.00"
"6.00"     "6.00" "0.00"
"108.50"   "108.50" "0.00"
"10.00"    "10.00" "0.00"
"290.00"   "290.00" "0.00"
"41.80"    "41.80" "0.00"
"27.00"    "27.00" "0.00"
"241.00"   "241.00" "0.00"
"904.14"   "904.14" "0.00"
"1962.13"  "1762.13" "200.00"
"2184.50"  "2184.50" "0.00"
"2318.03"  "2318.03" "0.00"
"26.25"    "26.25" "0.00"
"17.50"    "17.50" "0.00"
"39.77"    "39.77" "0.00"
"111.00"   "111.00" "0.00"
"158.00"   "158.00" "0.00"
"739.20"   "739.20" "0.00"
"60.00"    "60.00" "0.00"
"147.25"   "147.25" "0.00"
"85.31"    "0.00" "0.00"
"38.75"    "38.75" "0.00"
"32.70"    "32.70" "0.00"
"16.62"    "16.62" "0.00"
"162.75"   "162.75" "0.00"
"52.25"    "0.00" "0.00"
"600.00"   "600.00" "0.00"
"26881.40" "26881.40" "0.00"
"356.48"   "356.48" "0.00"
"579.42"   "0.00" "0.00"
"59.97"    "0.00" "0.00"
"67.92"    "0.00" "0.00"
"30.75"    "0.00" "0.00"
"20551.18" "0.00" "1200.00"
"2051.59"  "2051.59" "0.00"
"44.44"    "44.44" "0.00"
"503.20"   "0.00" "0.00"
"23517.58" "21221.63" "2295.95"
"3689.99"  "3689.99" "0.00"
"67.00"    "67.00" "0.00"
"1000.46"  "1000.46" "0.00"
"90.36"    "0.00" "0.00"
"22.57"    "22.57" "0.00"
"10976.06" "0.00" "0.00"
"224.00"   "0.00" "0.00"
"127.75"   "127.75" "0.00"
"8344.50"  "0.00" "0.00"
"8344.50"  "0.00" "0.00"
```

