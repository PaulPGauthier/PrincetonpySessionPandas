# PrincetonpySessionPandas

Import Necessary Libraries

Pandas is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series

NumPy is an extension to the Python programming language, adding support for large, multi-dimensional arrays and matrices, along with a large library of high-level mathematical functions to operate on these arrays.

Matplotlib is a plotting library for the Python programming language and its numerical mathematics extension NumPy. There is also a procedural "pylab" interface based on a state machine (like OpenGL), designed to closely resemble that of MATLAB. Pandas makes use of matplotlib.

# 1. How to import libraries


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

By default I always call pandas: pd, numpy: np and matplotlib.pyplot: plt

A good practice, with Ipython would be to include, right after the import of librairies an inline caller. 


```python
import pandas as pd
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
%matplotlib inline   
mpl.rcParams["figure.figsize"] = (14, 10)
```

# 2. Verifying you have the right version of pandas

Python libraries are often updated. So regularly test for your version of the main librairies you are using. 


```python
pd.__version__,np.__version__
```




    (u'0.18.0', '1.10.0')



If your version is older, you can directly update it using Terminal:
    
conda update pandas

conda update matplotlib

conda update numpy

Once you did it, check your versions again


```python
pd.__version__,np.__version__
```




    (u'0.18.0', '1.10.0')



# 3. Working with real data

a. Import Data

There is multiple options in Pandas to import data. You could import different file format:
    - csv
    - excel
    - json
    - pickle
    - sql
    - ....

First define the path to a folder in your directory


```python
Path_CO2 = '/Users/paulgauthier/Documents/Postdoc/PUPC/Princetonpy/CO2.csv'
Path_H2O = '/Users/paulgauthier/Documents/Postdoc/PUPC/Princetonpy/H2O.csv'
Path_RaspPi = '/Users/paulgauthier/Documents/Postdoc/PUPC/Princetonpy/RaspPi.csv'
Path_O2 = '/Users/paulgauthier/Documents/Postdoc/PUPC/Princetonpy/O2.csv'
```

Now, import the data using the path you just created


```python
CO2 = pd.read_csv(Path_CO2)
Water = pd.read_csv(Path_H2O)
RaspPi = pd.read_csv(Path_RaspPi)
O2 = pd.read_csv(Path_O2)
```

You now have 4 dataframes containing the data from 4 csv files

You can do the same with Excel files


```python
Path_CO2_xls = '/Users/paulgauthier/Documents/Postdoc/PUPC/Princetonpy/CO2.xlsx'
CO2_xls = pd.read_excel(Path_CO2_xls)
```

Both dataframe should be exactly similar. We can test the Dimension of the DataFrame using the attribute "shape"


```python
CO2.shape
```




    (891, 7)



Compare the shape of the 2 dataframe. If they have the same shape then, equality should return True


```python
CO2.shape == CO2_xls.shape
```




    True



Show how the dataframe looks like by calling DataFrame name


```python
CO2=pd.read_csv(Path_CO2)
CO2.columns
```




    Index([u'gmtime', u'EPOCH_TIME', u'Conditions', u'Species', u'12CO2', u'13CO2',
           u'Delta_Raw'],
          dtype='object')




```python
CO2.columns=[CO2.loc[0].values]
CO2.columns
```




    Index([ 41695.37061,   1393336413, u'Stability',  u'Xanthium',  419.0879284,
            4.707806238, -10.62752774],
          dtype='object')



Sometime you will find that this table is invasive and you would prefer to have a shorter version of it. Pandas has a serie of options that you could use to customize what is displayed:

    - max_rows
    - max_columns
    - width 
    - precision
    - ....

I always think that 10 rows are enough for the global view.


```python
pd.options.display.max_rows = 10
```

Let's try again!


```python
CO2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 7 columns</p>
</div>



You now have a smaller view of you table and you start playing with your data. 

We imported multiple csv files, let's look what they are. But first you need to remember the name of the variables you created. To do so, the functions whos and who are very useful:

    - "who" give you a list of active variables
    - "whos" gives you details on the variables


```python
who
```

    CO2	 CO2_xls	 Data_CO2	 FileCO2	 O2	 Path_CO2	 Path_CO2_xls	 Path_H2O	 Path_O2	 
    Path_RaspPi	 RaspPi	 Water	 df	 mpl	 np	 os	 path_CO2	 pd	 
    plt	 



```python
whos
```

    Variable       Type         Data/Info
    -------------------------------------
    CO2            DataFrame              gmtime  EPOCH_T<...>n\n[891 rows x 7 columns]
    CO2_xls        DataFrame               gmtime    EPOC<...>n\n[891 rows x 7 columns]
    Data_CO2       DataFrame                             <...>[52237 rows x 30 columns]
    FileCO2        str          CFFDS2010-20150628-203257Z-DataLog_User.dat
    O2             DataFrame              gmtime  EPOCH_T<...>n\n[891 rows x 6 columns]
    Path_CO2       str          /Users/paulgauthier/Docum<...>/PUPC/Princetonpy/CO2.csv
    Path_CO2_xls   str          /Users/paulgauthier/Docum<...>PUPC/Princetonpy/CO2.xlsx
    Path_H2O       str          /Users/paulgauthier/Docum<...>/PUPC/Princetonpy/H2O.csv
    Path_O2        str          /Users/paulgauthier/Docum<...>c/PUPC/Princetonpy/O2.csv
    Path_RaspPi    str          /Users/paulgauthier/Docum<...>PC/Princetonpy/RaspPi.csv
    RaspPi         DataFrame              gmtime  EPOCH_T<...>n\n[891 rows x 7 columns]
    Water          DataFrame              gmtime  EPOCH_T<...>n\n[891 rows x 7 columns]
    df             DataFrame                             <...>\n[965 rows x 30 columns]
    mpl            module       <module 'matplotlib' from<...>matplotlib/__init__.pyc'>
    np             module       <module 'numpy' from '/Us<...>ages/numpy/__init__.pyc'>
    os             module       <module 'os' from '/Users<...>da/lib/python2.7/os.pyc'>
    path_CO2       str          /Users/paulgauthier/Docum<...>5/Birch 21 LRC/Tree2/CO2/
    pd             module       <module 'pandas' from '/U<...>ges/pandas/__init__.pyc'>
    plt            module       <module 'matplotlib.pyplo<...>s/matplotlib/pyplot.pyc'>


You now know what are your variables, so let show them at once:


```python
CO2,O2,RaspPi,Water
```




    (          gmtime  EPOCH_TIME Conditions   Species       12CO2     13CO2  \
     0    41695.37061  1393336413  Stability  Xanthium  419.087928  4.707806   
     1    41695.37113  1393336441  Stability  Xanthium  419.097669  4.705214   
     2    41695.37164  1393336497  Stability  Xanthium  418.742995  4.707043   
     3    41695.37216  1393336553  Stability  Xanthium  418.511088  4.701826   
     4    41695.37267  1393336580  Stability  Xanthium  418.384253  4.699435   
     ..           ...         ...        ...       ...         ...       ...   
     886  41695.84775  1393377633         28  Xanthium  418.873640  4.706932   
     887  41695.84822  1393377660         28  Xanthium  418.817308  4.710468   
     888  41695.84869  1393377716         28  Xanthium  418.794454  4.707813   
     889  41695.84916  1393377743         28  Xanthium  418.925316  4.706894   
     890  41695.84963  1393377799         28  Xanthium  418.912498  4.711570   
     
          Delta_Raw  
     0   -10.627528  
     1   -10.946173  
     2   -10.010987  
     3   -10.610874  
     4   -10.708263  
     ..         ...  
     886 -10.153910  
     887  -9.312446  
     888  -9.857508  
     889 -10.585101  
     890  -9.324520  
     
     [891 rows x 7 columns],
               gmtime  EPOCH_TIME Conditions   Species    dO2/N2      d18O
     0    41695.37061  1393336413  Stability  Xanthium -0.506601 -0.067217
     1    41695.37113  1393336441  Stability  Xanthium -0.267160 -0.083961
     2    41695.37164  1393336497  Stability  Xanthium -0.228845  0.061407
     3    41695.37216  1393336553  Stability  Xanthium -0.167285  0.220573
     4    41695.37267  1393336580  Stability  Xanthium -0.127173  0.024999
     ..           ...         ...        ...       ...       ...       ...
     886  41695.84775  1393377633         28  Xanthium -0.074825  0.271343
     887  41695.84822  1393377660         28  Xanthium -0.075662  0.147222
     888  41695.84869  1393377716         28  Xanthium -0.060336  0.530910
     889  41695.84916  1393377743         28  Xanthium -0.070518  0.313668
     890  41695.84963  1393377799         28  Xanthium -0.066876  0.244234
     
     [891 rows x 6 columns],
               gmtime  EPOCH_TIME Conditions   Species  Tleaf   Tair  Flow rate
     0    41695.37061  1393336413  Stability  Xanthium  21.25  20.25       1.96
     1    41695.37113  1393336441  Stability  Xanthium  21.25  20.25       1.96
     2    41695.37164  1393336497  Stability  Xanthium  21.25  20.25       1.96
     3    41695.37216  1393336553  Stability  Xanthium  21.25  20.25       1.96
     4    41695.37267  1393336580  Stability  Xanthium  21.25  20.25       1.96
     ..           ...         ...        ...       ...    ...    ...        ...
     886  41695.84775  1393377633         28  Xanthium  19.25  18.50       2.74
     887  41695.84822  1393377660         28  Xanthium  19.50  18.50       2.48
     888  41695.84869  1393377716         28  Xanthium  19.25  18.50       2.48
     889  41695.84916  1393377743         28  Xanthium  19.25  18.75       2.49
     890  41695.84963  1393377799         28  Xanthium  19.25  18.50       2.53
     
     [891 rows x 7 columns],
               gmtime  EPOCH_TIME Conditions   Species          H2O  Delta_18_16  \
     0    41695.37061  1393336413  Stability  Xanthium    18.304179   142.932962   
     1    41695.37113  1393336441  Stability  Xanthium    17.564865   132.181044   
     2    41695.37164  1393336497  Stability  Xanthium    16.798687   121.437411   
     3    41695.37216  1393336553  Stability  Xanthium    15.970207   144.785544   
     4    41695.37267  1393336580  Stability  Xanthium    16.096752    95.504243   
     ..           ...         ...        ...       ...          ...          ...   
     886  41695.84775  1393377633         28  Xanthium  6080.841143  7874.774110   
     887  41695.84822  1393377660         28  Xanthium  6124.385549  7879.733552   
     888  41695.84869  1393377716         28  Xanthium  6146.538170  7881.091023   
     889  41695.84916  1393377743         28  Xanthium  6165.700096  7884.878053   
     890  41695.84963  1393377799         28  Xanthium  6154.869221  7884.848328   
     
           Delta_D_H  
     0     51.476888  
     1   -126.439366  
     2    -71.991218  
     3    -15.744760  
     4     30.552564  
     ..          ...  
     886  124.642147  
     887  125.940038  
     888  126.829252  
     889  127.173989  
     890  127.588930  
     
     [891 rows x 7 columns])



One can notice that the first column 'gmtime' is common to all variables. So let try to combine all these variable in one big dataframe based on 'gmtime'.

To do so, you have multiple options. First, Pandas is a very smart library that includes 3 amazing functions: merge, join and concatenate. We will just focus on "merge" for now.

merge(left,right,how='',on='',left_on='',right_on='',left_index='',right_index='',sort=True,suffixes, copy=True)

You can find details about each argument in Wes McKinney Book or http://pandas.pydata.org/pandas-docs/stable/merging.html


```python
#I will call this function by default A

A = pd.merge(CO2,O2, how='inner', on='gmtime')
```

Let's show what the dataframe looks like


```python
A
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME_x</th>
      <th>Conditions_x</th>
      <th>Species_x</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>EPOCH_TIME_y</th>
      <th>Conditions_y</th>
      <th>Species_y</th>
      <th>dO2/N2</th>
      <th>d18O</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>-0.228845</td>
      <td>0.061407</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>-0.167285</td>
      <td>0.220573</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>-0.127173</td>
      <td>0.024999</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>-0.074825</td>
      <td>0.271343</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>-0.075662</td>
      <td>0.147222</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>-0.060336</td>
      <td>0.530910</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>-0.070518</td>
      <td>0.313668</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>-0.066876</td>
      <td>0.244234</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 12 columns</p>
</div>



To avoid showing all the tabl everytime you are looking for a column title, you use the attribute columns:


```python
A.columns
```




    Index([u'gmtime', u'EPOCH_TIME_x', u'Conditions_x', u'Species_x', u'12CO2',
           u'13CO2', u'Delta_Raw', u'EPOCH_TIME_y', u'Conditions_y', u'Species_y',
           u'dO2/N2', u'd18O'],
          dtype='object')



You can now remove the extra columns you don't need, using .drop()


```python
A.drop(['EPOCH_TIME_y'],axis=1,inplace=True)
A.drop(['Conditions_y'],axis=1,inplace=True)
A.drop(['Species_y'],axis=1,inplace=True)
```


```python
A
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME_x</th>
      <th>Conditions_x</th>
      <th>Species_x</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 9 columns</p>
</div>




```python
B = pd.merge(A,Water,how='inner', on='gmtime')
```


```python
B
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME_x</th>
      <th>Conditions_x</th>
      <th>Species_x</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>18.304179</td>
      <td>142.932962</td>
      <td>51.476888</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>17.564865</td>
      <td>132.181044</td>
      <td>-126.439366</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>16.798687</td>
      <td>121.437411</td>
      <td>-71.991218</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>15.970207</td>
      <td>144.785544</td>
      <td>-15.744760</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>16.096752</td>
      <td>95.504243</td>
      <td>30.552564</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>6080.841143</td>
      <td>7874.774110</td>
      <td>124.642147</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>6124.385549</td>
      <td>7879.733552</td>
      <td>125.940038</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>6146.538170</td>
      <td>7881.091023</td>
      <td>126.829252</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>6165.700096</td>
      <td>7884.878053</td>
      <td>127.173989</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>6154.869221</td>
      <td>7884.848328</td>
      <td>127.588930</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 15 columns</p>
</div>




```python
data = pd.merge(B,RaspPi,how='inner', on='gmtime')
```


```python
data
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME_x</th>
      <th>Conditions_x</th>
      <th>Species_x</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>EPOCH_TIME_x</th>
      <th>...</th>
      <th>Species_x</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
      <th>EPOCH_TIME_y</th>
      <th>Conditions_y</th>
      <th>Species_y</th>
      <th>Tleaf</th>
      <th>Tair</th>
      <th>Flow rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
      <td>1393336413</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>18.304179</td>
      <td>142.932962</td>
      <td>51.476888</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
      <td>1393336441</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>17.564865</td>
      <td>132.181044</td>
      <td>-126.439366</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
      <td>1393336497</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>16.798687</td>
      <td>121.437411</td>
      <td>-71.991218</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
      <td>1393336553</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>15.970207</td>
      <td>144.785544</td>
      <td>-15.744760</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
      <td>1393336580</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>16.096752</td>
      <td>95.504243</td>
      <td>30.552564</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
      <td>1393377633</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>6080.841143</td>
      <td>7874.774110</td>
      <td>124.642147</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.74</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
      <td>1393377660</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>6124.385549</td>
      <td>7879.733552</td>
      <td>125.940038</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>19.50</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
      <td>1393377716</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>6146.538170</td>
      <td>7881.091023</td>
      <td>126.829252</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
      <td>1393377743</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>6165.700096</td>
      <td>7884.878053</td>
      <td>127.173989</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>19.25</td>
      <td>18.75</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
      <td>1393377799</td>
      <td>...</td>
      <td>Xanthium</td>
      <td>6154.869221</td>
      <td>7884.848328</td>
      <td>127.588930</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.53</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 21 columns</p>
</div>




```python
data.columns
```




    Index([u'gmtime', u'EPOCH_TIME_x', u'Conditions_x', u'Species_x', u'12CO2',
           u'13CO2', u'Delta_Raw', u'dO2/N2', u'd18O', u'EPOCH_TIME_x',
           u'Conditions_x', u'Species_x', u'H2O', u'Delta_18_16', u'Delta_D_H',
           u'EPOCH_TIME_y', u'Conditions_y', u'Species_y', u'Tleaf', u'Tair',
           u'Flow rate'],
          dtype='object')



But Pandas is very smart and is able to figure out how to merge you data if your data contain similar columns. Here EPOCH_TIME,Conditions, Species and gmtime


```python
A1 = pd.merge(CO2,O2)
```


```python
A1
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 9 columns</p>
</div>




```python
B1 = pd.merge(A1,Water)
```


```python
B1
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
      <td>18.304179</td>
      <td>142.932962</td>
      <td>51.476888</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
      <td>17.564865</td>
      <td>132.181044</td>
      <td>-126.439366</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
      <td>16.798687</td>
      <td>121.437411</td>
      <td>-71.991218</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
      <td>15.970207</td>
      <td>144.785544</td>
      <td>-15.744760</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
      <td>16.096752</td>
      <td>95.504243</td>
      <td>30.552564</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
      <td>6080.841143</td>
      <td>7874.774110</td>
      <td>124.642147</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
      <td>6124.385549</td>
      <td>7879.733552</td>
      <td>125.940038</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
      <td>6146.538170</td>
      <td>7881.091023</td>
      <td>126.829252</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
      <td>6165.700096</td>
      <td>7884.878053</td>
      <td>127.173989</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
      <td>6154.869221</td>
      <td>7884.848328</td>
      <td>127.588930</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 12 columns</p>
</div>




```python
data1 = pd.merge(B1,RaspPi)
```


```python
data1
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
      <th>Tleaf</th>
      <th>Tair</th>
      <th>Flow rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
      <td>18.304179</td>
      <td>142.932962</td>
      <td>51.476888</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
      <td>17.564865</td>
      <td>132.181044</td>
      <td>-126.439366</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
      <td>16.798687</td>
      <td>121.437411</td>
      <td>-71.991218</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
      <td>15.970207</td>
      <td>144.785544</td>
      <td>-15.744760</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
      <td>16.096752</td>
      <td>95.504243</td>
      <td>30.552564</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
      <td>6080.841143</td>
      <td>7874.774110</td>
      <td>124.642147</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.74</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
      <td>6124.385549</td>
      <td>7879.733552</td>
      <td>125.940038</td>
      <td>19.50</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
      <td>6146.538170</td>
      <td>7881.091023</td>
      <td>126.829252</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
      <td>6165.700096</td>
      <td>7884.878053</td>
      <td>127.173989</td>
      <td>19.25</td>
      <td>18.75</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
      <td>6154.869221</td>
      <td>7884.848328</td>
      <td>127.588930</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.53</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 15 columns</p>
</div>



You can also write this is one line 


```python
data2 = pd.merge(pd.merge(pd.merge(CO2,O2),Water),RaspPi)
```


```python
data2
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
      <th>Tleaf</th>
      <th>Tair</th>
      <th>Flow rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41695.37061</td>
      <td>1393336413</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.087928</td>
      <td>4.707806</td>
      <td>-10.627528</td>
      <td>-0.506601</td>
      <td>-0.067217</td>
      <td>18.304179</td>
      <td>142.932962</td>
      <td>51.476888</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41695.37113</td>
      <td>1393336441</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>419.097669</td>
      <td>4.705214</td>
      <td>-10.946173</td>
      <td>-0.267160</td>
      <td>-0.083961</td>
      <td>17.564865</td>
      <td>132.181044</td>
      <td>-126.439366</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41695.37164</td>
      <td>1393336497</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.742995</td>
      <td>4.707043</td>
      <td>-10.010987</td>
      <td>-0.228845</td>
      <td>0.061407</td>
      <td>16.798687</td>
      <td>121.437411</td>
      <td>-71.991218</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41695.37216</td>
      <td>1393336553</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.511088</td>
      <td>4.701826</td>
      <td>-10.610874</td>
      <td>-0.167285</td>
      <td>0.220573</td>
      <td>15.970207</td>
      <td>144.785544</td>
      <td>-15.744760</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>4</th>
      <td>41695.37267</td>
      <td>1393336580</td>
      <td>Stability</td>
      <td>Xanthium</td>
      <td>418.384253</td>
      <td>4.699435</td>
      <td>-10.708263</td>
      <td>-0.127173</td>
      <td>0.024999</td>
      <td>16.096752</td>
      <td>95.504243</td>
      <td>30.552564</td>
      <td>21.25</td>
      <td>20.25</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
      <td>6080.841143</td>
      <td>7874.774110</td>
      <td>124.642147</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.74</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
      <td>6124.385549</td>
      <td>7879.733552</td>
      <td>125.940038</td>
      <td>19.50</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
      <td>6146.538170</td>
      <td>7881.091023</td>
      <td>126.829252</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
      <td>6165.700096</td>
      <td>7884.878053</td>
      <td>127.173989</td>
      <td>19.25</td>
      <td>18.75</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
      <td>6154.869221</td>
      <td>7884.848328</td>
      <td>127.588930</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.53</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 15 columns</p>
</div>



Following are some interesting functions in Pandas:


```python
data2.tail(10).mean()
```




    gmtime         4.169585e+04
    EPOCH_TIME     1.393378e+09
    12CO2          4.188142e+02
    13CO2          4.708682e+00
    Delta_Raw     -9.738182e+00
                       ...     
    Delta_18_16    7.874504e+03
    Delta_D_H      1.252641e+02
    Tleaf          1.940000e+01
    Tair           1.865000e+01
    Flow rate      2.548000e+00
    dtype: float64




```python
pd.options.display.max_rows=20
```


```python
data2.mean
```




    <bound method DataFrame.mean of           gmtime  EPOCH_TIME Conditions   Species       12CO2     13CO2  \
    0    41695.37061  1393336413  Stability  Xanthium  419.087928  4.707806   
    1    41695.37113  1393336441  Stability  Xanthium  419.097669  4.705214   
    2    41695.37164  1393336497  Stability  Xanthium  418.742995  4.707043   
    3    41695.37216  1393336553  Stability  Xanthium  418.511088  4.701826   
    4    41695.37267  1393336580  Stability  Xanthium  418.384253  4.699435   
    5    41695.37319  1393336636  Stability  Xanthium  418.370112  4.700013   
    6    41695.37370  1393336664  Stability  Xanthium  418.303371  4.700067   
    7    41695.37422  1393336720  Stability  Xanthium  418.300288  4.700902   
    8    41695.37473  1393336776  Stability  Xanthium  418.387038  4.701533   
    9    41695.37525  1393336803  Stability  Xanthium  418.484204  4.700034   
    ..           ...         ...        ...       ...         ...       ...   
    881  41695.84540  1393377438         28  Xanthium  418.748610  4.707859   
    882  41695.84587  1393377465         28  Xanthium  418.763545  4.708985   
    883  41695.84634  1393377521         28  Xanthium  418.803603  4.711569   
    884  41695.84681  1393377549         28  Xanthium  418.754631  4.710123   
    885  41695.84728  1393377605         28  Xanthium  418.748367  4.704608   
    886  41695.84775  1393377633         28  Xanthium  418.873640  4.706932   
    887  41695.84822  1393377660         28  Xanthium  418.817308  4.710468   
    888  41695.84869  1393377716         28  Xanthium  418.794454  4.707813   
    889  41695.84916  1393377743         28  Xanthium  418.925316  4.706894   
    890  41695.84963  1393377799         28  Xanthium  418.912498  4.711570   
    
         Delta_Raw    dO2/N2      d18O          H2O  Delta_18_16   Delta_D_H  \
    0   -10.627528 -0.506601 -0.067217    18.304179   142.932962   51.476888   
    1   -10.946173 -0.267160 -0.083961    17.564865   132.181044 -126.439366   
    2   -10.010987 -0.228845  0.061407    16.798687   121.437411  -71.991218   
    3   -10.610874 -0.167285  0.220573    15.970207   144.785544  -15.744760   
    4   -10.708263 -0.127173  0.024999    16.096752    95.504243   30.552564   
    5   -10.421035 -0.145070 -0.047130    14.920012   146.016649  -50.546914   
    6   -10.311241 -0.126203  0.043221    14.883563   115.672003  -67.739303   
    7    -9.711163 -0.101915 -0.192479    14.531847   114.784274   38.337363   
    8   -10.094058 -0.080671 -0.036712    14.106746   130.340317 -153.678399   
    9   -10.678810 -0.081789  0.046688    13.597614   132.057826 -131.404251   
    ..         ...       ...       ...          ...          ...         ...   
    881  -9.830024 -0.086602  0.110932  6222.210587  7864.184746  123.853490   
    882  -9.432420 -0.075429  0.305682  6134.037193  7866.491720  123.932564   
    883  -9.005807 -0.066257  0.386005  6092.471758  7866.891018  124.061794   
    884  -9.511522 -0.080159  0.133830  6058.206529  7869.598815  124.628978   
    885 -10.368561 -0.087229  0.240412  6069.909525  7872.552368  123.990113   
    886 -10.153910 -0.074825  0.271343  6080.841143  7874.774110  124.642147   
    887  -9.312446 -0.075662  0.147222  6124.385549  7879.733552  125.940038   
    888  -9.857508 -0.060336  0.530910  6146.538170  7881.091023  126.829252   
    889 -10.585101 -0.070518  0.313668  6165.700096  7884.878053  127.173989   
    890  -9.324520 -0.066876  0.244234  6154.869221  7884.848328  127.588930   
    
         Tleaf   Tair  Flow rate  
    0    21.25  20.25       1.96  
    1    21.25  20.25       1.96  
    2    21.25  20.25       1.96  
    3    21.25  20.25       1.96  
    4    21.25  20.25       1.96  
    5    21.25  20.25       1.96  
    6    21.25  20.25       1.96  
    7    21.25  20.25       1.96  
    8    21.25  20.25       1.96  
    9    21.25  20.25       1.96  
    ..     ...    ...        ...  
    881  19.50  18.75       2.63  
    882  19.50  18.75       2.50  
    883  19.50  18.75       2.54  
    884  19.50  18.75       2.56  
    885  19.50  18.75       2.53  
    886  19.25  18.50       2.74  
    887  19.50  18.50       2.48  
    888  19.25  18.50       2.48  
    889  19.25  18.75       2.49  
    890  19.25  18.50       2.53  
    
    [891 rows x 15 columns]>




```python
data2.std()
```




    gmtime             0.135423
    EPOCH_TIME     11700.606807
    12CO2             34.224812
    13CO2              0.378836
    Delta_Raw          1.458688
    dO2/N2             0.166391
    d18O               2.289179
    H2O             4891.261397
    Delta_18_16     2691.446749
    Delta_D_H         80.448794
    Tleaf              1.487626
    Tair               1.094692
    Flow rate          0.331625
    dtype: float64




```python
data2.max()
```




    gmtime            41695.8
    EPOCH_TIME     1393377799
    Conditions      Stability
    Species          Xanthium
    12CO2             433.435
    13CO2             4.86858
    Delta_Raw        -5.27089
    dO2/N2           0.389468
    d18O              6.63759
    H2O                 14148
    Delta_18_16       7884.88
    Delta_D_H         446.097
    Tleaf                  24
    Tair                21.25
    Flow rate            2.94
    dtype: object




```python
data2.min()
```




    gmtime            41695.4
    EPOCH_TIME     1393336413
    Conditions            107
    Species          Xanthium
    12CO2             336.086
    13CO2              3.7917
    Delta_Raw        -11.5253
    dO2/N2          -0.506601
    d18O            -0.239792
    H2O               5.35646
    Delta_18_16       32.5315
    Delta_D_H        -524.189
    Tleaf                17.5
    Tair                16.25
    Flow rate            1.15
    dtype: object



You can also obtain all of this statistical parameters by using describe()


```python
data2.describe()

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
      <th>Tleaf</th>
      <th>Tair</th>
      <th>Flow rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>8.910000e+02</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>877.000000</td>
      <td>877.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>41695.620226</td>
      <td>1.393358e+09</td>
      <td>370.602244</td>
      <td>4.174146</td>
      <td>-7.944638</td>
      <td>0.168258</td>
      <td>2.267445</td>
      <td>9612.520295</td>
      <td>4495.294564</td>
      <td>19.196335</td>
      <td>21.244388</td>
      <td>19.558923</td>
      <td>2.268911</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.135423</td>
      <td>1.170061e+04</td>
      <td>34.224812</td>
      <td>0.378836</td>
      <td>1.458688</td>
      <td>0.166391</td>
      <td>2.289179</td>
      <td>4891.261397</td>
      <td>2691.446749</td>
      <td>80.448794</td>
      <td>1.487626</td>
      <td>1.094692</td>
      <td>0.331625</td>
    </tr>
    <tr>
      <th>min</th>
      <td>41695.370610</td>
      <td>1.393336e+09</td>
      <td>336.086167</td>
      <td>3.791698</td>
      <td>-11.525282</td>
      <td>-0.506601</td>
      <td>-0.239792</td>
      <td>5.356458</td>
      <td>32.531461</td>
      <td>-524.189054</td>
      <td>17.500000</td>
      <td>16.250000</td>
      <td>1.150000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>41695.512245</td>
      <td>1.393349e+09</td>
      <td>340.530944</td>
      <td>3.841495</td>
      <td>-9.334801</td>
      <td>-0.018065</td>
      <td>0.066253</td>
      <td>6869.997186</td>
      <td>1893.826355</td>
      <td>-41.619948</td>
      <td>20.000000</td>
      <td>18.750000</td>
      <td>2.010000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>41695.626270</td>
      <td>1.393358e+09</td>
      <td>346.592190</td>
      <td>3.907594</td>
      <td>-7.427033</td>
      <td>0.242251</td>
      <td>1.202294</td>
      <td>12061.197450</td>
      <td>4989.665324</td>
      <td>27.123020</td>
      <td>21.750000</td>
      <td>19.750000</td>
      <td>2.470000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>41695.735745</td>
      <td>1.393368e+09</td>
      <td>411.696577</td>
      <td>4.630448</td>
      <td>-6.773218</td>
      <td>0.307567</td>
      <td>4.482016</td>
      <td>13335.795425</td>
      <td>7037.470504</td>
      <td>67.083729</td>
      <td>22.500000</td>
      <td>20.500000</td>
      <td>2.510000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>41695.849630</td>
      <td>1.393378e+09</td>
      <td>433.435473</td>
      <td>4.868579</td>
      <td>-5.270891</td>
      <td>0.389468</td>
      <td>6.637588</td>
      <td>14148.007620</td>
      <td>7884.878053</td>
      <td>446.097195</td>
      <td>24.000000</td>
      <td>21.250000</td>
      <td>2.940000</td>
    </tr>
  </tbody>
</table>
</div>



By incorporating it into a variable, you can call the parameter you are looking for


```python
detail = data2.describe()
detail['12CO2']['count']
```




    891.0



In the dataframe, you can also select the values selecting from a variable. 

Here, we will select all the values corresponding to the values in column Conditions which are equal to 28.


```python
data2[data2.Conditions=='28']
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gmtime</th>
      <th>EPOCH_TIME</th>
      <th>Conditions</th>
      <th>Species</th>
      <th>12CO2</th>
      <th>13CO2</th>
      <th>Delta_Raw</th>
      <th>dO2/N2</th>
      <th>d18O</th>
      <th>H2O</th>
      <th>Delta_18_16</th>
      <th>Delta_D_H</th>
      <th>Tleaf</th>
      <th>Tair</th>
      <th>Flow rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>875</th>
      <td>41695.84258</td>
      <td>1393377187</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>414.985963</td>
      <td>4.664634</td>
      <td>-9.792294</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6510.852237</td>
      <td>7850.565191</td>
      <td>122.572860</td>
      <td>19.75</td>
      <td>19.00</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>876</th>
      <td>41695.84305</td>
      <td>1393377215</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>415.663994</td>
      <td>4.671857</td>
      <td>-10.097414</td>
      <td>-0.083994</td>
      <td>0.330128</td>
      <td>6492.805438</td>
      <td>7850.081257</td>
      <td>123.150441</td>
      <td>19.75</td>
      <td>19.00</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>877</th>
      <td>41695.84352</td>
      <td>1393377271</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>417.080892</td>
      <td>4.690118</td>
      <td>-9.512900</td>
      <td>-0.081404</td>
      <td>0.226415</td>
      <td>6442.851720</td>
      <td>7854.085594</td>
      <td>122.518974</td>
      <td>19.75</td>
      <td>19.00</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>878</th>
      <td>41695.84399</td>
      <td>1393377299</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>417.648469</td>
      <td>4.693107</td>
      <td>-10.135795</td>
      <td>-0.059380</td>
      <td>0.420483</td>
      <td>6396.351571</td>
      <td>7856.723351</td>
      <td>123.371632</td>
      <td>19.25</td>
      <td>18.75</td>
      <td>2.51</td>
    </tr>
    <tr>
      <th>879</th>
      <td>41695.84446</td>
      <td>1393377355</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.365926</td>
      <td>4.703225</td>
      <td>-9.907277</td>
      <td>-0.076562</td>
      <td>0.295628</td>
      <td>6337.277628</td>
      <td>7861.333256</td>
      <td>123.803045</td>
      <td>19.25</td>
      <td>18.75</td>
      <td>2.55</td>
    </tr>
    <tr>
      <th>880</th>
      <td>41695.84493</td>
      <td>1393377383</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.511629</td>
      <td>4.706058</td>
      <td>-9.587423</td>
      <td>-0.064097</td>
      <td>0.198806</td>
      <td>6265.877193</td>
      <td>7861.981398</td>
      <td>123.575816</td>
      <td>19.50</td>
      <td>18.75</td>
      <td>2.52</td>
    </tr>
    <tr>
      <th>881</th>
      <td>41695.84540</td>
      <td>1393377438</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.748610</td>
      <td>4.707859</td>
      <td>-9.830024</td>
      <td>-0.086602</td>
      <td>0.110932</td>
      <td>6222.210587</td>
      <td>7864.184746</td>
      <td>123.853490</td>
      <td>19.50</td>
      <td>18.75</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>882</th>
      <td>41695.84587</td>
      <td>1393377465</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.763545</td>
      <td>4.708985</td>
      <td>-9.432420</td>
      <td>-0.075429</td>
      <td>0.305682</td>
      <td>6134.037193</td>
      <td>7866.491720</td>
      <td>123.932564</td>
      <td>19.50</td>
      <td>18.75</td>
      <td>2.50</td>
    </tr>
    <tr>
      <th>883</th>
      <td>41695.84634</td>
      <td>1393377521</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.803603</td>
      <td>4.711569</td>
      <td>-9.005807</td>
      <td>-0.066257</td>
      <td>0.386005</td>
      <td>6092.471758</td>
      <td>7866.891018</td>
      <td>124.061794</td>
      <td>19.50</td>
      <td>18.75</td>
      <td>2.54</td>
    </tr>
    <tr>
      <th>884</th>
      <td>41695.84681</td>
      <td>1393377549</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.754631</td>
      <td>4.710123</td>
      <td>-9.511522</td>
      <td>-0.080159</td>
      <td>0.133830</td>
      <td>6058.206529</td>
      <td>7869.598815</td>
      <td>124.628978</td>
      <td>19.50</td>
      <td>18.75</td>
      <td>2.56</td>
    </tr>
    <tr>
      <th>885</th>
      <td>41695.84728</td>
      <td>1393377605</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.748367</td>
      <td>4.704608</td>
      <td>-10.368561</td>
      <td>-0.087229</td>
      <td>0.240412</td>
      <td>6069.909525</td>
      <td>7872.552368</td>
      <td>123.990113</td>
      <td>19.50</td>
      <td>18.75</td>
      <td>2.53</td>
    </tr>
    <tr>
      <th>886</th>
      <td>41695.84775</td>
      <td>1393377633</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.873640</td>
      <td>4.706932</td>
      <td>-10.153910</td>
      <td>-0.074825</td>
      <td>0.271343</td>
      <td>6080.841143</td>
      <td>7874.774110</td>
      <td>124.642147</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.74</td>
    </tr>
    <tr>
      <th>887</th>
      <td>41695.84822</td>
      <td>1393377660</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.817308</td>
      <td>4.710468</td>
      <td>-9.312446</td>
      <td>-0.075662</td>
      <td>0.147222</td>
      <td>6124.385549</td>
      <td>7879.733552</td>
      <td>125.940038</td>
      <td>19.50</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>888</th>
      <td>41695.84869</td>
      <td>1393377716</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.794454</td>
      <td>4.707813</td>
      <td>-9.857508</td>
      <td>-0.060336</td>
      <td>0.530910</td>
      <td>6146.538170</td>
      <td>7881.091023</td>
      <td>126.829252</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>889</th>
      <td>41695.84916</td>
      <td>1393377743</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.925316</td>
      <td>4.706894</td>
      <td>-10.585101</td>
      <td>-0.070518</td>
      <td>0.313668</td>
      <td>6165.700096</td>
      <td>7884.878053</td>
      <td>127.173989</td>
      <td>19.25</td>
      <td>18.75</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>890</th>
      <td>41695.84963</td>
      <td>1393377799</td>
      <td>28</td>
      <td>Xanthium</td>
      <td>418.912498</td>
      <td>4.711570</td>
      <td>-9.324520</td>
      <td>-0.066876</td>
      <td>0.244234</td>
      <td>6154.869221</td>
      <td>7884.848328</td>
      <td>127.588930</td>
      <td>19.25</td>
      <td>18.50</td>
      <td>2.53</td>
    </tr>
  </tbody>
</table>
</div>




```python
data2['12CO2'][data2.Conditions=='28']
```




    875    414.985963
    876    415.663994
    877    417.080892
    878    417.648469
    879    418.365926
    880    418.511629
    881    418.748610
    882    418.763545
    883    418.803603
    884    418.754631
    885    418.748367
    886    418.873640
    887    418.817308
    888    418.794454
    889    418.925316
    890    418.912498
    Name: 12CO2, dtype: float64




```python
set(data2['Conditions'])
```




    {'107',
     '200',
     '28',
     '493',
     '51',
     '60',
     '90',
     '954',
     'Dark',
     'Light1',
     'REF',
     'Stability'}




```python
list(set(data2['Conditions']))
```




    ['Dark',
     '200',
     '28',
     '51',
     '954',
     '60',
     'Stability',
     'Light1',
     '90',
     'REF',
     '107',
     '493']




```python
data2.Conditions.unique()
```




    array(['Stability', 'Dark', 'Light1', '954', 'REF', '493', '200', '107',
           '90', '60', '51', '28'], dtype=object)



Finally, let's plot some values. 

Pandas has a special function plot in it.


```python
data2['12CO2'].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x109f23a50>




![png](output_77_1.png)



```python
data2[['12CO2','d18O']].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x119ae6450>




![png](output_78_1.png)



```python
import os

path_CO2='/Users/paulgauthier/Documents/Postdoc/Princeton/Experiments/Abisko/2015/Birch 21 LRC/Tree2/CO2/'
#import data from Picarro CO2 analyzer
Data_CO2=pd.DataFrame()
for FileCO2 in os.listdir(path_CO2):
    if FileCO2.endswith(".dat"):
        df=pd.read_csv('%s%s'%(path_CO2,FileCO2),delimiter='\s*',parse_dates={'time':[0, 1]}, index_col=0)
        Data_CO2=pd.concat([Data_CO2,df])
Data_CO2.index = Data_CO2.index.tz_localize('UTC').tz_convert('Europe/Stockholm')
```

    /Users/paulgauthier/anaconda/lib/python2.7/site-packages/IPython/kernel/__main__.py:8: ParserWarning: Falling back to the 'python' engine because the 'c' engine does not support regex separators; you can avoid this warning by specifying engine='python'.



```python
Data_CO2['06/28/2015 11:15:00':'06/28/2015 14:00:00'].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x10c8c4610>




![png](output_80_1.png)



```python
Data_CO2.resample('h')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FRAC_DAYS_SINCE_JAN1</th>
      <th>FRAC_HRS_SINCE_JAN1</th>
      <th>EPOCH_TIME</th>
      <th>ALARM_STATUS</th>
      <th>12CO2</th>
      <th>12CO2_dry</th>
      <th>13CO2</th>
      <th>13CO2_dry</th>
      <th>DasTemp</th>
      <th>Delta_2min</th>
      <th>...</th>
      <th>Ratio_Raw</th>
      <th>SpectrumID</th>
      <th>species</th>
      <th>CH4</th>
      <th>CH4_High_Precision</th>
      <th>peak_75</th>
      <th>ch4_splinemax_for_correct</th>
      <th>peak87_baseave_spec</th>
      <th>peak88_baseave</th>
      <th>y87_ave</th>
    </tr>
    <tr>
      <th>time</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-06-28 08:00:00+02:00</th>
      <td>178.083041</td>
      <td>4273.992989</td>
      <td>1.435475e+09</td>
      <td>0</td>
      <td>354.681079</td>
      <td>354.838393</td>
      <td>3.989251</td>
      <td>3.991018</td>
      <td>31.959196</td>
      <td>-10.472004</td>
      <td>...</td>
      <td>0.011132</td>
      <td>69.037736</td>
      <td>69.037736</td>
      <td>1.932809</td>
      <td>1.966912</td>
      <td>3.130568</td>
      <td>418.024452</td>
      <td>213.393546</td>
      <td>6.276824</td>
      <td>1.617180</td>
    </tr>
    <tr>
      <th>2015-06-28 09:00:00+02:00</th>
      <td>178.104177</td>
      <td>4274.500246</td>
      <td>1.435477e+09</td>
      <td>0</td>
      <td>354.557477</td>
      <td>354.633758</td>
      <td>3.983330</td>
      <td>3.984186</td>
      <td>35.286123</td>
      <td>-10.582588</td>
      <td>...</td>
      <td>0.011119</td>
      <td>69.289144</td>
      <td>69.289144</td>
      <td>1.945364</td>
      <td>1.962726</td>
      <td>1.519346</td>
      <td>420.734345</td>
      <td>213.319306</td>
      <td>6.266957</td>
      <td>1.619013</td>
    </tr>
    <tr>
      <th>2015-06-28 10:00:00+02:00</th>
      <td>178.145843</td>
      <td>4275.500227</td>
      <td>1.435480e+09</td>
      <td>0</td>
      <td>354.461236</td>
      <td>354.515766</td>
      <td>3.981341</td>
      <td>3.981953</td>
      <td>37.288145</td>
      <td>-10.842845</td>
      <td>...</td>
      <td>0.011117</td>
      <td>69.263679</td>
      <td>69.263679</td>
      <td>1.948390</td>
      <td>1.962604</td>
      <td>1.086621</td>
      <td>421.391102</td>
      <td>213.261500</td>
      <td>6.263678</td>
      <td>1.617159</td>
    </tr>
    <tr>
      <th>2015-06-28 11:00:00+02:00</th>
      <td>178.190993</td>
      <td>4276.583827</td>
      <td>1.435484e+09</td>
      <td>0</td>
      <td>346.773920</td>
      <td>348.533919</td>
      <td>3.897910</td>
      <td>3.917671</td>
      <td>37.456700</td>
      <td>-10.159077</td>
      <td>...</td>
      <td>0.011125</td>
      <td>69.346340</td>
      <td>69.346340</td>
      <td>1.910099</td>
      <td>1.955349</td>
      <td>35.749419</td>
      <td>413.103724</td>
      <td>208.576092</td>
      <td>6.144904</td>
      <td>1.621029</td>
    </tr>
    <tr>
      <th>2015-06-28 12:00:00+02:00</th>
      <td>178.229150</td>
      <td>4277.499606</td>
      <td>1.435487e+09</td>
      <td>0</td>
      <td>337.708018</td>
      <td>341.016531</td>
      <td>3.800406</td>
      <td>3.837573</td>
      <td>37.599081</td>
      <td>-9.043993</td>
      <td>...</td>
      <td>0.011137</td>
      <td>69.328817</td>
      <td>69.328817</td>
      <td>1.880917</td>
      <td>1.948462</td>
      <td>67.556190</td>
      <td>406.791294</td>
      <td>203.198847</td>
      <td>6.003006</td>
      <td>1.625134</td>
    </tr>
    <tr>
      <th>2015-06-28 13:00:00+02:00</th>
      <td>178.270840</td>
      <td>4278.500151</td>
      <td>1.435491e+09</td>
      <td>0</td>
      <td>340.216384</td>
      <td>342.951862</td>
      <td>3.826427</td>
      <td>3.857140</td>
      <td>38.468128</td>
      <td>-9.577167</td>
      <td>...</td>
      <td>0.011131</td>
      <td>69.309300</td>
      <td>69.309300</td>
      <td>1.895632</td>
      <td>1.950841</td>
      <td>55.696546</td>
      <td>409.976518</td>
      <td>204.705472</td>
      <td>6.039705</td>
      <td>1.623359</td>
    </tr>
    <tr>
      <th>2015-06-28 14:00:00+02:00</th>
      <td>178.312492</td>
      <td>4279.499801</td>
      <td>1.435495e+09</td>
      <td>0</td>
      <td>348.730410</td>
      <td>350.995148</td>
      <td>3.919933</td>
      <td>3.945344</td>
      <td>38.664205</td>
      <td>-10.076467</td>
      <td>...</td>
      <td>0.011125</td>
      <td>69.310264</td>
      <td>69.310264</td>
      <td>1.903498</td>
      <td>1.950314</td>
      <td>44.752500</td>
      <td>411.678182</td>
      <td>209.819336</td>
      <td>6.183075</td>
      <td>1.621877</td>
    </tr>
    <tr>
      <th>2015-06-28 15:00:00+02:00</th>
      <td>178.354156</td>
      <td>4280.499752</td>
      <td>1.435498e+09</td>
      <td>0</td>
      <td>348.291810</td>
      <td>350.145617</td>
      <td>3.915333</td>
      <td>3.936137</td>
      <td>38.514838</td>
      <td>-10.027613</td>
      <td>...</td>
      <td>0.011126</td>
      <td>69.325496</td>
      <td>69.325496</td>
      <td>1.916089</td>
      <td>1.954348</td>
      <td>37.044336</td>
      <td>414.402795</td>
      <td>209.555895</td>
      <td>6.172964</td>
      <td>1.621105</td>
    </tr>
    <tr>
      <th>2015-06-28 16:00:00+02:00</th>
      <td>178.395842</td>
      <td>4281.500203</td>
      <td>1.435502e+09</td>
      <td>0</td>
      <td>351.174042</td>
      <td>352.888734</td>
      <td>3.947709</td>
      <td>3.966951</td>
      <td>38.252418</td>
      <td>-9.993749</td>
      <td>...</td>
      <td>0.011126</td>
      <td>69.316119</td>
      <td>69.316119</td>
      <td>1.918467</td>
      <td>1.955705</td>
      <td>33.831267</td>
      <td>414.916272</td>
      <td>211.287079</td>
      <td>6.222798</td>
      <td>1.620659</td>
    </tr>
    <tr>
      <th>2015-06-28 17:00:00+02:00</th>
      <td>178.437508</td>
      <td>4282.500184</td>
      <td>1.435505e+09</td>
      <td>0</td>
      <td>350.959406</td>
      <td>352.454287</td>
      <td>3.944746</td>
      <td>3.961520</td>
      <td>38.139087</td>
      <td>-10.167798</td>
      <td>...</td>
      <td>0.011124</td>
      <td>69.297473</td>
      <td>69.297473</td>
      <td>1.922746</td>
      <td>1.956214</td>
      <td>29.777047</td>
      <td>415.842504</td>
      <td>211.158160</td>
      <td>6.216604</td>
      <td>1.619385</td>
    </tr>
    <tr>
      <th>2015-06-28 18:00:00+02:00</th>
      <td>178.479168</td>
      <td>4283.500030</td>
      <td>1.435509e+09</td>
      <td>0</td>
      <td>351.475990</td>
      <td>352.885610</td>
      <td>3.949892</td>
      <td>3.965706</td>
      <td>37.840492</td>
      <td>-10.310525</td>
      <td>...</td>
      <td>0.011123</td>
      <td>69.325351</td>
      <td>69.325351</td>
      <td>1.924654</td>
      <td>1.956527</td>
      <td>28.054607</td>
      <td>416.255748</td>
      <td>211.468441</td>
      <td>6.224074</td>
      <td>1.619080</td>
    </tr>
    <tr>
      <th>2015-06-28 19:00:00+02:00</th>
      <td>178.520828</td>
      <td>4284.499861</td>
      <td>1.435513e+09</td>
      <td>0</td>
      <td>352.729023</td>
      <td>354.104471</td>
      <td>3.964874</td>
      <td>3.980308</td>
      <td>38.681413</td>
      <td>-10.088620</td>
      <td>...</td>
      <td>0.011125</td>
      <td>69.310219</td>
      <td>69.310219</td>
      <td>1.926524</td>
      <td>1.956731</td>
      <td>27.285120</td>
      <td>416.660722</td>
      <td>212.221063</td>
      <td>6.247383</td>
      <td>1.619078</td>
    </tr>
    <tr>
      <th>2015-06-28 20:00:00+02:00</th>
      <td>178.562507</td>
      <td>4285.500158</td>
      <td>1.435516e+09</td>
      <td>0</td>
      <td>353.446400</td>
      <td>354.819738</td>
      <td>3.972754</td>
      <td>3.988165</td>
      <td>39.071983</td>
      <td>-10.153998</td>
      <td>...</td>
      <td>0.011124</td>
      <td>69.282285</td>
      <td>69.282285</td>
      <td>1.927205</td>
      <td>1.956750</td>
      <td>27.188827</td>
      <td>416.807560</td>
      <td>212.651948</td>
      <td>6.259758</td>
      <td>1.618913</td>
    </tr>
    <tr>
      <th>2015-06-28 21:00:00+02:00</th>
      <td>178.604173</td>
      <td>4286.500154</td>
      <td>1.435520e+09</td>
      <td>0</td>
      <td>355.698617</td>
      <td>357.079818</td>
      <td>3.997816</td>
      <td>4.013314</td>
      <td>39.522170</td>
      <td>-10.192231</td>
      <td>...</td>
      <td>0.011124</td>
      <td>69.353309</td>
      <td>69.353309</td>
      <td>1.926136</td>
      <td>1.956688</td>
      <td>27.171861</td>
      <td>416.576477</td>
      <td>214.004720</td>
      <td>6.299205</td>
      <td>1.619345</td>
    </tr>
    <tr>
      <th>2015-06-28 22:00:00+02:00</th>
      <td>178.641658</td>
      <td>4287.399790</td>
      <td>1.435523e+09</td>
      <td>0</td>
      <td>365.920879</td>
      <td>367.039892</td>
      <td>4.109502</td>
      <td>4.122042</td>
      <td>39.784774</td>
      <td>-10.770319</td>
      <td>...</td>
      <td>0.011117</td>
      <td>69.288787</td>
      <td>69.288787</td>
      <td>1.930821</td>
      <td>1.955034</td>
      <td>20.357914</td>
      <td>417.591087</td>
      <td>220.144619</td>
      <td>6.472683</td>
      <td>1.618369</td>
    </tr>
  </tbody>
</table>
<p>15 rows × 30 columns</p>
</div>




```python
Data_CO2.resample('h').plot(subplots=True)
```

    /Users/paulgauthier/anaconda/lib/python2.7/site-packages/IPython/kernel/__main__.py:1: FutureWarning: .resample() is now a deferred operation
    use .resample(...).mean() instead of .resample(...)
      if __name__ == '__main__':





    array([<matplotlib.axes._subplots.AxesSubplot object at 0x10dc52f90>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111089a10>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111107e10>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x11118aa50>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x11120aa10>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1111ac650>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1112fc690>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1113813d0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1113e3a50>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111467890>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1114cd690>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x11154f4d0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1115d3210>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1116402d0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1116b6fd0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111835e90>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1118b8cd0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x11185a850>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1119aaad0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111a2e810>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111a92e90>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111b15cd0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111b6ead0>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x111bfd910>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x11343f650>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1134b0710>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x113534450>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x113579450>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x1135fd190>,
           <matplotlib.axes._subplots.AxesSubplot object at 0x11362a650>], dtype=object)




![png](output_82_2.png)



```python
Data_CO2.resample('h',how='mean')
```

    /Users/paulgauthier/anaconda/lib/python2.7/site-packages/IPython/kernel/__main__.py:1: FutureWarning: how in .resample() is deprecated
    the new syntax is .resample(...).mean()
      if __name__ == '__main__':





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FRAC_DAYS_SINCE_JAN1</th>
      <th>FRAC_HRS_SINCE_JAN1</th>
      <th>EPOCH_TIME</th>
      <th>ALARM_STATUS</th>
      <th>12CO2</th>
      <th>12CO2_dry</th>
      <th>13CO2</th>
      <th>13CO2_dry</th>
      <th>DasTemp</th>
      <th>Delta_2min</th>
      <th>...</th>
      <th>Ratio_Raw</th>
      <th>SpectrumID</th>
      <th>species</th>
      <th>CH4</th>
      <th>CH4_High_Precision</th>
      <th>peak_75</th>
      <th>ch4_splinemax_for_correct</th>
      <th>peak87_baseave_spec</th>
      <th>peak88_baseave</th>
      <th>y87_ave</th>
    </tr>
    <tr>
      <th>time</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-06-28 08:00:00+02:00</th>
      <td>178.083041</td>
      <td>4273.992989</td>
      <td>1.435475e+09</td>
      <td>0</td>
      <td>354.681079</td>
      <td>354.838393</td>
      <td>3.989251</td>
      <td>3.991018</td>
      <td>31.959196</td>
      <td>-10.472004</td>
      <td>...</td>
      <td>0.011132</td>
      <td>69.037736</td>
      <td>69.037736</td>
      <td>1.932809</td>
      <td>1.966912</td>
      <td>3.130568</td>
      <td>418.024452</td>
      <td>213.393546</td>
      <td>6.276824</td>
      <td>1.617180</td>
    </tr>
    <tr>
      <th>2015-06-28 09:00:00+02:00</th>
      <td>178.104177</td>
      <td>4274.500246</td>
      <td>1.435477e+09</td>
      <td>0</td>
      <td>354.557477</td>
      <td>354.633758</td>
      <td>3.983330</td>
      <td>3.984186</td>
      <td>35.286123</td>
      <td>-10.582588</td>
      <td>...</td>
      <td>0.011119</td>
      <td>69.289144</td>
      <td>69.289144</td>
      <td>1.945364</td>
      <td>1.962726</td>
      <td>1.519346</td>
      <td>420.734345</td>
      <td>213.319306</td>
      <td>6.266957</td>
      <td>1.619013</td>
    </tr>
    <tr>
      <th>2015-06-28 10:00:00+02:00</th>
      <td>178.145843</td>
      <td>4275.500227</td>
      <td>1.435480e+09</td>
      <td>0</td>
      <td>354.461236</td>
      <td>354.515766</td>
      <td>3.981341</td>
      <td>3.981953</td>
      <td>37.288145</td>
      <td>-10.842845</td>
      <td>...</td>
      <td>0.011117</td>
      <td>69.263679</td>
      <td>69.263679</td>
      <td>1.948390</td>
      <td>1.962604</td>
      <td>1.086621</td>
      <td>421.391102</td>
      <td>213.261500</td>
      <td>6.263678</td>
      <td>1.617159</td>
    </tr>
    <tr>
      <th>2015-06-28 11:00:00+02:00</th>
      <td>178.190993</td>
      <td>4276.583827</td>
      <td>1.435484e+09</td>
      <td>0</td>
      <td>346.773920</td>
      <td>348.533919</td>
      <td>3.897910</td>
      <td>3.917671</td>
      <td>37.456700</td>
      <td>-10.159077</td>
      <td>...</td>
      <td>0.011125</td>
      <td>69.346340</td>
      <td>69.346340</td>
      <td>1.910099</td>
      <td>1.955349</td>
      <td>35.749419</td>
      <td>413.103724</td>
      <td>208.576092</td>
      <td>6.144904</td>
      <td>1.621029</td>
    </tr>
    <tr>
      <th>2015-06-28 12:00:00+02:00</th>
      <td>178.229150</td>
      <td>4277.499606</td>
      <td>1.435487e+09</td>
      <td>0</td>
      <td>337.708018</td>
      <td>341.016531</td>
      <td>3.800406</td>
      <td>3.837573</td>
      <td>37.599081</td>
      <td>-9.043993</td>
      <td>...</td>
      <td>0.011137</td>
      <td>69.328817</td>
      <td>69.328817</td>
      <td>1.880917</td>
      <td>1.948462</td>
      <td>67.556190</td>
      <td>406.791294</td>
      <td>203.198847</td>
      <td>6.003006</td>
      <td>1.625134</td>
    </tr>
    <tr>
      <th>2015-06-28 13:00:00+02:00</th>
      <td>178.270840</td>
      <td>4278.500151</td>
      <td>1.435491e+09</td>
      <td>0</td>
      <td>340.216384</td>
      <td>342.951862</td>
      <td>3.826427</td>
      <td>3.857140</td>
      <td>38.468128</td>
      <td>-9.577167</td>
      <td>...</td>
      <td>0.011131</td>
      <td>69.309300</td>
      <td>69.309300</td>
      <td>1.895632</td>
      <td>1.950841</td>
      <td>55.696546</td>
      <td>409.976518</td>
      <td>204.705472</td>
      <td>6.039705</td>
      <td>1.623359</td>
    </tr>
    <tr>
      <th>2015-06-28 14:00:00+02:00</th>
      <td>178.312492</td>
      <td>4279.499801</td>
      <td>1.435495e+09</td>
      <td>0</td>
      <td>348.730410</td>
      <td>350.995148</td>
      <td>3.919933</td>
      <td>3.945344</td>
      <td>38.664205</td>
      <td>-10.076467</td>
      <td>...</td>
      <td>0.011125</td>
      <td>69.310264</td>
      <td>69.310264</td>
      <td>1.903498</td>
      <td>1.950314</td>
      <td>44.752500</td>
      <td>411.678182</td>
      <td>209.819336</td>
      <td>6.183075</td>
      <td>1.621877</td>
    </tr>
    <tr>
      <th>2015-06-28 15:00:00+02:00</th>
      <td>178.354156</td>
      <td>4280.499752</td>
      <td>1.435498e+09</td>
      <td>0</td>
      <td>348.291810</td>
      <td>350.145617</td>
      <td>3.915333</td>
      <td>3.936137</td>
      <td>38.514838</td>
      <td>-10.027613</td>
      <td>...</td>
      <td>0.011126</td>
      <td>69.325496</td>
      <td>69.325496</td>
      <td>1.916089</td>
      <td>1.954348</td>
      <td>37.044336</td>
      <td>414.402795</td>
      <td>209.555895</td>
      <td>6.172964</td>
      <td>1.621105</td>
    </tr>
    <tr>
      <th>2015-06-28 16:00:00+02:00</th>
      <td>178.395842</td>
      <td>4281.500203</td>
      <td>1.435502e+09</td>
      <td>0</td>
      <td>351.174042</td>
      <td>352.888734</td>
      <td>3.947709</td>
      <td>3.966951</td>
      <td>38.252418</td>
      <td>-9.993749</td>
      <td>...</td>
      <td>0.011126</td>
      <td>69.316119</td>
      <td>69.316119</td>
      <td>1.918467</td>
      <td>1.955705</td>
      <td>33.831267</td>
      <td>414.916272</td>
      <td>211.287079</td>
      <td>6.222798</td>
      <td>1.620659</td>
    </tr>
    <tr>
      <th>2015-06-28 17:00:00+02:00</th>
      <td>178.437508</td>
      <td>4282.500184</td>
      <td>1.435505e+09</td>
      <td>0</td>
      <td>350.959406</td>
      <td>352.454287</td>
      <td>3.944746</td>
      <td>3.961520</td>
      <td>38.139087</td>
      <td>-10.167798</td>
      <td>...</td>
      <td>0.011124</td>
      <td>69.297473</td>
      <td>69.297473</td>
      <td>1.922746</td>
      <td>1.956214</td>
      <td>29.777047</td>
      <td>415.842504</td>
      <td>211.158160</td>
      <td>6.216604</td>
      <td>1.619385</td>
    </tr>
    <tr>
      <th>2015-06-28 18:00:00+02:00</th>
      <td>178.479168</td>
      <td>4283.500030</td>
      <td>1.435509e+09</td>
      <td>0</td>
      <td>351.475990</td>
      <td>352.885610</td>
      <td>3.949892</td>
      <td>3.965706</td>
      <td>37.840492</td>
      <td>-10.310525</td>
      <td>...</td>
      <td>0.011123</td>
      <td>69.325351</td>
      <td>69.325351</td>
      <td>1.924654</td>
      <td>1.956527</td>
      <td>28.054607</td>
      <td>416.255748</td>
      <td>211.468441</td>
      <td>6.224074</td>
      <td>1.619080</td>
    </tr>
    <tr>
      <th>2015-06-28 19:00:00+02:00</th>
      <td>178.520828</td>
      <td>4284.499861</td>
      <td>1.435513e+09</td>
      <td>0</td>
      <td>352.729023</td>
      <td>354.104471</td>
      <td>3.964874</td>
      <td>3.980308</td>
      <td>38.681413</td>
      <td>-10.088620</td>
      <td>...</td>
      <td>0.011125</td>
      <td>69.310219</td>
      <td>69.310219</td>
      <td>1.926524</td>
      <td>1.956731</td>
      <td>27.285120</td>
      <td>416.660722</td>
      <td>212.221063</td>
      <td>6.247383</td>
      <td>1.619078</td>
    </tr>
    <tr>
      <th>2015-06-28 20:00:00+02:00</th>
      <td>178.562507</td>
      <td>4285.500158</td>
      <td>1.435516e+09</td>
      <td>0</td>
      <td>353.446400</td>
      <td>354.819738</td>
      <td>3.972754</td>
      <td>3.988165</td>
      <td>39.071983</td>
      <td>-10.153998</td>
      <td>...</td>
      <td>0.011124</td>
      <td>69.282285</td>
      <td>69.282285</td>
      <td>1.927205</td>
      <td>1.956750</td>
      <td>27.188827</td>
      <td>416.807560</td>
      <td>212.651948</td>
      <td>6.259758</td>
      <td>1.618913</td>
    </tr>
    <tr>
      <th>2015-06-28 21:00:00+02:00</th>
      <td>178.604173</td>
      <td>4286.500154</td>
      <td>1.435520e+09</td>
      <td>0</td>
      <td>355.698617</td>
      <td>357.079818</td>
      <td>3.997816</td>
      <td>4.013314</td>
      <td>39.522170</td>
      <td>-10.192231</td>
      <td>...</td>
      <td>0.011124</td>
      <td>69.353309</td>
      <td>69.353309</td>
      <td>1.926136</td>
      <td>1.956688</td>
      <td>27.171861</td>
      <td>416.576477</td>
      <td>214.004720</td>
      <td>6.299205</td>
      <td>1.619345</td>
    </tr>
    <tr>
      <th>2015-06-28 22:00:00+02:00</th>
      <td>178.641658</td>
      <td>4287.399790</td>
      <td>1.435523e+09</td>
      <td>0</td>
      <td>365.920879</td>
      <td>367.039892</td>
      <td>4.109502</td>
      <td>4.122042</td>
      <td>39.784774</td>
      <td>-10.770319</td>
      <td>...</td>
      <td>0.011117</td>
      <td>69.288787</td>
      <td>69.288787</td>
      <td>1.930821</td>
      <td>1.955034</td>
      <td>20.357914</td>
      <td>417.591087</td>
      <td>220.144619</td>
      <td>6.472683</td>
      <td>1.618369</td>
    </tr>
  </tbody>
</table>
<p>15 rows × 30 columns</p>
</div>




```python
Data_CO2.resample('h',how='mean')['12CO2'].plot(subplots=True)
```

    /Users/paulgauthier/anaconda/lib/python2.7/site-packages/IPython/kernel/__main__.py:1: FutureWarning: how in .resample() is deprecated
    the new syntax is .resample(...).mean()
      if __name__ == '__main__':





    array([<matplotlib.axes._subplots.AxesSubplot object at 0x10caa8e90>], dtype=object)




![png](output_84_2.png)



```python

```
