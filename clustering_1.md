
### This notenook will be used for the final Data Science Capstone Project!


```python
import pandas as pd
import numpy as np

print("Hello Capstone Project Course!")
```

    Hello Capstone Project Course!


### Create Initial dataframe from Wikipedia


```python
import requests
import pandas as pd

#Get data from WiKi
URL ='https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M'
d = pd.read_html(URL)
df = d[0]
df.head()
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
      <th>Postcode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1A</td>
      <td>Not assigned</td>
      <td>Not assigned</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M2A</td>
      <td>Not assigned</td>
      <td>Not assigned</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront</td>
    </tr>
  </tbody>
</table>
</div>



### Filter out not assigned bourough and combine Neighbourhoods


```python
#Filter where not like 'Not assigned'
df = df[df.Borough != 'Not assigned']
# Group by postcode and borough and combine neighbourhoods
test = df.groupby(['Postcode','Borough'])['Neighbourhood'].apply(lambda neighbour: ','.join(neighbour))
df = test.to_frame().reset_index()
df.head()

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
      <th>Postcode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Rouge,Malvern</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Highland Creek,Rouge Hill,Port Union</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>Scarborough</td>
      <td>Guildwood,Morningside,West Hill</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>Scarborough</td>
      <td>Woburn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
    </tr>
  </tbody>
</table>
</div>



### Fix not assigned Neighbourhoods


```python
df.loc[df.Neighbourhood == 'Not assigned', 'Neighbourhood'] = df.Borough

```


```python
df.head(100)
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
      <th>Postcode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Rouge,Malvern</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Highland Creek,Rouge Hill,Port Union</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>Scarborough</td>
      <td>Guildwood,Morningside,West Hill</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>Scarborough</td>
      <td>Woburn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M1J</td>
      <td>Scarborough</td>
      <td>Scarborough Village</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M1K</td>
      <td>Scarborough</td>
      <td>East Birchmount Park,Ionview,Kennedy Park</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M1L</td>
      <td>Scarborough</td>
      <td>Clairlea,Golden Mile,Oakridge</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M1M</td>
      <td>Scarborough</td>
      <td>Cliffcrest,Cliffside,Scarborough Village West</td>
    </tr>
    <tr>
      <th>9</th>
      <td>M1N</td>
      <td>Scarborough</td>
      <td>Birch Cliff,Cliffside West</td>
    </tr>
    <tr>
      <th>10</th>
      <td>M1P</td>
      <td>Scarborough</td>
      <td>Dorset Park,Scarborough Town Centre,Wexford He...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>M1R</td>
      <td>Scarborough</td>
      <td>Maryvale,Wexford</td>
    </tr>
    <tr>
      <th>12</th>
      <td>M1S</td>
      <td>Scarborough</td>
      <td>Agincourt</td>
    </tr>
    <tr>
      <th>13</th>
      <td>M1T</td>
      <td>Scarborough</td>
      <td>Clarks Corners,Sullivan,Tam O'Shanter</td>
    </tr>
    <tr>
      <th>14</th>
      <td>M1V</td>
      <td>Scarborough</td>
      <td>Agincourt North,L'Amoreaux East,Milliken,Steel...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>M1W</td>
      <td>Scarborough</td>
      <td>L'Amoreaux West</td>
    </tr>
    <tr>
      <th>16</th>
      <td>M1X</td>
      <td>Scarborough</td>
      <td>Upper Rouge</td>
    </tr>
    <tr>
      <th>17</th>
      <td>M2H</td>
      <td>North York</td>
      <td>Hillcrest Village</td>
    </tr>
    <tr>
      <th>18</th>
      <td>M2J</td>
      <td>North York</td>
      <td>Fairview,Henry Farm,Oriole</td>
    </tr>
    <tr>
      <th>19</th>
      <td>M2K</td>
      <td>North York</td>
      <td>Bayview Village</td>
    </tr>
    <tr>
      <th>20</th>
      <td>M2L</td>
      <td>North York</td>
      <td>Silver Hills,York Mills</td>
    </tr>
    <tr>
      <th>21</th>
      <td>M2M</td>
      <td>North York</td>
      <td>Newtonbrook,Willowdale</td>
    </tr>
    <tr>
      <th>22</th>
      <td>M2N</td>
      <td>North York</td>
      <td>Willowdale South</td>
    </tr>
    <tr>
      <th>23</th>
      <td>M2P</td>
      <td>North York</td>
      <td>York Mills West</td>
    </tr>
    <tr>
      <th>24</th>
      <td>M2R</td>
      <td>North York</td>
      <td>Willowdale West</td>
    </tr>
    <tr>
      <th>25</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>26</th>
      <td>M3B</td>
      <td>North York</td>
      <td>Don Mills North</td>
    </tr>
    <tr>
      <th>27</th>
      <td>M3C</td>
      <td>North York</td>
      <td>Flemingdon Park,Don Mills South</td>
    </tr>
    <tr>
      <th>28</th>
      <td>M3H</td>
      <td>North York</td>
      <td>Bathurst Manor,Downsview North,Wilson Heights</td>
    </tr>
    <tr>
      <th>29</th>
      <td>M3J</td>
      <td>North York</td>
      <td>Northwood Park,York University</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>M5X</td>
      <td>Downtown Toronto</td>
      <td>First Canadian Place,Underground city</td>
    </tr>
    <tr>
      <th>71</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Heights,Lawrence Manor</td>
    </tr>
    <tr>
      <th>72</th>
      <td>M6B</td>
      <td>North York</td>
      <td>Glencairn</td>
    </tr>
    <tr>
      <th>73</th>
      <td>M6C</td>
      <td>York</td>
      <td>Humewood-Cedarvale</td>
    </tr>
    <tr>
      <th>74</th>
      <td>M6E</td>
      <td>York</td>
      <td>Caledonia-Fairbanks</td>
    </tr>
    <tr>
      <th>75</th>
      <td>M6G</td>
      <td>Downtown Toronto</td>
      <td>Christie</td>
    </tr>
    <tr>
      <th>76</th>
      <td>M6H</td>
      <td>West Toronto</td>
      <td>Dovercourt Village,Dufferin</td>
    </tr>
    <tr>
      <th>77</th>
      <td>M6J</td>
      <td>West Toronto</td>
      <td>Little Portugal,Trinity</td>
    </tr>
    <tr>
      <th>78</th>
      <td>M6K</td>
      <td>West Toronto</td>
      <td>Brockton,Exhibition Place,Parkdale Village</td>
    </tr>
    <tr>
      <th>79</th>
      <td>M6L</td>
      <td>North York</td>
      <td>Downsview,North Park,Upwood Park</td>
    </tr>
    <tr>
      <th>80</th>
      <td>M6M</td>
      <td>York</td>
      <td>Del Ray,Keelesdale,Mount Dennis,Silverthorn</td>
    </tr>
    <tr>
      <th>81</th>
      <td>M6N</td>
      <td>York</td>
      <td>The Junction North,Runnymede</td>
    </tr>
    <tr>
      <th>82</th>
      <td>M6P</td>
      <td>West Toronto</td>
      <td>High Park,The Junction South</td>
    </tr>
    <tr>
      <th>83</th>
      <td>M6R</td>
      <td>West Toronto</td>
      <td>Parkdale,Roncesvalles</td>
    </tr>
    <tr>
      <th>84</th>
      <td>M6S</td>
      <td>West Toronto</td>
      <td>Runnymede,Swansea</td>
    </tr>
    <tr>
      <th>85</th>
      <td>M7A</td>
      <td>Queen's Park</td>
      <td>Queen's Park</td>
    </tr>
    <tr>
      <th>86</th>
      <td>M7R</td>
      <td>Mississauga</td>
      <td>Canada Post Gateway Processing Centre</td>
    </tr>
    <tr>
      <th>87</th>
      <td>M7Y</td>
      <td>East Toronto</td>
      <td>Business Reply Mail Processing Centre 969 Eastern</td>
    </tr>
    <tr>
      <th>88</th>
      <td>M8V</td>
      <td>Etobicoke</td>
      <td>Humber Bay Shores,Mimico South,New Toronto</td>
    </tr>
    <tr>
      <th>89</th>
      <td>M8W</td>
      <td>Etobicoke</td>
      <td>Alderwood,Long Branch</td>
    </tr>
    <tr>
      <th>90</th>
      <td>M8X</td>
      <td>Etobicoke</td>
      <td>The Kingsway,Montgomery Road,Old Mill North</td>
    </tr>
    <tr>
      <th>91</th>
      <td>M8Y</td>
      <td>Etobicoke</td>
      <td>Humber Bay,King's Mill Park,Kingsway Park Sout...</td>
    </tr>
    <tr>
      <th>92</th>
      <td>M8Z</td>
      <td>Etobicoke</td>
      <td>Kingsway Park South West,Mimico NW,The Queensw...</td>
    </tr>
    <tr>
      <th>93</th>
      <td>M9A</td>
      <td>Etobicoke</td>
      <td>Islington Avenue</td>
    </tr>
    <tr>
      <th>94</th>
      <td>M9B</td>
      <td>Etobicoke</td>
      <td>Cloverdale,Islington,Martin Grove,Princess Gar...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>M9C</td>
      <td>Etobicoke</td>
      <td>Bloordale Gardens,Eringate,Markland Wood,Old B...</td>
    </tr>
    <tr>
      <th>96</th>
      <td>M9L</td>
      <td>North York</td>
      <td>Humber Summit</td>
    </tr>
    <tr>
      <th>97</th>
      <td>M9M</td>
      <td>North York</td>
      <td>Emery,Humberlea</td>
    </tr>
    <tr>
      <th>98</th>
      <td>M9N</td>
      <td>York</td>
      <td>Weston</td>
    </tr>
    <tr>
      <th>99</th>
      <td>M9P</td>
      <td>Etobicoke</td>
      <td>Westmount</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 3 columns</p>
</div>




```python
df.shape
```




    (103, 3)




```python

```
