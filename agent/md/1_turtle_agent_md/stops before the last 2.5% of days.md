Looking at line 42 in the `buy_stock` function:

```python
for i in range(real_movement.shape[0] - int(0.025 * len(df))):
```

## Explanation

This creates a loop that iterates through most days of stock data, **but stops before the last 2.5% of days**.

### Breaking it down:

**`real_movement.shape[0]`**
- Gets the total number of rows (days) in the price data
- Example: If you have 252 trading days, this equals 252

**`len(df)`**
- Length of the original dataframe (also number of days)

**`0.025 * len(df)`**
- Calculates 2.5% of total days
- Example: `0.025 * 252 = 6.3` days

**`int(0.025 * len(df))`**
- Converts to integer: `6` days

**`real_movement.shape[0] - int(0.025 * len(df))`**
- Subtracts 2.5% from the end
- Example: `252 - 6 = 246`

**`range(246)`**
- Creates a loop from day 0 to day 245 (stops at 246)

### Why stop early?

This reserves the **last 2.5% of data** for validation/testing purposes. By not trading on these days, you can:

1. **Avoid edge effects** - Can't execute sell orders that might need future price data
2. **Reserve test data** - Keep final days as unseen data to evaluate strategy performance
3. **Prevent lookahead bias** - Ensure the model doesn't "peek" at the very end of the dataset

### Visual Example:

```
Total days: [0, 1, 2, ... 245, 246, 247, 248, 249, 250, 251]
Trading on: [0, 1, 2, ... 245] ← Loop stops here
Reserved:                        [246, 247, 248, 249, 250, 251] ← Last 2.5%
```

This is a common practice in backtesting trading strategies to maintain data integrity!