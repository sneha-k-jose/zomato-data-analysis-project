# zomato-data-analysis-project  zomato data analysis project
step 1 : import libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
​
step 2 create data frame
dataframe = pd.read_csv("Zomato data .csv")
print(dataframe)
                      name online_order book_table   rate  votes  \
0                    Jalsa          Yes        Yes  4.1/5    775   
1           Spice Elephant          Yes         No  4.1/5    787   
2          San Churro Cafe          Yes         No  3.8/5    918   
3    Addhuri Udupi Bhojana           No         No  3.7/5     88   
4            Grand Village           No         No  3.8/5    166   
..                     ...          ...        ...    ...    ...   
143       Melting Melodies           No         No  3.3/5      0   
144        New Indraprasta           No         No  3.3/5      0   
145           Anna Kuteera          Yes         No  4.0/5    771   
146                 Darbar           No         No  3.0/5     98   
147          Vijayalakshmi          Yes         No  3.9/5     47   

     approx_cost(for two people) listed_in(type)  
0                            800          Buffet  
1                            800          Buffet  
2                            800          Buffet  
3                            300          Buffet  
4                            600          Buffet  
..                           ...             ...  
143                          100          Dining  
144                          150          Dining  
145                          450          Dining  
146                          800          Dining  
147                          200          Dining  

[148 rows x 7 columns]
dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1/5	775	800	Buffet
1	Spice Elephant	Yes	No	4.1/5	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8/5	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7/5	88	300	Buffet
4	Grand Village	No	No	3.8/5	166	600	Buffet
dataframe.tail()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
143	Melting Melodies	No	No	3.3/5	0	100	Dining
144	New Indraprasta	No	No	3.3/5	0	150	Dining
145	Anna Kuteera	Yes	No	4.0/5	771	450	Dining
146	Darbar	No	No	3.0/5	98	800	Dining
147	Vijayalakshmi	Yes	No	3.9/5	47	200	Dining
convert data type of column rate
def handleRate(value):
    value = str(value).split('/')
    value=value[0];
    return float(value)
dataframe['rate']=dataframe['rate'].apply(handleRate)
print(dataframe.head())
                    name online_order book_table  rate  votes  \
0                  Jalsa          Yes        Yes   4.1    775   
1         Spice Elephant          Yes         No   4.1    787   
2        San Churro Cafe          Yes         No   3.8    918   
3  Addhuri Udupi Bhojana           No         No   3.7     88   
4          Grand Village           No         No   3.8    166   

   approx_cost(for two people) listed_in(type)  
0                          800          Buffet  
1                          800          Buffet  
2                          800          Buffet  
3                          300          Buffet  
4                          600          Buffet  
dataframe.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 148 entries, 0 to 147
Data columns (total 7 columns):
 #   Column                       Non-Null Count  Dtype  
---  ------                       --------------  -----  
 0   name                         148 non-null    object 
 1   online_order                 148 non-null    object 
 2   book_table                   148 non-null    object 
 3   rate                         148 non-null    float64
 4   votes                        148 non-null    int64  
 5   approx_cost(for two people)  148 non-null    int64  
 6   listed_in(type)              148 non-null    object 
dtypes: float64(1), int64(2), object(4)
memory usage: 8.2+ KB
type of resturant
dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1	775	800	Buffet
1	Spice Elephant	Yes	No	4.1	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7	88	300	Buffet
4	Grand Village	No	No	3.8	166	600	Buffet
sns.countplot(x=dataframe['listed_in(type)'])
plt.xlabel("type of resturant")
Text(0.5, 0, 'type of resturant')

conclusion - majority of the resturant falls in dinning category
dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1	775	800	Buffet
1	Spice Elephant	Yes	No	4.1	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7	88	300	Buffet
4	Grand Village	No	No	3.8	166	600	Buffet
grouped_data = dataframe.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})
plt.plot(result, c="BLUE",marker = "o")
plt.xlabel("Type of resturant", c="RED" , size = 20 )
plt.ylabel("votes" , c = "BLACK" , size = 20)
Text(0, 0.5, 'votes')

CONCLUSION - DINNING RESTURANTS HAS RECEIVED MAX VOTES
dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1	775	800	Buffet
1	Spice Elephant	Yes	No	4.1	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7	88	300	Buffet
4	Grand Village	No	No	3.8	166	600	Buffet
plt.hist(dataframe['rate'],bins=5)
plt.title("ratings distribution")
plt.show()

conclusion - the majority rest recieved ratings from 3.5 to 4
Average order spending by customer
dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1	775	800	Buffet
1	Spice Elephant	Yes	No	4.1	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7	88	300	Buffet
4	Grand Village	No	No	3.8	166	600	Buffet
couple_data = dataframe['approx_cost(for two people)']
sns.countplot(x=couple_data)
<Axes: xlabel='approx_cost(for two people)', ylabel='count'>

dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1	775	800	Buffet
1	Spice Elephant	Yes	No	4.1	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7	88	300	Buffet
4	Grand Village	No	No	3.8	166	600	Buffet
plt.figure(figsize = (6,6))
sns.boxplot(x = 'online_order' , y = 'rate' , data = dataframe)
<Axes: xlabel='online_order', ylabel='rate'>

dataframe.head()
name	online_order	book_table	rate	votes	approx_cost(for two people)	listed_in(type)
0	Jalsa	Yes	Yes	4.1	775	800	Buffet
1	Spice Elephant	Yes	No	4.1	787	800	Buffet
2	San Churro Cafe	Yes	No	3.8	918	800	Buffet
3	Addhuri Udupi Bhojana	No	No	3.7	88	300	Buffet
4	Grand Village	No	No	3.8	166	600	Buffet
conclusion - offline order received lower rating in comparison to online orders
pivot_table = dataframe.pivot_table(index = 'listed_in(type)' , columns = 'online_order' , aggfunc = "size"  , fill_value=0)
sns.heatmap(pivot_table , annot = True , cmap = "YIGnBu" , fmt = 'd')
plt.title("Heatmap")
plt.xlabel("Online_Order")
plt.ylabel("Listed In (Type)")
plt.show()
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
Cell In[33], line 2
      1 pivot_table = dataframe.pivot_table(index = 'listed_in(type)' , columns = 'online_order' , aggfunc = "size"  , fill_value=0)
----> 2 sns.heatmap(pivot_table , annot = True , cmap = "YIGnBu" , fmt = 'd')
      3 plt.title("Heatmap")
      4 plt.xlabel("Online_Order")

File ~/anaconda3/lib/python3.11/site-packages/seaborn/matrix.py:446, in heatmap(data, vmin, vmax, cmap, center, robust, annot, fmt, annot_kws, linewidths, linecolor, cbar, cbar_kws, cbar_ax, square, xticklabels, yticklabels, mask, ax, **kwargs)
    365 """Plot rectangular data as a color-encoded matrix.
    366 
    367 This is an Axes-level function and will draw the heatmap into the
   (...)
    443 
    444 """
    445 # Initialize the plotter object
--> 446 plotter = _HeatMapper(data, vmin, vmax, cmap, center, robust, annot, fmt,
    447                       annot_kws, cbar, cbar_kws, xticklabels,
    448                       yticklabels, mask)
    450 # Add the pcolormesh kwargs here
    451 kwargs["linewidths"] = linewidths

File ~/anaconda3/lib/python3.11/site-packages/seaborn/matrix.py:163, in _HeatMapper.__init__(self, data, vmin, vmax, cmap, center, robust, annot, fmt, annot_kws, cbar, cbar_kws, xticklabels, yticklabels, mask)
    160 self.ylabel = ylabel if ylabel is not None else ""
    162 # Determine good default values for the colormapping
--> 163 self._determine_cmap_params(plot_data, vmin, vmax,
    164                             cmap, center, robust)
    166 # Sort out the annotations
    167 if annot is None or annot is False:

File ~/anaconda3/lib/python3.11/site-packages/seaborn/matrix.py:217, in _HeatMapper._determine_cmap_params(self, plot_data, vmin, vmax, cmap, center, robust)
    215         self.cmap = cm.icefire
    216 elif isinstance(cmap, str):
--> 217     self.cmap = get_colormap(cmap)
    218 elif isinstance(cmap, list):
    219     self.cmap = mpl.colors.ListedColormap(cmap)

File ~/anaconda3/lib/python3.11/site-packages/seaborn/_compat.py:133, in get_colormap(name)
    131 """Handle changes to matplotlib colormap interface in 3.6."""
    132 try:
--> 133     return mpl.colormaps[name]
    134 except AttributeError:
    135     return mpl.cm.get_cmap(name)

File ~/anaconda3/lib/python3.11/site-packages/matplotlib/cm.py:82, in ColormapRegistry.__getitem__(self, item)
     80     return self._cmaps[item].copy()
     81 except KeyError:
---> 82     raise KeyError(f"{item!r} is not a known colormap name") from None

KeyError: "'YIGnBu' is not a known colormap name"

CONCLUSION = DINING REST PRIMARLIY ACCEPT OFFLINE ORDERS
​
​
​
