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

## When considering total number of items purchased from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?

```sql
SELECT IF(
    (
        SELECT COUNT(*) as acceptedCount
        FROM Receipt r INNER JOIN Receipt_Item ri ON(r.receiptId = ri.receiptId)
        WHERE r.rewardsReceiptStatus = 'Accepted'
    ) > (
        SELECT COUNT(*) as rejectedCount
        FROM Receipt r INNER JOIN Receipt_Item ri ON(r.receiptId = ri.receiptId)
        WHERE r.rewardsReceiptStatus = 'Rejected'
    )
    , "Total number of items purchased from receipts with rewardsReceiptStatus = Accepted is greater", "Total number of items purchased from receipts with rewardsReceiptStatus = Rejected is greater"
) as Which_Is_Greater_Status_AC_or_RJ;
```
