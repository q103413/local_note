**FEATURE ENGINEERING**

- As indicated in the introduction, in the current problem, we will focus on `technical indicators` as part of our `feature engineering` approach in an attempt to introduce more relevant features into the `feature matrix`.
- It's interesting to know (in the context of a `digital asset` ), which features have impact on the model's performance, if any.

**Specifically:**

> - `Moving Average` : A moving average provides an indication of the trend of the price movement by reducing the amount of noise.
> - `Stochastic Oscillator %K and %D` : A stochastic oscillator is a momentum indicator comparing a particular closing price of a security to a range of its prices over a certain period of time. %K and %D are slow and fast indicators.
> - `Relative Strength Index(RSI)` : It is a momentum indicator that measures the magnitude of recent price changes to evaluate overbought or oversold conditions in the price of a stock or other asset. Ranging from [0,100]. **Asset -> 70: asset deemed overbought**. **Asset -> 30: asset getting undersold & undervalued.**
> - `Rate Of Change(ROC)`: It is a momentum oscillator, which measures the percentage change between the current price and the n period past price. Assets with **higher ROC values** are considered more likely to be overbought & **lower ROC**; more likely to be oversold.
> - `Momentum (MOM)` : It is the rate of acceleration of a security's price or volume; the speed at which the price is changing.

Can be all be potentially useful to model the target variable, `signal`, with of course varing degress of influence.

In [16]:

```
df_tr2 = df_tr1.copy()  # Create duplicate dataframe & add features to it
df_te2 = df_tr2.copy()
```

In [17]:

```
''' Technical Indicators '''

#Calculation of moving average
def ma(df, n):
    return pd.Series(df['Close'].rolling(n, min_periods=n).mean(), name='MA_' + str(n))

# exponentially weighted moving average 
def ema(df, n):
    return pd.Series(df['Close'].ewm(span=n,min_periods=n).mean(), name='EMA_' + str(n))

#Calculation of price momentum
def mom(df, n):     
    return pd.Series(df.diff(n), name='Momentum_' + str(n))  

# rate of change
def roc(df, n):  
    M = df.diff(n - 1) ; N = df.shift(n - 1)  
    return pd.Series(((M / N) * 100), name = 'ROC_' + str(n)) 

# relative strength index
def rsi(df, period):
    delta = df.diff().dropna()
    u = delta * 0; d = u.copy()
    u[delta > 0] = delta[delta > 0]; d[delta < 0] = -delta[delta < 0]
    u[u.index[period-1]] = np.mean( u[:period] ) #first value is sum of avg gains
    u = u.drop(u.index[:(period-1)])
    d[d.index[period-1]] = np.mean( d[:period] ) #first value is sum of avg losses
    d = d.drop(d.index[:(period-1)])
    rs = u.ewm(com=period-1, adjust=False).mean() / d.ewm(com=period-1, adjust=False).mean()
    return 100 - 100 / (1 + rs)

# stochastic oscillators slow & fast
def sto(close, low, high, n,id): 
    stok = ((close - low.rolling(n).min()) / (high.rolling(n).max() - low.rolling(n).min())) * 100
    if(id is 0):
        return stok
    else:
        return stok.rolling(3).mean()
```

*unfold_more*Show hidden code

In [19]:

```
tech_indi(df_tr2) # add technical features to training set
tech_indi(df_te2,tr_id=False) # add technical features to test set
```

00:00Jul 7, 202001:0002:0003:0004:0005:0006:0007:0008:009240926092809300932093409360

MA21MA63MA252Moving Average (window=21,63,252)











00:00Jul 7, 202001:0002:0003:0004:0005:0006:0007:0008:009240926092809300932093409360

EMA10EMA30EMA200Exponential Moving Average (window=10,30,200)











00:00Jul 7, 202001:0002:0003:0004:0005:0006:0007:0008:00−60−40−2002040

MOM10MOM30Momentum











00:00Jul 7, 202001:0002:0003:0004:0005:0006:0007:0008:0020304050607080

RSI10RSI30RSI200Relative Strength Index











00:00Jul 7, 202001:0002:0003:0004:0005:0006:0007:0008:00020406080100

%K10%K30%K200Stochastic Oscillators (slow)











00:00Jul 7, 202001:0002:0003:0004:0005:0006:0007:0008:00020406080100

%D10%D30%D200Stochastic Oscillators (Fast)











In [20]:

```
# All the current features
df_tr2.columns
```

Out[20]:

```
Index(['Open', 'High', 'Low', 'Close', 'Volume_(BTC)', 'Volume_(Currency)',
       'Weighted_Price', 'signal', 'MA21', 'MA63', 'MA252', 'EMA10', 'EMA30',
       'EMA200', 'MOM10', 'MOM30', 'RSI10', 'RSI30', 'RSI200', '%K10', '%K30',
       '%K200', '%D10', '%D30', '%D200'],
      dtype='object')
```

### **3.2 | Updated Feature Model Features**

**UPDATED FEATURE LINEAR CORRELATION**

- Having created new features; `MA`,`EMA`,`MOM`,`RSI`,`%K/%D`,
- let's investigate the linear correlation of these new featuers to the target variable & compare to the `baseline dataset` features

In [21]:

```
corrMat(df_tr2,'signal',figsize=(15,0.5))
```