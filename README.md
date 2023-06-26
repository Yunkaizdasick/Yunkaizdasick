from datetime import datetime
import pandas as pd
from backtesting import Backtest, Strategy
from backtesting.lib import crossover
from ta.trend import sma_indicator
df = pd.read_csv("D:\Stutdy Documents\Data Analyst\AI\REE.csv")
df = df.set_index('Date')
df['SMA 50'] = sma_indicator(close = df['Close'], window = 50)
df['SMA 200'] = sma_indicator(close = df['Close'], window = 200)
df.loc[
    (df['SMA 50'] > df['SMA 200'])
    & (df['SMA 50'].shift(1) <= df['SMA 200'].shift(1)), 'position'] = 1
df.loc[
    (df['SMA 50'] < df['SMA 200'])
    & (df['SMA 50'].shift(1) >= df['SMA 200'].shift(1)), 'position'] = -1
df[df['position'].notnull()] 
