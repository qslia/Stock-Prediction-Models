`.rolling()` is a pandas method that creates a **rolling window** (also called moving window or sliding window) over your data. It's used to calculate statistics over a sliding window of consecutive rows.

## Basic Concept

`rolling(2)` means "create a window that looks at 2 consecutive rows at a time":

```python
# Example data
[10, 20, 30, 40, 50]

# With rolling(2):
# Row 0: [NaN] - not enough data (need 2 rows)
# Row 1: [10, 20] - window contains rows 0-1
# Row 2: [20, 30] - window contains rows 1-2
# Row 3: [30, 40] - window contains rows 2-3
# Row 4: [40, 50] - window contains rows 3-4
```

## Common Usage

After creating a rolling window, you typically apply an aggregation function:

```python
test_df.shift(1).rolling(2).mean()   # Rolling average of 2 periods
test_df.shift(1).rolling(2).max()    # Rolling maximum of 2 periods
test_df.shift(1).rolling(2).min()    # Rolling minimum of 2 periods
test_df.shift(1).rolling(2).sum()    # Rolling sum of 2 periods
```

## Your Code Breakdown

```python
test_df.shift(1).rolling(2)
```

1. **`.shift(1)`**: Shifts all values down by 1 row (previous day's values)
2. **`.rolling(2)`**: Creates a 2-period rolling window on the shifted data

This is commonly used in trading strategies (like in the turtle-agent) to look at historical data without including the current period.

## Real Example from Your Notebook

Looking at the turtle-agent code:

```python
signals['RollingMax'] = (signals.trend.shift(1).rolling(count).max())
signals['RollingMin'] = (signals.trend.shift(1).rolling(count).min())
```

This calculates:
- **RollingMax**: The maximum price over the last `count` periods (excluding today)
- **RollingMin**: The minimum price over the last `count` periods (excluding today)

This prevents "look-ahead bias" in trading strategies - you're only using past data to make decisions, not the current day's data.