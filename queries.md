# Queries for Task 2

## What are the top 5 brands by receipts scanned for most recent month?

```sql
SELECT b.name as TopBrands
FROM Receipt r INNER JOIN Receipt_Item ri ON(r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH) AND r.dateScanned <= CURDATE() AND r.receiptId = ri.receiptId) INNER JOIN Item i ON(ri.itemId = i.itemId) INNER JOIN Brands b ON(i.brandId = b.brandId)
GROUP BY b.brandId
ORDER BY COUNT(*) DESC
LIMIT 5;
```

## When considering average spend from receipts with 'rewardsReceiptStatus' of 'Accepted' or 'Rejected', which is greater?

```sql
-- To find which is greater we will write a simple if

SELECT IF(
    (
        SELECT AVG(totalSpent) as avgSpentForAc
        FROM Receipt
        WHERE rewardsReceiptStatus = 'Accepted'
    ) > (
        SELECT AVG(totalSpent) as avgSpentForAc
        FROM Receipt
        WHERE rewardsReceiptStatus = 'Rejected'
    ), "Average spent from receipts with rewardsReceiptStatus = Accepted is greater", "Average spent from receipts with rewardsReceiptStatus = Rejected is greater") as Which_Is_Greater_Status_AC_or_RJ;
```

## How does the ranking of the top 5 brands by receipts scanned for the recent month compare to the ranking for the previous month?

```sql
-- We can get the top brands by receipts scanned for the current month using query:
-- QUERY 1:
SELECT b.name as name, COUNT(_) as cnt
FROM Receipt r INNER JOIN Receipt_Item ri ON(r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH) AND r.dateScanned <= CURDATE() AND r.receiptId = ri.receiptId) INNER JOIN Item i ON(ri.itemId = i.itemId) INNER JOIN Brands b ON(i.brandId = b.brandId)
GROUP BY b.brandId
ORDER BY COUNT(_) DESC

-- We can get ranking of the brands by receipts scanned for the previous month using query:
-- QUERY 2:
SELECT b.name as name, , COUNT(_) as cnt
FROM Receipt r INNER JOIN Receipt_Item ri ON(r.dateScanned >= DATE_SUB(CURDATE(), INTERVAL 2 MONTH) AND r.dateScanned <= DATE_SUB(CURDATE(), INTERVAL 1 MONTH) AND r.receiptId = ri.receiptId) INNER JOIN Item i ON(ri.itemId = i.itemId) INNER JOIN Brands b ON(i.brandId = b.brandId)
GROUP BY b.brandId
ORDER BY COUNT(_) DESC

-- -> We can rank both resultsets and then combine them by brand name. By subtracting their ranks, we can identify which brands have improved in sales and which have experienced a decline.
```
