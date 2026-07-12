# Data Science Project 1 

okay so this is my first data science project from DecodeLabs. basically we had to clean a messy e-commerce dataset and make it ready for machine learning. sounds simple but there was actually a lot going on.

---

## the dataset

1200 rows, 14 columns. orders data — stuff like product names, prices, payment methods, order status etc. loaded it straight from google sheets, no downloading needed:

```python
url = "the google sheets export link"
df = pd.read_csv(url)
```

---

## what I did

### missing values
checked which columns had missing data. turns out only `CouponCode` was missing (25.75% of rows). everything else was clean which was surprising honestly.

for `CouponCode` I just left it as NaN — missing coupon obviously means the person didn't use one. no need to fill that with anything.

### outliers
ran IQR on all numeric columns to find outliers. only `TotalPrice` had 8 outliers. instead of deleting those rows I just capped the values at the boundary using `numpy.clip()` — this way we keep all 1200 rows.

### feature engineering
made some new columns from existing data:

- `RevenuePerItem` — total price divided by quantity
- `CouponUsed` — 1 if coupon was used, 0 if not
- `OrderMonth`, `OrderYear`, `OrderDay` — extracted from the date column
- `CartUtilization` — how much of the cart was actually purchased

---

## libraries
```
pandas, numpy, sklearn
```

---

## honestly what I learned
- NaN doesn't always need to be fixed, sometimes it means something
- never use loops in pandas, there's always a better way
- outliers are better capped than deleted most of the time
- cleaning data is like 80% of the actual work lol
