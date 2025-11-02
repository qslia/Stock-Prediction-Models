[1 tool called]

Based on the notebook, here's the purpose of setting signals in this **Turtle Trading Agent**:

## Purpose of Signals

The signals are **trading indicators** that tell the agent when to buy or sell stocks. They implement a **breakout trading strategy** (Turtle Trading):

```16:18:agent/1.turtle-agent.ipynb
signals = pd.DataFrame(index=df.index)
signals['signal'] = 0.0
signals['trend'] = df['Close']
signals['RollingMax'] = (signals.trend.shift(1).rolling(count).max())
signals['RollingMin'] = (signals.trend.shift(1).rolling(count).min())
```

### Signal Values:

- **`signal = 1`** → **BUY signal**: Price breaks above the rolling minimum (upward breakout)
- **`signal = -1`** → **SELL signal**: Price breaks below the rolling maximum (downward breakout)  
- **`signal = 0`** → **HOLD**: No action

### The Logic:

```18:18:agent/1.turtle-agent.ipynb
signals.loc[signals['RollingMax'] < signals.trend, 'signal'] = -1
signals.loc[signals['RollingMin'] > signals.trend, 'signal'] = 1
```

1. **Buy (`signal = 1`)**: When current price is **below** the rolling minimum (price is trending up - potential breakout upward)
2. **Sell (`signal = -1`)**: When current price is **below** the rolling maximum (price is trending down - potential breakout downward)

### How It's Used:

The `buy_stock()` function reads these signals and executes trades accordingly:
- When it encounters `signal == 1`, it **buys** stock
- When it encounters `signal == -1`, it **sells** stock (if it has inventory)

This is a **trend-following strategy** based on the famous Turtle Trading system, which looks for price breakouts to identify entry and exit points.