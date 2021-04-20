```python
import numpy as np
import pandas as pd
```


```python
pets = pd.DataFrame({'sex': np.array(['M', 'M', 'F', 'M', 'F', 'F', 'F', 'M', 'F', 'M']),
                   'age': np.array([21, 45, 23, 56, 47, 70, 34, 30, 19, 62]),
                   'pets': np.array([['cat', 'dog'],
                                    ['hamster'],
                                    ['cat', 'gerbil'],
                                    ['fish', 'hamster', 'gerbil'],
                                    ['cat'],
                                    ['dog'],
                                    ['dog'],
                                    ['cat'],
                                    ['rabbit', 'cat'],
                                    ['dog']])})
```

    <ipython-input-3-697f91f7354f>:3: VisibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray
      'pets': np.array([['cat', 'dog'],



```python
pets
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sex</th>
      <th>age</th>
      <th>pets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M</td>
      <td>21</td>
      <td>[cat, dog]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>45</td>
      <td>[hamster]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>F</td>
      <td>23</td>
      <td>[cat, gerbil]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M</td>
      <td>56</td>
      <td>[fish, hamster, gerbil]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>F</td>
      <td>47</td>
      <td>[cat]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>F</td>
      <td>70</td>
      <td>[dog]</td>
    </tr>
    <tr>
      <th>6</th>
      <td>F</td>
      <td>34</td>
      <td>[dog]</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M</td>
      <td>30</td>
      <td>[cat]</td>
    </tr>
    <tr>
      <th>8</th>
      <td>F</td>
      <td>19</td>
      <td>[rabbit, cat]</td>
    </tr>
    <tr>
      <th>9</th>
      <td>M</td>
      <td>62</td>
      <td>[dog]</td>
    </tr>
  </tbody>
</table>
</div>




```python
pets.loc[pets['age'] == min(pets['age']), 'sex']
```




    8    F
    Name: sex, dtype: object




```python
# task: create new column 'num_pets' which contains the number of pets
# each person had (hint: this is the length of each list in the pets column)
# one line of code here:
pets['num_pets'] = pets['pets'].apply(lambda x: len(x))
```


```python
pets
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sex</th>
      <th>age</th>
      <th>pets</th>
      <th>num_pets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M</td>
      <td>21</td>
      <td>[cat, dog]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>45</td>
      <td>[hamster]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>F</td>
      <td>23</td>
      <td>[cat, gerbil]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M</td>
      <td>56</td>
      <td>[fish, hamster, gerbil]</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>F</td>
      <td>47</td>
      <td>[cat]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>F</td>
      <td>70</td>
      <td>[dog]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>F</td>
      <td>34</td>
      <td>[dog]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M</td>
      <td>30</td>
      <td>[cat]</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>F</td>
      <td>19</td>
      <td>[rabbit, cat]</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>M</td>
      <td>62</td>
      <td>[dog]</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
pet_series = pets['pets'].apply(pd.Series).stack().reset_index(drop=True)
pet_series
```




    0         cat
    1         dog
    2     hamster
    3         cat
    4      gerbil
    5        fish
    6     hamster
    7      gerbil
    8         cat
    9         dog
    10        dog
    11        cat
    12     rabbit
    13        cat
    14        dog
    dtype: object




```python
# task: produce an ordered count of each animal
# one line of code here:
pet_series.value_counts()
```




    cat        5
    dog        4
    hamster    2
    gerbil     2
    fish       1
    rabbit     1
    dtype: int64




```python
pets.loc[pets['pets'].apply(lambda x: 'dog' in x), 'age'].mean()
```




    46.75




```python

```
