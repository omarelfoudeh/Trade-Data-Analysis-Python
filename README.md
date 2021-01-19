# Trade-Data-Analysis-Python
Analyse Forex trade data with python


import pandas as pd
import numpy as np
%matplotlib inline
import matplotlib.pyplot as plt
import datetime
from dateutil.relativedelta import relativedelta
from datetime import date

d_parser = lambda x: pd.datetime.strptime(x,'%Y.%m.%d %H:%M:%S')
df = pd.read_excel (r'C:\Users\omarf\OneDrive\Desktop\TRADING.xlsx', parse_dates=['Open Time'], date_parser=d_parser)
#deals = pd.read_excel (r'C:\Users\omarf\OneDrive\Desktop\deals.xlsx', parse_dates=['Close Time'], date_parser=d_parser)

#EXPOSURE
df['Volume2'] = np.where(df['Type'] == 'sell', df['Volume'] *-1, df['Volume'])
df['Exposure'] = df.groupby(['Symbol'])['Volume2'].cumsum()


#DURATION
df['Open Time'] = pd.to_datetime(df['Open Time']).astype('datetime64[ns]') 
df['Close Time'] = pd.to_datetime(df['Close Time']).astype('datetime64[ns]')
df['Duration'] = df['Close Time'] - df['Open Time'] 


df.set_index('Open Time')

#CLOSED PROFIT


df.head()
