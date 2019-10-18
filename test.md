
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



### Join on postal code


```python
geo = pd.read_csv('Geospatial_Coordinates.csv')
geo_df = pd.merge(df,geo, on=[df.Postcode, geo["Postal Code"]])
geo_df.drop(['key_0','key_1','Postcode'], axis=1,inplace=True)
```


```python
geo_df.head()
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
      <th>Borough</th>
      <th>Neighbourhood</th>
      <th>Postal Code</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Scarborough</td>
      <td>Rouge,Malvern</td>
      <td>M1B</td>
      <td>43.806686</td>
      <td>-79.194353</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Scarborough</td>
      <td>Highland Creek,Rouge Hill,Port Union</td>
      <td>M1C</td>
      <td>43.784535</td>
      <td>-79.160497</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Scarborough</td>
      <td>Guildwood,Morningside,West Hill</td>
      <td>M1E</td>
      <td>43.763573</td>
      <td>-79.188711</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Scarborough</td>
      <td>Woburn</td>
      <td>M1G</td>
      <td>43.770992</td>
      <td>-79.216917</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
      <td>M1H</td>
      <td>43.773136</td>
      <td>-79.239476</td>
    </tr>
  </tbody>
</table>
</div>




```python
geo_df = geo_df[["Postal Code", "Borough", "Neighbourhood", "Latitude", "Longitude"]]
geo_df.rename(columns={"Postal Code":"PostalCode"}, inplace=True)
geo_df.head(11)
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighbourhood</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Rouge,Malvern</td>
      <td>43.806686</td>
      <td>-79.194353</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Highland Creek,Rouge Hill,Port Union</td>
      <td>43.784535</td>
      <td>-79.160497</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>Scarborough</td>
      <td>Guildwood,Morningside,West Hill</td>
      <td>43.763573</td>
      <td>-79.188711</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>Scarborough</td>
      <td>Woburn</td>
      <td>43.770992</td>
      <td>-79.216917</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
      <td>43.773136</td>
      <td>-79.239476</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M1J</td>
      <td>Scarborough</td>
      <td>Scarborough Village</td>
      <td>43.744734</td>
      <td>-79.239476</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M1K</td>
      <td>Scarborough</td>
      <td>East Birchmount Park,Ionview,Kennedy Park</td>
      <td>43.727929</td>
      <td>-79.262029</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M1L</td>
      <td>Scarborough</td>
      <td>Clairlea,Golden Mile,Oakridge</td>
      <td>43.711112</td>
      <td>-79.284577</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M1M</td>
      <td>Scarborough</td>
      <td>Cliffcrest,Cliffside,Scarborough Village West</td>
      <td>43.716316</td>
      <td>-79.239476</td>
    </tr>
    <tr>
      <th>9</th>
      <td>M1N</td>
      <td>Scarborough</td>
      <td>Birch Cliff,Cliffside West</td>
      <td>43.692657</td>
      <td>-79.264848</td>
    </tr>
    <tr>
      <th>10</th>
      <td>M1P</td>
      <td>Scarborough</td>
      <td>Dorset Park,Scarborough Town Centre,Wexford He...</td>
      <td>43.757410</td>
      <td>-79.273304</td>
    </tr>
  </tbody>
</table>
</div>



### First initial visual look at the locations


```python
# create map of Toronto using latitude and longitude values
import folium
map_test = folium.Map(location=["43.6532", "-79.3832"])

# add markers to map
for lat, lng, borough, neighborhood in zip(geo_df['Latitude'], geo_df['Longitude'], geo_df['Borough'], geo_df['Neighbourhood']):
    label = '{}, {}'.format(neighborhood, borough)
    label = folium.Popup(label, parse_html=True)
    folium.CircleMarker(
        [lat, lng],
        radius=5,
        popup=label,
        color='blue',
        fill=True,
        fill_color='#3186cc',
        fill_opacity=0.7,
        parse_html=False).add_to(map_test)  
    
map_test
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgCiAgICAgICAgPHNjcmlwdD4KICAgICAgICAgICAgTF9OT19UT1VDSCA9IGZhbHNlOwogICAgICAgICAgICBMX0RJU0FCTEVfM0QgPSBmYWxzZTsKICAgICAgICA8L3NjcmlwdD4KICAgIAogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuanMiPjwvc2NyaXB0PgogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY29kZS5qcXVlcnkuY29tL2pxdWVyeS0xLjEyLjQubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9qcy9ib290c3RyYXAubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5qcyI+PC9zY3JpcHQ+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vYm9vdHN0cmFwLzMuMi4wL2Nzcy9ib290c3RyYXAubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLXRoZW1lLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9mb250LWF3ZXNvbWUvNC42LjMvY3NzL2ZvbnQtYXdlc29tZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuanMuY2xvdWRmbGFyZS5jb20vYWpheC9saWJzL0xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLzIuMC4yL2xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL3Jhd2Nkbi5naXRoYWNrLmNvbS9weXRob24tdmlzdWFsaXphdGlvbi9mb2xpdW0vbWFzdGVyL2ZvbGl1bS90ZW1wbGF0ZXMvbGVhZmxldC5hd2Vzb21lLnJvdGF0ZS5jc3MiLz4KICAgIDxzdHlsZT5odG1sLCBib2R5IHt3aWR0aDogMTAwJTtoZWlnaHQ6IDEwMCU7bWFyZ2luOiAwO3BhZGRpbmc6IDA7fTwvc3R5bGU+CiAgICA8c3R5bGU+I21hcCB7cG9zaXRpb246YWJzb2x1dGU7dG9wOjA7Ym90dG9tOjA7cmlnaHQ6MDtsZWZ0OjA7fTwvc3R5bGU+CiAgICAKICAgICAgICAgICAgPG1ldGEgbmFtZT0idmlld3BvcnQiIGNvbnRlbnQ9IndpZHRoPWRldmljZS13aWR0aCwKICAgICAgICAgICAgICAgIGluaXRpYWwtc2NhbGU9MS4wLCBtYXhpbXVtLXNjYWxlPTEuMCwgdXNlci1zY2FsYWJsZT1ubyIgLz4KICAgICAgICAgICAgPHN0eWxlPgogICAgICAgICAgICAgICAgI21hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSB7CiAgICAgICAgICAgICAgICAgICAgcG9zaXRpb246IHJlbGF0aXZlOwogICAgICAgICAgICAgICAgICAgIHdpZHRoOiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgbGVmdDogMC4wJTsKICAgICAgICAgICAgICAgICAgICB0b3A6IDAuMCU7CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIDwvc3R5bGU+CiAgICAgICAgCjwvaGVhZD4KPGJvZHk+ICAgIAogICAgCiAgICAgICAgICAgIDxkaXYgY2xhc3M9ImZvbGl1bS1tYXAiIGlkPSJtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEiID48L2Rpdj4KICAgICAgICAKPC9ib2R5Pgo8c2NyaXB0PiAgICAKICAgIAogICAgICAgICAgICB2YXIgbWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhID0gTC5tYXAoCiAgICAgICAgICAgICAgICAibWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhIiwKICAgICAgICAgICAgICAgIHsKICAgICAgICAgICAgICAgICAgICBjZW50ZXI6IFs0My42NTMyLCAtNzkuMzgzMl0sCiAgICAgICAgICAgICAgICAgICAgY3JzOiBMLkNSUy5FUFNHMzg1NywKICAgICAgICAgICAgICAgICAgICB6b29tOiAxMCwKICAgICAgICAgICAgICAgICAgICB6b29tQ29udHJvbDogdHJ1ZSwKICAgICAgICAgICAgICAgICAgICBwcmVmZXJDYW52YXM6IGZhbHNlLAogICAgICAgICAgICAgICAgfQogICAgICAgICAgICApOwoKICAgICAgICAgICAgCgogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyXzk0YzQyNGYyMjEwZDQxM2U5MzM0MDA4ZTZjMTcxOTViID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAiaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmciLAogICAgICAgICAgICAgICAgeyJhdHRyaWJ1dGlvbiI6ICJEYXRhIGJ5IFx1MDAyNmNvcHk7IFx1MDAzY2EgaHJlZj1cImh0dHA6Ly9vcGVuc3RyZWV0bWFwLm9yZ1wiXHUwMDNlT3BlblN0cmVldE1hcFx1MDAzYy9hXHUwMDNlLCB1bmRlciBcdTAwM2NhIGhyZWY9XCJodHRwOi8vd3d3Lm9wZW5zdHJlZXRtYXAub3JnL2NvcHlyaWdodFwiXHUwMDNlT0RiTFx1MDAzYy9hXHUwMDNlLiIsICJkZXRlY3RSZXRpbmEiOiBmYWxzZSwgIm1heE5hdGl2ZVpvb20iOiAxOCwgIm1heFpvb20iOiAxOCwgIm1pblpvb20iOiAwLCAibm9XcmFwIjogZmFsc2UsICJvcGFjaXR5IjogMSwgInN1YmRvbWFpbnMiOiAiYWJjIiwgInRtcyI6IGZhbHNlfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZTE1ODQwN2QwZDVjNGRkZjgwMzRlMTdlZTUyMzI2ODQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My44MDY2ODYyOTk5OTk5OTYsIC03OS4xOTQzNTM0MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF85MzJkM2ZlNTQyYzY0MTM2YmU1NTAzMDY1YmQyZjIwZiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYzRiODQ1ZWVmZDY1NGRjMmI3OWRiYjhlODkxZTU0ZTcgPSAkKGA8ZGl2IGlkPSJodG1sX2M0Yjg0NWVlZmQ2NTRkYzJiNzlkYmI4ZTg5MWU1NGU3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Sb3VnZSxNYWx2ZXJuLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF85MzJkM2ZlNTQyYzY0MTM2YmU1NTAzMDY1YmQyZjIwZi5zZXRDb250ZW50KGh0bWxfYzRiODQ1ZWVmZDY1NGRjMmI3OWRiYjhlODkxZTU0ZTcpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2UxNTg0MDdkMGQ1YzRkZGY4MDM0ZTE3ZWU1MjMyNjg0LmJpbmRQb3B1cChwb3B1cF85MzJkM2ZlNTQyYzY0MTM2YmU1NTAzMDY1YmQyZjIwZikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTg4ZWFlNjQ4YTQ5NGY3MDk0ZmRmZTkzYzY0YTA4ZDcgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43ODQ1MzUxLCAtNzkuMTYwNDk3MDk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZGQyODFhY2VmNDBhNDMxZmIxMjgyZmU3OGI1YmJlNWEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQwODYwODJjNDRmMzRjOGU5NDRiZTY4OTc4NzI0YWY1ID0gJChgPGRpdiBpZD0iaHRtbF80MDg2MDgyYzQ0ZjM0YzhlOTQ0YmU2ODk3ODcyNGFmNSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+SGlnaGxhbmQgQ3JlZWssUm91Z2UgSGlsbCxQb3J0IFVuaW9uLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9kZDI4MWFjZWY0MGE0MzFmYjEyODJmZTc4YjViYmU1YS5zZXRDb250ZW50KGh0bWxfNDA4NjA4MmM0NGYzNGM4ZTk0NGJlNjg5Nzg3MjRhZjUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2E4OGVhZTY0OGE0OTRmNzA5NGZkZmU5M2M2NGEwOGQ3LmJpbmRQb3B1cChwb3B1cF9kZDI4MWFjZWY0MGE0MzFmYjEyODJmZTc4YjViYmU1YSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZTBlZjljOGIwMjdlNDg1YTkxNDczMjFiZDc0MzllOGIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NjM1NzI2LCAtNzkuMTg4NzExNV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF84NDc2MzU3ZTdiMTA0MzI0YjZmZWExMmUyZDU5ODIxNiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYjE0MzJkY2YzN2UyNDdiNjliYTQ2ZTY3NGVhYjgxNmMgPSAkKGA8ZGl2IGlkPSJodG1sX2IxNDMyZGNmMzdlMjQ3YjY5YmE0NmU2NzRlYWI4MTZjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5HdWlsZHdvb2QsTW9ybmluZ3NpZGUsV2VzdCBIaWxsLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF84NDc2MzU3ZTdiMTA0MzI0YjZmZWExMmUyZDU5ODIxNi5zZXRDb250ZW50KGh0bWxfYjE0MzJkY2YzN2UyNDdiNjliYTQ2ZTY3NGVhYjgxNmMpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2UwZWY5YzhiMDI3ZTQ4NWE5MTQ3MzIxYmQ3NDM5ZThiLmJpbmRQb3B1cChwb3B1cF84NDc2MzU3ZTdiMTA0MzI0YjZmZWExMmUyZDU5ODIxNikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfY2JiNTQ3YzdkYzEwNDFkZDk2ZWI4NTkwZGNjYmVjZjMgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NzA5OTIxLCAtNzkuMjE2OTE3NDAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZmJjZWE0NzAzZTgyNDEwN2JhOTI2ZTg4Y2RiZTRiMzQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2FjY2JmMjJlMjJhMzQxNDQ4MzI3ODY5NGU3OTllYzEzID0gJChgPGRpdiBpZD0iaHRtbF9hY2NiZjIyZTIyYTM0MTQ0ODMyNzg2OTRlNzk5ZWMxMyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+V29idXJuLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9mYmNlYTQ3MDNlODI0MTA3YmE5MjZlODhjZGJlNGIzNC5zZXRDb250ZW50KGh0bWxfYWNjYmYyMmUyMmEzNDE0NDgzMjc4Njk0ZTc5OWVjMTMpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2NiYjU0N2M3ZGMxMDQxZGQ5NmViODU5MGRjY2JlY2YzLmJpbmRQb3B1cChwb3B1cF9mYmNlYTQ3MDNlODI0MTA3YmE5MjZlODhjZGJlNGIzNCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYzYwMzExNjE4MzhiNGRjZDk0NTc4YjFkYjVjYmZkOWUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NzMxMzYsIC03OS4yMzk0NzYwOTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF82YTM4ZDk1NDI5ZTg0NWExYjNjNThhYzI1N2Q4NjY5YiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMWZiMDFlNGJiOTRiNGYyMmE3NzBmYzEyYTU0YTA3MTEgPSAkKGA8ZGl2IGlkPSJodG1sXzFmYjAxZTRiYjk0YjRmMjJhNzcwZmMxMmE1NGEwNzExIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DZWRhcmJyYWUsIFNjYXJib3JvdWdoPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzZhMzhkOTU0MjllODQ1YTFiM2M1OGFjMjU3ZDg2NjliLnNldENvbnRlbnQoaHRtbF8xZmIwMWU0YmI5NGI0ZjIyYTc3MGZjMTJhNTRhMDcxMSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYzYwMzExNjE4MzhiNGRjZDk0NTc4YjFkYjVjYmZkOWUuYmluZFBvcHVwKHBvcHVwXzZhMzhkOTU0MjllODQ1YTFiM2M1OGFjMjU3ZDg2NjliKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80NGUzNGM5NmZkYTc0NTU5YTc0NDU3NGU2MmJmMWQwYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjc0NDczNDIsIC03OS4yMzk0NzYwOTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8wMDcxNTYxNjkxYzk0NTkxYjg2NmQxMjhlNDU5MTk2MSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYTMxMzIxYTNjMWIzNDgzZWJmNmM0ZTU5Y2MxODU4YWEgPSAkKGA8ZGl2IGlkPSJodG1sX2EzMTMyMWEzYzFiMzQ4M2ViZjZjNGU1OWNjMTg1OGFhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TY2FyYm9yb3VnaCBWaWxsYWdlLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8wMDcxNTYxNjkxYzk0NTkxYjg2NmQxMjhlNDU5MTk2MS5zZXRDb250ZW50KGh0bWxfYTMxMzIxYTNjMWIzNDgzZWJmNmM0ZTU5Y2MxODU4YWEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzQ0ZTM0Yzk2ZmRhNzQ1NTlhNzQ0NTc0ZTYyYmYxZDBiLmJpbmRQb3B1cChwb3B1cF8wMDcxNTYxNjkxYzk0NTkxYjg2NmQxMjhlNDU5MTk2MSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNTBlN2M0N2VlOTJiNGNlN2FhNWRlZTE4NjVhYzExZTkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43Mjc5MjkyLCAtNzkuMjYyMDI5NDAwMDAwMDJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfN2RjMjIxYjBkNTg3NGNlM2FiOWVlYzk5NjVhODI4ZGMgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2ZlNDA4YTIxMWZlNzQ0MTM4OGUwYWZmY2Y2OTUxZmFlID0gJChgPGRpdiBpZD0iaHRtbF9mZTQwOGEyMTFmZTc0NDEzODhlMGFmZmNmNjk1MWZhZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RWFzdCBCaXJjaG1vdW50IFBhcmssSW9udmlldyxLZW5uZWR5IFBhcmssIFNjYXJib3JvdWdoPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzdkYzIyMWIwZDU4NzRjZTNhYjllZWM5OTY1YTgyOGRjLnNldENvbnRlbnQoaHRtbF9mZTQwOGEyMTFmZTc0NDEzODhlMGFmZmNmNjk1MWZhZSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNTBlN2M0N2VlOTJiNGNlN2FhNWRlZTE4NjVhYzExZTkuYmluZFBvcHVwKHBvcHVwXzdkYzIyMWIwZDU4NzRjZTNhYjllZWM5OTY1YTgyOGRjKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9iMTBhODE4MDI0NWQ0ODk0OTkzYzIyMGJjZjE0NTNkNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcxMTExMTcwMDAwMDAwNCwgLTc5LjI4NDU3NzJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMzM2M2IwNzc4YTZjNDMzOTk4OGNjNDY1ZDAxYTlkNGYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzljODY2NmRhYzU0MzQ0MGE4Mjk1ZjIxNWI0ZTNhNjEzID0gJChgPGRpdiBpZD0iaHRtbF85Yzg2NjZkYWM1NDM0NDBhODI5NWYyMTViNGUzYTYxMyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2xhaXJsZWEsR29sZGVuIE1pbGUsT2FrcmlkZ2UsIFNjYXJib3JvdWdoPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzMzNjNiMDc3OGE2YzQzMzk5ODhjYzQ2NWQwMWE5ZDRmLnNldENvbnRlbnQoaHRtbF85Yzg2NjZkYWM1NDM0NDBhODI5NWYyMTViNGUzYTYxMyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYjEwYTgxODAyNDVkNDg5NDk5M2MyMjBiY2YxNDUzZDYuYmluZFBvcHVwKHBvcHVwXzMzNjNiMDc3OGE2YzQzMzk5ODhjYzQ2NWQwMWE5ZDRmKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9kYjY4YmQ2NDk5Nzc0ODZjYTM4NjlhMzhlNzA1MjNmZCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcxNjMxNiwgLTc5LjIzOTQ3NjA5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2FjODQ0YjMzMzQ5NjQyZDBiMTRjNjcyNTg5MWNkMmJlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8zZmNmNTRkMTk1MzU0OWIzYjk0OGQ5MGM3ZDIwMDNhZiA9ICQoYDxkaXYgaWQ9Imh0bWxfM2ZjZjU0ZDE5NTM1NDliM2I5NDhkOTBjN2QyMDAzYWYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNsaWZmY3Jlc3QsQ2xpZmZzaWRlLFNjYXJib3JvdWdoIFZpbGxhZ2UgV2VzdCwgU2NhcmJvcm91Z2g8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfYWM4NDRiMzMzNDk2NDJkMGIxNGM2NzI1ODkxY2QyYmUuc2V0Q29udGVudChodG1sXzNmY2Y1NGQxOTUzNTQ5YjNiOTQ4ZDkwYzdkMjAwM2FmKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9kYjY4YmQ2NDk5Nzc0ODZjYTM4NjlhMzhlNzA1MjNmZC5iaW5kUG9wdXAocG9wdXBfYWM4NDRiMzMzNDk2NDJkMGIxNGM2NzI1ODkxY2QyYmUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzlhNjU1M2RkYTIxMzQ5M2JiNTM3Mjc3MGQxMGNhM2RhID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjkyNjU3MDAwMDAwMDA0LCAtNzkuMjY0ODQ4MV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF85YmZjNGI0Y2FiZTk0YzQ4YWZkOGFkMWRjYmMzOTAwNCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYmZjOWUyZTg0MjNmNDE2MmFmZWU4MThiOWY5YjMyZmYgPSAkKGA8ZGl2IGlkPSJodG1sX2JmYzllMmU4NDIzZjQxNjJhZmVlODE4YjlmOWIzMmZmIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CaXJjaCBDbGlmZixDbGlmZnNpZGUgV2VzdCwgU2NhcmJvcm91Z2g8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfOWJmYzRiNGNhYmU5NGM0OGFmZDhhZDFkY2JjMzkwMDQuc2V0Q29udGVudChodG1sX2JmYzllMmU4NDIzZjQxNjJhZmVlODE4YjlmOWIzMmZmKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl85YTY1NTNkZGEyMTM0OTNiYjUzNzI3NzBkMTBjYTNkYS5iaW5kUG9wdXAocG9wdXBfOWJmYzRiNGNhYmU5NGM0OGFmZDhhZDFkY2JjMzkwMDQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2YxYTAyMjQ0ZGU2OTQ1YTViZWIwODQ3ZmFlMjI0M2UyID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzU3NDA5NiwgLTc5LjI3MzMwNDAwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzNmODlmMjEyODQ2YzRjMDJiMzhlNDkwYjFjMjJiYzgzID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9mMGMxNjFhMjFiMWU0ZDk0OTc5YWYxYTdiOGVhZmRhOSA9ICQoYDxkaXYgaWQ9Imh0bWxfZjBjMTYxYTIxYjFlNGQ5NDk3OWFmMWE3YjhlYWZkYTkiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkRvcnNldCBQYXJrLFNjYXJib3JvdWdoIFRvd24gQ2VudHJlLFdleGZvcmQgSGVpZ2h0cywgU2NhcmJvcm91Z2g8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfM2Y4OWYyMTI4NDZjNGMwMmIzOGU0OTBiMWMyMmJjODMuc2V0Q29udGVudChodG1sX2YwYzE2MWEyMWIxZTRkOTQ5NzlhZjFhN2I4ZWFmZGE5KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9mMWEwMjI0NGRlNjk0NWE1YmViMDg0N2ZhZTIyNDNlMi5iaW5kUG9wdXAocG9wdXBfM2Y4OWYyMTI4NDZjNGMwMmIzOGU0OTBiMWMyMmJjODMpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzViMTk4YTVmMGIzODQwZWVhOGRmNmMyYzU2ZTYwYzM2ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzUwMDcxNTAwMDAwMDA0LCAtNzkuMjk1ODQ5MV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9jOWRiNDczZTU4ZjA0M2NhODEwZjFhNDMyZmY2YzM5ZSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMmFlMjBlNjE5YzI5NDRiYmFmOTIyOTcyYzM4ZWQyYjEgPSAkKGA8ZGl2IGlkPSJodG1sXzJhZTIwZTYxOWMyOTQ0YmJhZjkyMjk3MmMzOGVkMmIxIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5NYXJ5dmFsZSxXZXhmb3JkLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9jOWRiNDczZTU4ZjA0M2NhODEwZjFhNDMyZmY2YzM5ZS5zZXRDb250ZW50KGh0bWxfMmFlMjBlNjE5YzI5NDRiYmFmOTIyOTcyYzM4ZWQyYjEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzViMTk4YTVmMGIzODQwZWVhOGRmNmMyYzU2ZTYwYzM2LmJpbmRQb3B1cChwb3B1cF9jOWRiNDczZTU4ZjA0M2NhODEwZjFhNDMyZmY2YzM5ZSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOGIxODI5MWRmMzJkNDgzOWJjOTZmYjk5Njk2NTkzYmUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43OTQyMDAzLCAtNzkuMjYyMDI5NDAwMDAwMDJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYjJjM2E1YjEyZmIxNDZlNGJiMTNmYzYxNzcwODJkZjQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2FkNDhjZGE1NzM4YjRmYmM4NGE5YTQwYTVjNjkxNmM2ID0gJChgPGRpdiBpZD0iaHRtbF9hZDQ4Y2RhNTczOGI0ZmJjODRhOWE0MGE1YzY5MTZjNiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QWdpbmNvdXJ0LCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9iMmMzYTViMTJmYjE0NmU0YmIxM2ZjNjE3NzA4MmRmNC5zZXRDb250ZW50KGh0bWxfYWQ0OGNkYTU3MzhiNGZiYzg0YTlhNDBhNWM2OTE2YzYpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzhiMTgyOTFkZjMyZDQ4MzliYzk2ZmI5OTY5NjU5M2JlLmJpbmRQb3B1cChwb3B1cF9iMmMzYTViMTJmYjE0NmU0YmIxM2ZjNjE3NzA4MmRmNCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTU2YTg3MDI3ZjhmNDU0YTk3MGRjZTM0MzRjYTUyNTEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43ODE2Mzc1LCAtNzkuMzA0MzAyMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8wNGI3MGM5ZmIxNWM0NGMwODZiZjM3ZDUzMTUyNWExMyA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYzRlNDczMGE5NjNhNGZhNGExNTY4ZmE5Y2Y1MTA3Y2QgPSAkKGA8ZGl2IGlkPSJodG1sX2M0ZTQ3MzBhOTYzYTRmYTRhMTU2OGZhOWNmNTEwN2NkIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DbGFya3MgQ29ybmVycyxTdWxsaXZhbixUYW0gTyYjMzk7U2hhbnRlciwgU2NhcmJvcm91Z2g8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMDRiNzBjOWZiMTVjNDRjMDg2YmYzN2Q1MzE1MjVhMTMuc2V0Q29udGVudChodG1sX2M0ZTQ3MzBhOTYzYTRmYTRhMTU2OGZhOWNmNTEwN2NkKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9hNTZhODcwMjdmOGY0NTRhOTcwZGNlMzQzNGNhNTI1MS5iaW5kUG9wdXAocG9wdXBfMDRiNzBjOWZiMTVjNDRjMDg2YmYzN2Q1MzE1MjVhMTMpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2JiZjEzNDc5MDlhMDQ2YTBhODE2OGQ5YzNmOTMwNjIxID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuODE1MjUyMiwgLTc5LjI4NDU3NzJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYzkxZjJhMmEwMWZlNGNhZDhmY2M1YzM3NjdiNWM5ZDAgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzNkYTM1N2E5ZGRiNTQxNjNhNWUxZjBhNGVhNTQyNjgyID0gJChgPGRpdiBpZD0iaHRtbF8zZGEzNTdhOWRkYjU0MTYzYTVlMWYwYTRlYTU0MjY4MiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QWdpbmNvdXJ0IE5vcnRoLEwmIzM5O0Ftb3JlYXV4IEVhc3QsTWlsbGlrZW4sU3RlZWxlcyBFYXN0LCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9jOTFmMmEyYTAxZmU0Y2FkOGZjYzVjMzc2N2I1YzlkMC5zZXRDb250ZW50KGh0bWxfM2RhMzU3YTlkZGI1NDE2M2E1ZTFmMGE0ZWE1NDI2ODIpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2JiZjEzNDc5MDlhMDQ2YTBhODE2OGQ5YzNmOTMwNjIxLmJpbmRQb3B1cChwb3B1cF9jOTFmMmEyYTAxZmU0Y2FkOGZjYzVjMzc2N2I1YzlkMCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzMyNDMyZjliZDMyNGRkNmJiOTY2YmJhYjViOGRmN2YgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43OTk1MjUyMDAwMDAwMDUsIC03OS4zMTgzODg3XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzZiNTg1YWZiMThlMzQzMzA4YzVjY2Q2Y2E3NDZmMzkxID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83ZWZlYTNhYWE2OGM0ZGMzYWU4NWM1MDRlNzMyNzQ2OCA9ICQoYDxkaXYgaWQ9Imh0bWxfN2VmZWEzYWFhNjhjNGRjM2FlODVjNTA0ZTczMjc0NjgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkwmIzM5O0Ftb3JlYXV4IFdlc3QsIFNjYXJib3JvdWdoPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzZiNTg1YWZiMThlMzQzMzA4YzVjY2Q2Y2E3NDZmMzkxLnNldENvbnRlbnQoaHRtbF83ZWZlYTNhYWE2OGM0ZGMzYWU4NWM1MDRlNzMyNzQ2OCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMzMyNDMyZjliZDMyNGRkNmJiOTY2YmJhYjViOGRmN2YuYmluZFBvcHVwKHBvcHVwXzZiNTg1YWZiMThlMzQzMzA4YzVjY2Q2Y2E3NDZmMzkxKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8zYWYyY2ZjYjYzYjI0ZjNkOTE3ZTk3ZGM2OTMzZmQ4YiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjgzNjEyNDcwMDAwMDAwNiwgLTc5LjIwNTYzNjA5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2FlYmJiN2Y4ZWQ3YTQ0MGM4ZGFhMGIzOWIzMzk2ZDcwID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9mZWQ1MWE4OWU5MmU0ZWZhYTQ1NmI1ZTk0YzM1OTk4MiA9ICQoYDxkaXYgaWQ9Imh0bWxfZmVkNTFhODllOTJlNGVmYWE0NTZiNWU5NGMzNTk5ODIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlVwcGVyIFJvdWdlLCBTY2FyYm9yb3VnaDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9hZWJiYjdmOGVkN2E0NDBjOGRhYTBiMzliMzM5NmQ3MC5zZXRDb250ZW50KGh0bWxfZmVkNTFhODllOTJlNGVmYWE0NTZiNWU5NGMzNTk5ODIpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzNhZjJjZmNiNjNiMjRmM2Q5MTdlOTdkYzY5MzNmZDhiLmJpbmRQb3B1cChwb3B1cF9hZWJiYjdmOGVkN2E0NDBjOGRhYTBiMzliMzM5NmQ3MCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfY2IzNGI3MjVlYjc1NGZkNmFiMTEyZjVkYjY4YTY4NjkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My44MDM3NjIyLCAtNzkuMzYzNDUxN10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF84MDA1ZjdlYTNmZjc0YWY4ODExMTdhMTdjMGQzOGQ3MiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMjExMDE3ZDkxOTVjNDViNzg1MzUzZmQ3NTYzZjhhZDAgPSAkKGA8ZGl2IGlkPSJodG1sXzIxMTAxN2Q5MTk1YzQ1Yjc4NTM1M2ZkNzU2M2Y4YWQwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IaWxsY3Jlc3QgVmlsbGFnZSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF84MDA1ZjdlYTNmZjc0YWY4ODExMTdhMTdjMGQzOGQ3Mi5zZXRDb250ZW50KGh0bWxfMjExMDE3ZDkxOTVjNDViNzg1MzUzZmQ3NTYzZjhhZDApOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2NiMzRiNzI1ZWI3NTRmZDZhYjExMmY1ZGI2OGE2ODY5LmJpbmRQb3B1cChwb3B1cF84MDA1ZjdlYTNmZjc0YWY4ODExMTdhMTdjMGQzOGQ3MikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZmJhMGEwMTcyY2EyNGRhMGFlMzdkMDNmMjQzMGMyMTMgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43Nzg1MTc1LCAtNzkuMzQ2NTU1N10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8zZjhmNTYzYTg1MTg0ZGVkYTE5ZTFiMjZlOTAwN2UyOSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZGE2MzA5NDY5OTA1NGE0YmI3M2Y1YTQxYjkzMTU0MmIgPSAkKGA8ZGl2IGlkPSJodG1sX2RhNjMwOTQ2OTkwNTRhNGJiNzNmNWE0MWI5MzE1NDJiIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5GYWlydmlldyxIZW5yeSBGYXJtLE9yaW9sZSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8zZjhmNTYzYTg1MTg0ZGVkYTE5ZTFiMjZlOTAwN2UyOS5zZXRDb250ZW50KGh0bWxfZGE2MzA5NDY5OTA1NGE0YmI3M2Y1YTQxYjkzMTU0MmIpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2ZiYTBhMDE3MmNhMjRkYTBhZTM3ZDAzZjI0MzBjMjEzLmJpbmRQb3B1cChwb3B1cF8zZjhmNTYzYTg1MTg0ZGVkYTE5ZTFiMjZlOTAwN2UyOSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZDM1MWQ0MDMwZDQ5NDZiY2I2MDBjZWU3YzNiZjk4NzggPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43ODY5NDczLCAtNzkuMzg1OTc1XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzgxZTFmOGU1MzM0YzQxN2RhMWViMTI1M2FmOWJmYTVlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF80MjE5MTgzNGI4MjQ0NTc3YmUzZmEyZWU0NjUwMTMzNyA9ICQoYDxkaXYgaWQ9Imh0bWxfNDIxOTE4MzRiODI0NDU3N2JlM2ZhMmVlNDY1MDEzMzciIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJheXZpZXcgVmlsbGFnZSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF84MWUxZjhlNTMzNGM0MTdkYTFlYjEyNTNhZjliZmE1ZS5zZXRDb250ZW50KGh0bWxfNDIxOTE4MzRiODI0NDU3N2JlM2ZhMmVlNDY1MDEzMzcpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2QzNTFkNDAzMGQ0OTQ2YmNiNjAwY2VlN2MzYmY5ODc4LmJpbmRQb3B1cChwb3B1cF84MWUxZjhlNTMzNGM0MTdkYTFlYjEyNTNhZjliZmE1ZSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOWQzZGYyY2YyNWQ2NDZjMDg0Y2FiMjI0NmQzNGRjMDYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NTc0OTAyLCAtNzkuMzc0NzE0MDk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMTRhYzhiZDBmNTc2NDQwMmE3NzE0NDQxMmUwNTk4N2IgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2I1M2I4ZjMzNmIwYzQ0NWNhYjU3NjEyY2I1MDgwZmUyID0gJChgPGRpdiBpZD0iaHRtbF9iNTNiOGYzMzZiMGM0NDVjYWI1NzYxMmNiNTA4MGZlMiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+U2lsdmVyIEhpbGxzLFlvcmsgTWlsbHMsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMTRhYzhiZDBmNTc2NDQwMmE3NzE0NDQxMmUwNTk4N2Iuc2V0Q29udGVudChodG1sX2I1M2I4ZjMzNmIwYzQ0NWNhYjU3NjEyY2I1MDgwZmUyKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl85ZDNkZjJjZjI1ZDY0NmMwODRjYWIyMjQ2ZDM0ZGMwNi5iaW5kUG9wdXAocG9wdXBfMTRhYzhiZDBmNTc2NDQwMmE3NzE0NDQxMmUwNTk4N2IpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2UxZTVhZDU0YTBjYTQ3Yzc5MzRkNWE2NzVmZmMyYTQwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzg5MDUzLCAtNzkuNDA4NDkyNzk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYjQ2MGVlYmZkMjViNGYxN2IxMjdiYzczNmFjZmVlZDMgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2U5NTQ4ZWM3YzdhNjQxNWFiMzdlYzhjZGU3NjRkMDRlID0gJChgPGRpdiBpZD0iaHRtbF9lOTU0OGVjN2M3YTY0MTVhYjM3ZWM4Y2RlNzY0ZDA0ZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TmV3dG9uYnJvb2ssV2lsbG93ZGFsZSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9iNDYwZWViZmQyNWI0ZjE3YjEyN2JjNzM2YWNmZWVkMy5zZXRDb250ZW50KGh0bWxfZTk1NDhlYzdjN2E2NDE1YWIzN2VjOGNkZTc2NGQwNGUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2UxZTVhZDU0YTBjYTQ3Yzc5MzRkNWE2NzVmZmMyYTQwLmJpbmRQb3B1cChwb3B1cF9iNDYwZWViZmQyNWI0ZjE3YjEyN2JjNzM2YWNmZWVkMykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNmExZWQyMGQyZmNmNGEzMWE4NTlkMjkyNTM5MDZkOTAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NzAxMTk5LCAtNzkuNDA4NDkyNzk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNzBiYTdjYTdmN2E4NDQ5NjkzMjRiOTMxOWIxMWQ4NTIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzUyMmQzMzcxYmQ5MTRkYTE5ZTY0NWQ2ZjNlYTE5ZTM5ID0gJChgPGRpdiBpZD0iaHRtbF81MjJkMzM3MWJkOTE0ZGExOWU2NDVkNmYzZWExOWUzOSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+V2lsbG93ZGFsZSBTb3V0aCwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83MGJhN2NhN2Y3YTg0NDk2OTMyNGI5MzE5YjExZDg1Mi5zZXRDb250ZW50KGh0bWxfNTIyZDMzNzFiZDkxNGRhMTllNjQ1ZDZmM2VhMTllMzkpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzZhMWVkMjBkMmZjZjRhMzFhODU5ZDI5MjUzOTA2ZDkwLmJpbmRQb3B1cChwb3B1cF83MGJhN2NhN2Y3YTg0NDk2OTMyNGI5MzE5YjExZDg1MikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMTU1MGEyNzI2M2YwNDAwZGFlYjFlODdmZjY5MGMxMGUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NTI3NTgyOTk5OTk5OTYsIC03OS40MDAwNDkzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzkzNzAzMjFkMTdmZjQyNjJhMzc4MmFiNjVkNDRlODZhID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF82MGIwNGRiY2Y1ODQ0MzUwODI1NjMzMzI1ZGQ0ZGE3OCA9ICQoYDxkaXYgaWQ9Imh0bWxfNjBiMDRkYmNmNTg0NDM1MDgyNTYzMzMyNWRkNGRhNzgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPllvcmsgTWlsbHMgV2VzdCwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF85MzcwMzIxZDE3ZmY0MjYyYTM3ODJhYjY1ZDQ0ZTg2YS5zZXRDb250ZW50KGh0bWxfNjBiMDRkYmNmNTg0NDM1MDgyNTYzMzMyNWRkNGRhNzgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzE1NTBhMjcyNjNmMDQwMGRhZWIxZTg3ZmY2OTBjMTBlLmJpbmRQb3B1cChwb3B1cF85MzcwMzIxZDE3ZmY0MjYyYTM3ODJhYjY1ZDQ0ZTg2YSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNjMwYmI2NzVlODY2NDFmNmExNTgyMDVjYmY1ZWEzODIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43ODI3MzY0LCAtNzkuNDQyMjU5M10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF82ZDBjODNlMTg3Yzg0ZmFlYTk1OTUzNmI5Y2RiZTEwMSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNTAxNjAyMTQxYzFkNDA1MDlkMTNiOTJhZDE1ZmVmNGEgPSAkKGA8ZGl2IGlkPSJodG1sXzUwMTYwMjE0MWMxZDQwNTA5ZDEzYjkyYWQxNWZlZjRhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5XaWxsb3dkYWxlIFdlc3QsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNmQwYzgzZTE4N2M4NGZhZWE5NTk1MzZiOWNkYmUxMDEuc2V0Q29udGVudChodG1sXzUwMTYwMjE0MWMxZDQwNTA5ZDEzYjkyYWQxNWZlZjRhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl82MzBiYjY3NWU4NjY0MWY2YTE1ODIwNWNiZjVlYTM4Mi5iaW5kUG9wdXAocG9wdXBfNmQwYzgzZTE4N2M4NGZhZWE5NTk1MzZiOWNkYmUxMDEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzNiNzUwYTcyODZkZDQzNTZiZWVmZjEzMGU5NDZkMjc4ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzUzMjU4NiwgLTc5LjMyOTY1NjVdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZmUyMDM5NzBmYzVmNGMwMjk5NTM5NGU5NGUwZDRlZDggPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzg3N2U2MzI4ZTE1MTRjYzY4YjMyYmNkMjIzMzJlZWJjID0gJChgPGRpdiBpZD0iaHRtbF84NzdlNjMyOGUxNTE0Y2M2OGIzMmJjZDIyMzMyZWViYyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UGFya3dvb2RzLCBOb3J0aCBZb3JrPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2ZlMjAzOTcwZmM1ZjRjMDI5OTUzOTRlOTRlMGQ0ZWQ4LnNldENvbnRlbnQoaHRtbF84NzdlNjMyOGUxNTE0Y2M2OGIzMmJjZDIyMzMyZWViYyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfM2I3NTBhNzI4NmRkNDM1NmJlZWZmMTMwZTk0NmQyNzguYmluZFBvcHVwKHBvcHVwX2ZlMjAzOTcwZmM1ZjRjMDI5OTUzOTRlOTRlMGQ0ZWQ4KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8wNjQ4YTM1MjQ0ZmI0Y2FjYTVkY2U3MjYwYWUyZjY4NiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjc0NTkwNTc5OTk5OTk5NiwgLTc5LjM1MjE4OF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9mNjA0NjBmNDg0OWU0ZTA3YmNkNTg2MDk2YzM0ZmVkMiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNTVmMThmNzU4NWNmNDc2ZDhjMmQ2MzFmNTY1MmY1ODEgPSAkKGA8ZGl2IGlkPSJodG1sXzU1ZjE4Zjc1ODVjZjQ3NmQ4YzJkNjMxZjU2NTJmNTgxIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Eb24gTWlsbHMgTm9ydGgsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfZjYwNDYwZjQ4NDllNGUwN2JjZDU4NjA5NmMzNGZlZDIuc2V0Q29udGVudChodG1sXzU1ZjE4Zjc1ODVjZjQ3NmQ4YzJkNjMxZjU2NTJmNTgxKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8wNjQ4YTM1MjQ0ZmI0Y2FjYTVkY2U3MjYwYWUyZjY4Ni5iaW5kUG9wdXAocG9wdXBfZjYwNDYwZjQ4NDllNGUwN2JjZDU4NjA5NmMzNGZlZDIpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzliMmI1YzUzMDk5OTQ2YWNhNGMzZjRiMjgyYzViMTQ4ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzI1ODk5NzAwMDAwMDEsIC03OS4zNDA5MjNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYmMzZTMxMWVlMDQwNDQ3OWFiYWMwMDBmNDU5NDFhMWEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQyMTRiNDE5NGQ1MDQ1OTBhNjQxYmJkZDRkMTIyMmE3ID0gJChgPGRpdiBpZD0iaHRtbF80MjE0YjQxOTRkNTA0NTkwYTY0MWJiZGQ0ZDEyMjJhNyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RmxlbWluZ2RvbiBQYXJrLERvbiBNaWxscyBTb3V0aCwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9iYzNlMzExZWUwNDA0NDc5YWJhYzAwMGY0NTk0MWExYS5zZXRDb250ZW50KGh0bWxfNDIxNGI0MTk0ZDUwNDU5MGE2NDFiYmRkNGQxMjIyYTcpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzliMmI1YzUzMDk5OTQ2YWNhNGMzZjRiMjgyYzViMTQ4LmJpbmRQb3B1cChwb3B1cF9iYzNlMzExZWUwNDA0NDc5YWJhYzAwMGY0NTk0MWExYSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODdiOGM2YTlmYzg0NDU3OGIzYmEwMjU2YmYzNjgyNGUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43NTQzMjgzLCAtNzkuNDQyMjU5M10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9jZDQxZjQ2MmJiMzY0ODQxYWUwZTZjZDZhOWI5MzAxYiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYjEyOWJhZDEyZmM2NGYyZmFjZGU5MjAyNzMzYTRjOGYgPSAkKGA8ZGl2IGlkPSJodG1sX2IxMjliYWQxMmZjNjRmMmZhY2RlOTIwMjczM2E0YzhmIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CYXRodXJzdCBNYW5vcixEb3duc3ZpZXcgTm9ydGgsV2lsc29uIEhlaWdodHMsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfY2Q0MWY0NjJiYjM2NDg0MWFlMGU2Y2Q2YTliOTMwMWIuc2V0Q29udGVudChodG1sX2IxMjliYWQxMmZjNjRmMmZhY2RlOTIwMjczM2E0YzhmKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl84N2I4YzZhOWZjODQ0NTc4YjNiYTAyNTZiZjM2ODI0ZS5iaW5kUG9wdXAocG9wdXBfY2Q0MWY0NjJiYjM2NDg0MWFlMGU2Y2Q2YTliOTMwMWIpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzQ0OWYxYThmMTcwZTQ3Yjc5NDFmZDE0MWZkMjY4NmMzID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzY3OTgwMywgLTc5LjQ4NzI2MTkwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2FjNDhjNWRiOTEyNjQwNTI5MmI1YmFkODhkOTEzMDE2ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8xYzE3NjkwNDJjM2Y0ODYzOWQ5MTQ1ZmM5YTgzYWY5NiA9ICQoYDxkaXYgaWQ9Imh0bWxfMWMxNzY5MDQyYzNmNDg2MzlkOTE0NWZjOWE4M2FmOTYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk5vcnRod29vZCBQYXJrLFlvcmsgVW5pdmVyc2l0eSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9hYzQ4YzVkYjkxMjY0MDUyOTJiNWJhZDg4ZDkxMzAxNi5zZXRDb250ZW50KGh0bWxfMWMxNzY5MDQyYzNmNDg2MzlkOTE0NWZjOWE4M2FmOTYpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzQ0OWYxYThmMTcwZTQ3Yjc5NDFmZDE0MWZkMjY4NmMzLmJpbmRQb3B1cChwb3B1cF9hYzQ4YzVkYjkxMjY0MDUyOTJiNWJhZDg4ZDkxMzAxNikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDBlYjExMDQ2YTAxNGZlNWE4ZTI1Y2Y0ZTNiMTk0ZTUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43Mzc0NzMyMDAwMDAwMDQsIC03OS40NjQ3NjMyOTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9kNGFhMmE0OTIyYWI0YjQzOGNkZjg1YTIyMDliZWY5MCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMGM2NDM4ODM3YjdmNDk2NWFlZGUzODc2OGEyNzdiNDYgPSAkKGA8ZGl2IGlkPSJodG1sXzBjNjQzODgzN2I3ZjQ5NjVhZWRlMzg3NjhhMjc3YjQ2IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DRkIgVG9yb250byxEb3duc3ZpZXcgRWFzdCwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9kNGFhMmE0OTIyYWI0YjQzOGNkZjg1YTIyMDliZWY5MC5zZXRDb250ZW50KGh0bWxfMGM2NDM4ODM3YjdmNDk2NWFlZGUzODc2OGEyNzdiNDYpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzAwZWIxMTA0NmEwMTRmZTVhOGUyNWNmNGUzYjE5NGU1LmJpbmRQb3B1cChwb3B1cF9kNGFhMmE0OTIyYWI0YjQzOGNkZjg1YTIyMDliZWY5MCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfY2JkMmJkY2FmYzE1NGY0NzgzMmQ4YjExNzIxMDk4NWYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MzkwMTQ2LCAtNzkuNTA2OTQzNl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9hMTcxNTBmMGNlNjI0ZjRkYWVjOWI3MmU1YTFlZjU2MiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZWQ2MDhmNWUzODk0NDgzMGExMjhkNDliMTg3ZGY4ZmUgPSAkKGA8ZGl2IGlkPSJodG1sX2VkNjA4ZjVlMzg5NDQ4MzBhMTI4ZDQ5YjE4N2RmOGZlIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Eb3duc3ZpZXcgV2VzdCwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9hMTcxNTBmMGNlNjI0ZjRkYWVjOWI3MmU1YTFlZjU2Mi5zZXRDb250ZW50KGh0bWxfZWQ2MDhmNWUzODk0NDgzMGExMjhkNDliMTg3ZGY4ZmUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2NiZDJiZGNhZmMxNTRmNDc4MzJkOGIxMTcyMTA5ODVmLmJpbmRQb3B1cChwb3B1cF9hMTcxNTBmMGNlNjI0ZjRkYWVjOWI3MmU1YTFlZjU2MikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNjZjZWY2ODhmM2EzNDk3YThkNmIxMjU0ZWI3MWFiYmQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43Mjg0OTY0LCAtNzkuNDk1Njk3NDAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNDc4OTRiY2RjY2I3NGY3ZjgxYWNiZTdjZTliM2UxM2YgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzMwN2ZkN2M2YThjZTQyODY4YmI2MzUxZThiMmE5MWZhID0gJChgPGRpdiBpZD0iaHRtbF8zMDdmZDdjNmE4Y2U0Mjg2OGJiNjM1MWU4YjJhOTFmYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RG93bnN2aWV3IENlbnRyYWwsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNDc4OTRiY2RjY2I3NGY3ZjgxYWNiZTdjZTliM2UxM2Yuc2V0Q29udGVudChodG1sXzMwN2ZkN2M2YThjZTQyODY4YmI2MzUxZThiMmE5MWZhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl82NmNlZjY4OGYzYTM0OTdhOGQ2YjEyNTRlYjcxYWJiZC5iaW5kUG9wdXAocG9wdXBfNDc4OTRiY2RjY2I3NGY3ZjgxYWNiZTdjZTliM2UxM2YpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzViZjZjYzc3YmZkMTRjNjhiM2FiODI0ZDI2ZWEwMDc0ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzYxNjMxMywgLTc5LjUyMDk5OTQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzk3M2IyZDhjYmMwMzQ3NTliYmU5ZGQ2OWQzNzM5OTdmID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9lMTkwNzBmOGM5MDc0YjA0YTIzNTRjYmEzYTk1MWE5ZiA9ICQoYDxkaXYgaWQ9Imh0bWxfZTE5MDcwZjhjOTA3NGIwNGEyMzU0Y2JhM2E5NTFhOWYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkRvd25zdmlldyBOb3J0aHdlc3QsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfOTczYjJkOGNiYzAzNDc1OWJiZTlkZDY5ZDM3Mzk5N2Yuc2V0Q29udGVudChodG1sX2UxOTA3MGY4YzkwNzRiMDRhMjM1NGNiYTNhOTUxYTlmKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl81YmY2Y2M3N2JmZDE0YzY4YjNhYjgyNGQyNmVhMDA3NC5iaW5kUG9wdXAocG9wdXBfOTczYjJkOGNiYzAzNDc1OWJiZTlkZDY5ZDM3Mzk5N2YpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2RjYzJkNzJhYzYzZjQyZWJhODNhY2U4ZTAxZDM5YzljID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzI1ODgyMjk5OTk5OTk1LCAtNzkuMzE1NTcxNTk5OTk5OThdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZGNjODEwMjA4OWY4NGYyMWI0Y2NjMTVhOGVjZTQ4YzMgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2YwNDMwZjFlY2YyZjQwOGY4MGJjMGQ4OGUwZjc4ZWZlID0gJChgPGRpdiBpZD0iaHRtbF9mMDQzMGYxZWNmMmY0MDhmODBiYzBkODhlMGY3OGVmZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+VmljdG9yaWEgVmlsbGFnZSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9kY2M4MTAyMDg5Zjg0ZjIxYjRjY2MxNWE4ZWNlNDhjMy5zZXRDb250ZW50KGh0bWxfZjA0MzBmMWVjZjJmNDA4ZjgwYmMwZDg4ZTBmNzhlZmUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2RjYzJkNzJhYzYzZjQyZWJhODNhY2U4ZTAxZDM5YzljLmJpbmRQb3B1cChwb3B1cF9kY2M4MTAyMDg5Zjg0ZjIxYjRjY2MxNWE4ZWNlNDhjMykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNDNiOTY5MTNiMDA4NGI5YmI4ODU1NDc2ZGM0OWQ5ZWEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MDYzOTcyLCAtNzkuMzA5OTM3XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2QxZWZiYmZlYTEzZjRkNmE4MTNjM2E4N2ZjNDhkZmI5ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8zMzBjYWE0ODBkYWM0MWIwYjgwYzM4NmEzY2IwYjFjNyA9ICQoYDxkaXYgaWQ9Imh0bWxfMzMwY2FhNDgwZGFjNDFiMGI4MGMzODZhM2NiMGIxYzciIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPldvb2RiaW5lIEdhcmRlbnMsUGFya3ZpZXcgSGlsbCwgRWFzdCBZb3JrPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2QxZWZiYmZlYTEzZjRkNmE4MTNjM2E4N2ZjNDhkZmI5LnNldENvbnRlbnQoaHRtbF8zMzBjYWE0ODBkYWM0MWIwYjgwYzM4NmEzY2IwYjFjNyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNDNiOTY5MTNiMDA4NGI5YmI4ODU1NDc2ZGM0OWQ5ZWEuYmluZFBvcHVwKHBvcHVwX2QxZWZiYmZlYTEzZjRkNmE4MTNjM2E4N2ZjNDhkZmI5KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9jYzNlZWM4ZjcyMDM0NjlkYWI4ZmU2MmJjMjcxMjBjYSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY5NTM0MzkwMDAwMDAwNSwgLTc5LjMxODM4ODddLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZjJjOWJkZTk5MmYxNGNmYzkwMmM0OGJjMDY4YzJiNGMgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzk0YzA0ZmM2ZTkyMjQwZmU4N2JlOGRjZTBkZjk4N2JmID0gJChgPGRpdiBpZD0iaHRtbF85NGMwNGZjNmU5MjI0MGZlODdiZThkY2UwZGY5ODdiZiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+V29vZGJpbmUgSGVpZ2h0cywgRWFzdCBZb3JrPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2YyYzliZGU5OTJmMTRjZmM5MDJjNDhiYzA2OGMyYjRjLnNldENvbnRlbnQoaHRtbF85NGMwNGZjNmU5MjI0MGZlODdiZThkY2UwZGY5ODdiZik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfY2MzZWVjOGY3MjAzNDY5ZGFiOGZlNjJiYzI3MTIwY2EuYmluZFBvcHVwKHBvcHVwX2YyYzliZGU5OTJmMTRjZmM5MDJjNDhiYzA2OGMyYjRjKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81NTBhNTgzNmYxMTA0NDU0OWRkYWIxZThkMWJmZTVjMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY3NjM1NzM5OTk5OTk5LCAtNzkuMjkzMDMxMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8wMmYyNGY0M2E5NzU0MmQzODcyMGMxOWI3NzM1ZGI2OCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZjZjZGY1Yjg2ZDYxNGM4ZGE3Mjc0MDU0MGQzYjE5YzEgPSAkKGA8ZGl2IGlkPSJodG1sX2Y2Y2RmNWI4NmQ2MTRjOGRhNzI3NDA1NDBkM2IxOWMxIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UaGUgQmVhY2hlcywgRWFzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzAyZjI0ZjQzYTk3NTQyZDM4NzIwYzE5Yjc3MzVkYjY4LnNldENvbnRlbnQoaHRtbF9mNmNkZjViODZkNjE0YzhkYTcyNzQwNTQwZDNiMTljMSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNTUwYTU4MzZmMTEwNDQ1NDlkZGFiMWU4ZDFiZmU1YzIuYmluZFBvcHVwKHBvcHVwXzAyZjI0ZjQzYTk3NTQyZDM4NzIwYzE5Yjc3MzVkYjY4KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9kYTU1YjBmM2EyNmU0N2FkYWY1MTE2YjhkZTJhZGFlNCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcwOTA2MDQsIC03OS4zNjM0NTE3XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2M0Y2JjOWI2NjhmNzQ3MWE5Yzk2YzU4ODRlNTQ4ZDViID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9iNDBhNDJjMDI3MDA0MWNlYmU0MzcwZmIxYWFlZWQ3NSA9ICQoYDxkaXYgaWQ9Imh0bWxfYjQwYTQyYzAyNzAwNDFjZWJlNDM3MGZiMWFhZWVkNzUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkxlYXNpZGUsIEVhc3QgWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9jNGNiYzliNjY4Zjc0NzFhOWM5NmM1ODg0ZTU0OGQ1Yi5zZXRDb250ZW50KGh0bWxfYjQwYTQyYzAyNzAwNDFjZWJlNDM3MGZiMWFhZWVkNzUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2RhNTViMGYzYTI2ZTQ3YWRhZjUxMTZiOGRlMmFkYWU0LmJpbmRQb3B1cChwb3B1cF9jNGNiYzliNjY4Zjc0NzFhOWM5NmM1ODg0ZTU0OGQ1YikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZDQzZWExNDFjZGVlNGFiNjhjMTc1ZWYwZjRjNGFiZjAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MDUzNjg5LCAtNzkuMzQ5MzcxOTAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNjA4NWM3YjJlOTE3NDRkODhjY2NjZGM3ZmVmZmRmMjYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQ5YzA1ZmYwNWVlMzRiNzA4ZDU3ZjM4OWU2ZWI1MTMyID0gJChgPGRpdiBpZD0iaHRtbF80OWMwNWZmMDVlZTM0YjcwOGQ1N2YzODllNmViNTEzMiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+VGhvcm5jbGlmZmUgUGFyaywgRWFzdCBZb3JrPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzYwODVjN2IyZTkxNzQ0ZDg4Y2NjY2RjN2ZlZmZkZjI2LnNldENvbnRlbnQoaHRtbF80OWMwNWZmMDVlZTM0YjcwOGQ1N2YzODllNmViNTEzMik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZDQzZWExNDFjZGVlNGFiNjhjMTc1ZWYwZjRjNGFiZjAuYmluZFBvcHVwKHBvcHVwXzYwODVjN2IyZTkxNzQ0ZDg4Y2NjY2RjN2ZlZmZkZjI2KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80ZDllOWFkODVkNmY0MDc1ODdmOTc4Zjc1M2Q2YzMwYyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY4NTM0NywgLTc5LjMzODEwNjVdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfN2QwYzA5MmMxYjNhNGFkODkyZjYxN2VmYTdjN2Q4ZDUgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzc5ODk3ZTE5ZjM1NzQ5N2ZhOWY5ZDNlNjE1NGZiY2Q0ID0gJChgPGRpdiBpZD0iaHRtbF83OTg5N2UxOWYzNTc0OTdmYTlmOWQzZTYxNTRmYmNkNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RWFzdCBUb3JvbnRvLCBFYXN0IFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfN2QwYzA5MmMxYjNhNGFkODkyZjYxN2VmYTdjN2Q4ZDUuc2V0Q29udGVudChodG1sXzc5ODk3ZTE5ZjM1NzQ5N2ZhOWY5ZDNlNjE1NGZiY2Q0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl80ZDllOWFkODVkNmY0MDc1ODdmOTc4Zjc1M2Q2YzMwYy5iaW5kUG9wdXAocG9wdXBfN2QwYzA5MmMxYjNhNGFkODkyZjYxN2VmYTdjN2Q4ZDUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2I4NDZiOWY2YjE5YTQ1NWM5NGRlZGU5MzNmZmYwYWEwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjc5NTU3MSwgLTc5LjM1MjE4OF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF81MjU4NzY4MGE1YzQ0MzIwYWJjMTQyMmQ3ZDNlZTRhMSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZWQyOTExM2E5MDA3NDFkYmI4MDQ2OTQ0YTU1ZGRlOTkgPSAkKGA8ZGl2IGlkPSJodG1sX2VkMjkxMTNhOTAwNzQxZGJiODA0Njk0NGE1NWRkZTk5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UaGUgRGFuZm9ydGggV2VzdCxSaXZlcmRhbGUsIEVhc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81MjU4NzY4MGE1YzQ0MzIwYWJjMTQyMmQ3ZDNlZTRhMS5zZXRDb250ZW50KGh0bWxfZWQyOTExM2E5MDA3NDFkYmI4MDQ2OTQ0YTU1ZGRlOTkpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2I4NDZiOWY2YjE5YTQ1NWM5NGRlZGU5MzNmZmYwYWEwLmJpbmRQb3B1cChwb3B1cF81MjU4NzY4MGE1YzQ0MzIwYWJjMTQyMmQ3ZDNlZTRhMSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZmMxMjM3YmZiMDRhNGZiZWI0NzcxOTk1MWZkYTk0OWMgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Njg5OTg1LCAtNzkuMzE1NTcxNTk5OTk5OThdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZGM2Y2YxOGZkZWQ5NGNlOWFmMGQ2ZDM5ZDBiYzNhZjcgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzU5OTdkZjg3N2ZlYjRiNjViZmUyNjE5NWQ0ZThjZDMzID0gJChgPGRpdiBpZD0iaHRtbF81OTk3ZGY4NzdmZWI0YjY1YmZlMjYxOTVkNGU4Y2QzMyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+VGhlIEJlYWNoZXMgV2VzdCxJbmRpYSBCYXphYXIsIEVhc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9kYzZjZjE4ZmRlZDk0Y2U5YWYwZDZkMzlkMGJjM2FmNy5zZXRDb250ZW50KGh0bWxfNTk5N2RmODc3ZmViNGI2NWJmZTI2MTk1ZDRlOGNkMzMpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2ZjMTIzN2JmYjA0YTRmYmViNDc3MTk5NTFmZGE5NDljLmJpbmRQb3B1cChwb3B1cF9kYzZjZjE4ZmRlZDk0Y2U5YWYwZDZkMzlkMGJjM2FmNykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODcwYjY3MjQ4MDllNDBmOGJkMWVhZmI1NTFhMTVlYWEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTk1MjU1LCAtNzkuMzQwOTIzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzM2OTc0ZGMxY2IxMDQxNDRhOTIwNjkwZTM3NmI4N2U2ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83MTQzYjUyZmNiNDc0ZGNhOWUyMWRkNWMwMTAyMzRhMiA9ICQoYDxkaXYgaWQ9Imh0bWxfNzE0M2I1MmZjYjQ3NGRjYTllMjFkZDVjMDEwMjM0YTIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlN0dWRpbyBEaXN0cmljdCwgRWFzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzM2OTc0ZGMxY2IxMDQxNDRhOTIwNjkwZTM3NmI4N2U2LnNldENvbnRlbnQoaHRtbF83MTQzYjUyZmNiNDc0ZGNhOWUyMWRkNWMwMTAyMzRhMik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfODcwYjY3MjQ4MDllNDBmOGJkMWVhZmI1NTFhMTVlYWEuYmluZFBvcHVwKHBvcHVwXzM2OTc0ZGMxY2IxMDQxNDRhOTIwNjkwZTM3NmI4N2U2KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl85NWNmZTM2OGQ5YTY0NzczOWNlMDNjMjFkZGE1NzgzNyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcyODAyMDUsIC03OS4zODg3OTAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2JjM2MwZTkzODA4MDQxMGM4Y2ZmNjU5MjI3NzI1OWI1ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF82ODdjNTBhNWQ0Mzg0ZGNhYTQwMGYxNTFiMjJhZGJkNiA9ICQoYDxkaXYgaWQ9Imh0bWxfNjg3YzUwYTVkNDM4NGRjYWE0MDBmMTUxYjIyYWRiZDYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkxhd3JlbmNlIFBhcmssIENlbnRyYWwgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9iYzNjMGU5MzgwODA0MTBjOGNmZjY1OTIyNzcyNTliNS5zZXRDb250ZW50KGh0bWxfNjg3YzUwYTVkNDM4NGRjYWE0MDBmMTUxYjIyYWRiZDYpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzk1Y2ZlMzY4ZDlhNjQ3NzM5Y2UwM2MyMWRkYTU3ODM3LmJpbmRQb3B1cChwb3B1cF9iYzNjMGU5MzgwODA0MTBjOGNmZjY1OTIyNzcyNTliNSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNzBjZDdjZjgzYjdiNGVhZGFmNDUzNDc4M2Q3MWUyZjAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MTI3NTExLCAtNzkuMzkwMTk3NV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9kZGQ0N2FjZDFlZmM0ODAwYTVlY2FhNzE0NjI2NWZlMiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfODc3MjJlZGQ3ZGJlNDNmODk5ZWNjMjlkOTMyZGZiOGYgPSAkKGA8ZGl2IGlkPSJodG1sXzg3NzIyZWRkN2RiZTQzZjg5OWVjYzI5ZDkzMmRmYjhmIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5EYXZpc3ZpbGxlIE5vcnRoLCBDZW50cmFsIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfZGRkNDdhY2QxZWZjNDgwMGE1ZWNhYTcxNDYyNjVmZTIuc2V0Q29udGVudChodG1sXzg3NzIyZWRkN2RiZTQzZjg5OWVjYzI5ZDkzMmRmYjhmKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl83MGNkN2NmODNiN2I0ZWFkYWY0NTM0NzgzZDcxZTJmMC5iaW5kUG9wdXAocG9wdXBfZGRkNDdhY2QxZWZjNDgwMGE1ZWNhYTcxNDYyNjVmZTIpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzRkZDg3MjlkNmIyNzQ3YTNhZWU0MWYyOGE2NGYwOTIyID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzE1MzgzNCwgLTc5LjQwNTY3ODQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2RjMjg1OWY3ODI3MzQ3YzRhNGUwYjdjNzM4ZDIzODc1ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF80MjdmMGI4ZTZmMjA0NTU5OTNlNTMwZDZhOGZjNmVjZSA9ICQoYDxkaXYgaWQ9Imh0bWxfNDI3ZjBiOGU2ZjIwNDU1OTkzZTUzMGQ2YThmYzZlY2UiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk5vcnRoIFRvcm9udG8gV2VzdCwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2RjMjg1OWY3ODI3MzQ3YzRhNGUwYjdjNzM4ZDIzODc1LnNldENvbnRlbnQoaHRtbF80MjdmMGI4ZTZmMjA0NTU5OTNlNTMwZDZhOGZjNmVjZSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNGRkODcyOWQ2YjI3NDdhM2FlZTQxZjI4YTY0ZjA5MjIuYmluZFBvcHVwKHBvcHVwX2RjMjg1OWY3ODI3MzQ3YzRhNGUwYjdjNzM4ZDIzODc1KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8xMmRmNmI2MmI4ZDE0OGZmYmI5YjBjN2Y4ZWEwZDM2OCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcwNDMyNDQsIC03OS4zODg3OTAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2E5MzVjZTgyZjY5ZTRhNWM4ZGViNWI0YWM2NjNmZTgwID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8yZGM2MDVjMTExYWQ0OWNhODRjNDJkM2Q2ZjM4YWI1OCA9ICQoYDxkaXYgaWQ9Imh0bWxfMmRjNjA1YzExMWFkNDljYTg0YzQyZDNkNmYzOGFiNTgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkRhdmlzdmlsbGUsIENlbnRyYWwgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9hOTM1Y2U4MmY2OWU0YTVjOGRlYjViNGFjNjYzZmU4MC5zZXRDb250ZW50KGh0bWxfMmRjNjA1YzExMWFkNDljYTg0YzQyZDNkNmYzOGFiNTgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzEyZGY2YjYyYjhkMTQ4ZmZiYjliMGM3ZjhlYTBkMzY4LmJpbmRQb3B1cChwb3B1cF9hOTM1Y2U4MmY2OWU0YTVjOGRlYjViNGFjNjYzZmU4MCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMWMyODI2ZDRjN2ZlNDNjYWJhZjM4ZmVjMzEwNjNmYjEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42ODk1NzQzLCAtNzkuMzgzMTU5OTAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZGExNDc5OTUzM2VjNGE4ZWI4OTZmZDZhZjRmNzE0ZTYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzdiMTdjOTIwMzNhZjRiNTQ4MWY4NjdkNmQ5YjVhYmQxID0gJChgPGRpdiBpZD0iaHRtbF83YjE3YzkyMDMzYWY0YjU0ODFmODY3ZDZkOWI1YWJkMSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TW9vcmUgUGFyayxTdW1tZXJoaWxsIEVhc3QsIENlbnRyYWwgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9kYTE0Nzk5NTMzZWM0YThlYjg5NmZkNmFmNGY3MTRlNi5zZXRDb250ZW50KGh0bWxfN2IxN2M5MjAzM2FmNGI1NDgxZjg2N2Q2ZDliNWFiZDEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzFjMjgyNmQ0YzdmZTQzY2FiYWYzOGZlYzMxMDYzZmIxLmJpbmRQb3B1cChwb3B1cF9kYTE0Nzk5NTMzZWM0YThlYjg5NmZkNmFmNGY3MTRlNikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYzdhZDg1MmQxYjAxNGMwOWIxOTY4ZmUyNGNmY2JiYTIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42ODY0MTIyOTk5OTk5OSwgLTc5LjQwMDA0OTNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZmQ4Nzc3NTc0NTJlNGVkZmEzODhmOGFjNzdmNGIzMWQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzZhYTQ5MzgxMDY3NTQzNWRhOGYxMTE0ZTgyNTZiODRiID0gJChgPGRpdiBpZD0iaHRtbF82YWE0OTM4MTA2NzU0MzVkYThmMTExNGU4MjU2Yjg0YiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGVlciBQYXJrLEZvcmVzdCBIaWxsIFNFLFJhdGhuZWxseSxTb3V0aCBIaWxsLFN1bW1lcmhpbGwgV2VzdCwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2ZkODc3NzU3NDUyZTRlZGZhMzg4ZjhhYzc3ZjRiMzFkLnNldENvbnRlbnQoaHRtbF82YWE0OTM4MTA2NzU0MzVkYThmMTExNGU4MjU2Yjg0Yik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYzdhZDg1MmQxYjAxNGMwOWIxOTY4ZmUyNGNmY2JiYTIuYmluZFBvcHVwKHBvcHVwX2ZkODc3NzU3NDUyZTRlZGZhMzg4ZjhhYzc3ZjRiMzFkKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9jM2Q3Yjk3ZDllMzg0MjZiYjZiMTI5Y2VhZjZjYzVjNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY3OTU2MjYsIC03OS4zNzc1Mjk0MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8xNzc0MzY0YzhjMjQ0ZThjOGRhY2Y4ZDExYzYyMDJjZSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNjU3NTRjZjg5NWY2NDRkNGJmNDU4ZTk5ODJjZWM2MjggPSAkKGA8ZGl2IGlkPSJodG1sXzY1NzU0Y2Y4OTVmNjQ0ZDRiZjQ1OGU5OTgyY2VjNjI4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Sb3NlZGFsZSwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8xNzc0MzY0YzhjMjQ0ZThjOGRhY2Y4ZDExYzYyMDJjZS5zZXRDb250ZW50KGh0bWxfNjU3NTRjZjg5NWY2NDRkNGJmNDU4ZTk5ODJjZWM2MjgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2MzZDdiOTdkOWUzODQyNmJiNmIxMjljZWFmNmNjNWM2LmJpbmRQb3B1cChwb3B1cF8xNzc0MzY0YzhjMjQ0ZThjOGRhY2Y4ZDExYzYyMDJjZSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNDQ1NGQyOGQzODVjNGIyMzlkOTk3NGNmMzg0MmVkNTggPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Njc5NjcsIC03OS4zNjc2NzUzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzNkZTA5NWUwOTliNTQ0ZDI4OTE1YzQ4MmNhM2FlNWNiID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9mMjZlZDg0OGYyYmM0NWEwODEzZTlkNTZlMzU4M2QyYSA9ICQoYDxkaXYgaWQ9Imh0bWxfZjI2ZWQ4NDhmMmJjNDVhMDgxM2U5ZDU2ZTM1ODNkMmEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhYmJhZ2V0b3duLFN0LiBKYW1lcyBUb3duLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzNkZTA5NWUwOTliNTQ0ZDI4OTE1YzQ4MmNhM2FlNWNiLnNldENvbnRlbnQoaHRtbF9mMjZlZDg0OGYyYmM0NWEwODEzZTlkNTZlMzU4M2QyYSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNDQ1NGQyOGQzODVjNGIyMzlkOTk3NGNmMzg0MmVkNTguYmluZFBvcHVwKHBvcHVwXzNkZTA5NWUwOTliNTQ0ZDI4OTE1YzQ4MmNhM2FlNWNiKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mMjk4NmQwNzcwZjQ0MjMyYTM0YzRjMGYwYjcyNDQ0ZCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2NTg1OTksIC03OS4zODMxNTk5MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9lYTU2ODQ2NTQzYmI0MDIzYWFhM2Y1MTEwYTM0OGY5MSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfOTNmYjdkNmZhOTZhNDA0MmJjODcyMjI4YmJjMThmODAgPSAkKGA8ZGl2IGlkPSJodG1sXzkzZmI3ZDZmYTk2YTQwNDJiYzg3MjIyOGJiYzE4ZjgwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DaHVyY2ggYW5kIFdlbGxlc2xleSwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9lYTU2ODQ2NTQzYmI0MDIzYWFhM2Y1MTEwYTM0OGY5MS5zZXRDb250ZW50KGh0bWxfOTNmYjdkNmZhOTZhNDA0MmJjODcyMjI4YmJjMThmODApOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2YyOTg2ZDA3NzBmNDQyMzJhMzRjNGMwZjBiNzI0NDRkLmJpbmRQb3B1cChwb3B1cF9lYTU2ODQ2NTQzYmI0MDIzYWFhM2Y1MTEwYTM0OGY5MSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNWZkMWRkNDNkZWM0NGViZDhlNjQyNWNjYmQxM2Q5OWIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTQyNTk5LCAtNzkuMzYwNjM1OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9jZWQ1NTZlNzU0NjE0NjMxYjhkN2M5Y2YyNWViMzZjNiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMzdiZGFlYTEwNjY3NGEzZWIzOWM0Y2UyZTM4OGIyZTEgPSAkKGA8ZGl2IGlkPSJodG1sXzM3YmRhZWExMDY2NzRhM2ViMzljNGNlMmUzODhiMmUxIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IYXJib3VyZnJvbnQsUmVnZW50IFBhcmssIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfY2VkNTU2ZTc1NDYxNDYzMWI4ZDdjOWNmMjVlYjM2YzYuc2V0Q29udGVudChodG1sXzM3YmRhZWExMDY2NzRhM2ViMzljNGNlMmUzODhiMmUxKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl81ZmQxZGQ0M2RlYzQ0ZWJkOGU2NDI1Y2NiZDEzZDk5Yi5iaW5kUG9wdXAocG9wdXBfY2VkNTU2ZTc1NDYxNDYzMWI4ZDdjOWNmMjVlYjM2YzYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2EzNzczYTc5YjNkMzQ4M2U5NDQ5MjNkYzk0YTU4ZTc1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjU3MTYxOCwgLTc5LjM3ODkzNzA5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2U4NjYwNzRhOTU3YTRkZjI5OTgyMTY2OGYxYTAxOGM0ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9mMmMxMWRhZmI3ZTQ0ODUwYjJmZWVmNmI0Yjg2ZDJhOCA9ICQoYDxkaXYgaWQ9Imh0bWxfZjJjMTFkYWZiN2U0NDg1MGIyZmVlZjZiNGI4NmQyYTgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJ5ZXJzb24sR2FyZGVuIERpc3RyaWN0LCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2U4NjYwNzRhOTU3YTRkZjI5OTgyMTY2OGYxYTAxOGM0LnNldENvbnRlbnQoaHRtbF9mMmMxMWRhZmI3ZTQ0ODUwYjJmZWVmNmI0Yjg2ZDJhOCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYTM3NzNhNzliM2QzNDgzZTk0NDkyM2RjOTRhNThlNzUuYmluZFBvcHVwKHBvcHVwX2U4NjYwNzRhOTU3YTRkZjI5OTgyMTY2OGYxYTAxOGM0KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8xMDcxNmMyZTFmYjY0NWM1OTYwYTk3NzI0ODk2MGJiYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1MTQ5MzksIC03OS4zNzU0MTc5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzY5YWY4NDdmNTMxNjQxZjVhYjk0NGNjNGM2NDNiZmU1ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF80NjM0MzRkMWUxOTE0ODg3YmNkMzVmYzI5MWIzNDAwZCA9ICQoYDxkaXYgaWQ9Imh0bWxfNDYzNDM0ZDFlMTkxNDg4N2JjZDM1ZmMyOTFiMzQwMGQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlN0LiBKYW1lcyBUb3duLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzY5YWY4NDdmNTMxNjQxZjVhYjk0NGNjNGM2NDNiZmU1LnNldENvbnRlbnQoaHRtbF80NjM0MzRkMWUxOTE0ODg3YmNkMzVmYzI5MWIzNDAwZCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMTA3MTZjMmUxZmI2NDVjNTk2MGE5NzcyNDg5NjBiYmIuYmluZFBvcHVwKHBvcHVwXzY5YWY4NDdmNTMxNjQxZjVhYjk0NGNjNGM2NDNiZmU1KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9kMzZlMjg0ZTE1ZDM0NWUxYTI3YmNiZTQxZTc2YjNlYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0NDc3MDc5OTk5OTk5NiwgLTc5LjM3MzMwNjRdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNWM1MzUxZDJlOTVmNDI4MzllMGM5ZTllY2UzNjk2M2UgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2Q5MTAxZGQ2NDBmNjQ3NDVhZTMxODI0YzM0OTNiNWFiID0gJChgPGRpdiBpZD0iaHRtbF9kOTEwMWRkNjQwZjY0NzQ1YWUzMTgyNGMzNDkzYjVhYiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QmVyY3p5IFBhcmssIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNWM1MzUxZDJlOTVmNDI4MzllMGM5ZTllY2UzNjk2M2Uuc2V0Q29udGVudChodG1sX2Q5MTAxZGQ2NDBmNjQ3NDVhZTMxODI0YzM0OTNiNWFiKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9kMzZlMjg0ZTE1ZDM0NWUxYTI3YmNiZTQxZTc2YjNlYi5iaW5kUG9wdXAocG9wdXBfNWM1MzUxZDJlOTVmNDI4MzllMGM5ZTllY2UzNjk2M2UpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2Y5YzA0ZjlkYzA3ZTRlNzQ5MTY3MzNmM2IxYThmOGQxID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjU3OTUyNCwgLTc5LjM4NzM4MjZdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZTU3YWY2ZjZjZDQxNDExMDg2OGVkOTBmNTBhMjQzMGEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzA2ZDgyNjk5MmFkYTQ5OWQ5MGZkMmZiMDE3NGU5MDc5ID0gJChgPGRpdiBpZD0iaHRtbF8wNmQ4MjY5OTJhZGE0OTlkOTBmZDJmYjAxNzRlOTA3OSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2VudHJhbCBCYXkgU3RyZWV0LCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2U1N2FmNmY2Y2Q0MTQxMTA4NjhlZDkwZjUwYTI0MzBhLnNldENvbnRlbnQoaHRtbF8wNmQ4MjY5OTJhZGE0OTlkOTBmZDJmYjAxNzRlOTA3OSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZjljMDRmOWRjMDdlNGU3NDkxNjczM2YzYjFhOGY4ZDEuYmluZFBvcHVwKHBvcHVwX2U1N2FmNmY2Y2Q0MTQxMTA4NjhlZDkwZjUwYTI0MzBhKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8zZDY0NTcyZDVjMDU0ZTliOWI0MDRiMWU1OThiMzY0NSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1MDU3MTIwMDAwMDAxLCAtNzkuMzg0NTY3NV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF85NGVmZDgxOWI1MTk0ODVjOTZjZTAzN2VhODYwNDMxMiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfOTRjM2Y2OWRiMGMzNDBjMTlhNjMyOThlNTRlYmQ2M2MgPSAkKGA8ZGl2IGlkPSJodG1sXzk0YzNmNjlkYjBjMzQwYzE5YTYzMjk4ZTU0ZWJkNjNjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5BZGVsYWlkZSxLaW5nLFJpY2htb25kLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzk0ZWZkODE5YjUxOTQ4NWM5NmNlMDM3ZWE4NjA0MzEyLnNldENvbnRlbnQoaHRtbF85NGMzZjY5ZGIwYzM0MGMxOWE2MzI5OGU1NGViZDYzYyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfM2Q2NDU3MmQ1YzA1NGU5YjliNDA0YjFlNTk4YjM2NDUuYmluZFBvcHVwKHBvcHVwXzk0ZWZkODE5YjUxOTQ4NWM5NmNlMDM3ZWE4NjA0MzEyKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80NjQxNzJlZGY4MDM0YWQ2OTFhNGVkNzc1OTRiMzkzMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0MDgxNTcsIC03OS4zODE3NTIyOTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9hNGVkNDQ2YjU5MTM0MjQ2YWYxN2JhZjljMjJiNjQ0MiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNzdlNGFlYjhiNGM4NDJmMTljODJjNzZiN2ExNDkxNzkgPSAkKGA8ZGl2IGlkPSJodG1sXzc3ZTRhZWI4YjRjODQyZjE5YzgyYzc2YjdhMTQ5MTc5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IYXJib3VyZnJvbnQgRWFzdCxUb3JvbnRvIElzbGFuZHMsVW5pb24gU3RhdGlvbiwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9hNGVkNDQ2YjU5MTM0MjQ2YWYxN2JhZjljMjJiNjQ0Mi5zZXRDb250ZW50KGh0bWxfNzdlNGFlYjhiNGM4NDJmMTljODJjNzZiN2ExNDkxNzkpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzQ2NDE3MmVkZjgwMzRhZDY5MWE0ZWQ3NzU5NGIzOTMyLmJpbmRQb3B1cChwb3B1cF9hNGVkNDQ2YjU5MTM0MjQ2YWYxN2JhZjljMjJiNjQ0MikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzJlM2M2MTExZjlmNDI0NThlZjQ5MmQ5ZDRlZmJiYWYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDcxNzY4LCAtNzkuMzgxNTc2NDAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMjUyZjExYTc4MWYwNGYwN2JkMDk5MjM1Yzg5Y2QzZjIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2ZjNmIyNzk0YmM2MDQ5MzRhN2ZmNDVmODMyNjNhMjY1ID0gJChgPGRpdiBpZD0iaHRtbF9mYzZiMjc5NGJjNjA0OTM0YTdmZjQ1ZjgzMjYzYTI2NSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGVzaWduIEV4Y2hhbmdlLFRvcm9udG8gRG9taW5pb24gQ2VudHJlLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzI1MmYxMWE3ODFmMDRmMDdiZDA5OTIzNWM4OWNkM2YyLnNldENvbnRlbnQoaHRtbF9mYzZiMjc5NGJjNjA0OTM0YTdmZjQ1ZjgzMjYzYTI2NSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMzJlM2M2MTExZjlmNDI0NThlZjQ5MmQ5ZDRlZmJiYWYuYmluZFBvcHVwKHBvcHVwXzI1MmYxMWE3ODFmMDRmMDdiZDA5OTIzNWM4OWNkM2YyKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9kZDFmNTYxOTJhZjc0OWI5YWNjYTAwM2FmYTE3MDYxMyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0ODE5ODUsIC03OS4zNzk4MTY5MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8xZTZiMWFiYzk0YzM0ZjczYTQzMWY3NGNkNTEyMDRiMCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfN2ViYTAxZTFmNjE1NDk1ODk1YWU2ZjI2ZjM2YWQxYTkgPSAkKGA8ZGl2IGlkPSJodG1sXzdlYmEwMWUxZjYxNTQ5NTg5NWFlNmYyNmYzNmFkMWE5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Db21tZXJjZSBDb3VydCxWaWN0b3JpYSBIb3RlbCwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8xZTZiMWFiYzk0YzM0ZjczYTQzMWY3NGNkNTEyMDRiMC5zZXRDb250ZW50KGh0bWxfN2ViYTAxZTFmNjE1NDk1ODk1YWU2ZjI2ZjM2YWQxYTkpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2RkMWY1NjE5MmFmNzQ5YjlhY2NhMDAzYWZhMTcwNjEzLmJpbmRQb3B1cChwb3B1cF8xZTZiMWFiYzk0YzM0ZjczYTQzMWY3NGNkNTEyMDRiMCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzQyZGJhYzhiOGI0NGEyYWE4ZjBhYzZlZGY0MGVjZWEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MzMyODI1LCAtNzkuNDE5NzQ5N10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF83NzNjMjY5Mjc0YzE0MTkwODdjY2RlMGU1YzQ4OTM4MyA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNWUyYzViYWFhODRhNDE3ZjliZGU5OWE2OTE1ZDdmNTIgPSAkKGA8ZGl2IGlkPSJodG1sXzVlMmM1YmFhYTg0YTQxN2Y5YmRlOTlhNjkxNWQ3ZjUyIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CZWRmb3JkIFBhcmssTGF3cmVuY2UgTWFub3IgRWFzdCwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83NzNjMjY5Mjc0YzE0MTkwODdjY2RlMGU1YzQ4OTM4My5zZXRDb250ZW50KGh0bWxfNWUyYzViYWFhODRhNDE3ZjliZGU5OWE2OTE1ZDdmNTIpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzM0MmRiYWM4YjhiNDRhMmFhOGYwYWM2ZWRmNDBlY2VhLmJpbmRQb3B1cChwb3B1cF83NzNjMjY5Mjc0YzE0MTkwODdjY2RlMGU1YzQ4OTM4MykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMmQ0NGU2NzRhZTZiNDkxZmJkYjdiMmYzYWM4ZjZhZTEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MTE2OTQ4LCAtNzkuNDE2OTM1NTk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNGUwOTRkYWUwYzdhNDIzOTgzNjFmNDRjMzVkZmUzYjQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2E3N2Y3M2U0NjNhZTRmN2E5MDNmYTFkNTllZTYzMjY2ID0gJChgPGRpdiBpZD0iaHRtbF9hNzdmNzNlNDYzYWU0ZjdhOTAzZmExZDU5ZWU2MzI2NiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Um9zZWxhd24sIENlbnRyYWwgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF80ZTA5NGRhZTBjN2E0MjM5ODM2MWY0NGMzNWRmZTNiNC5zZXRDb250ZW50KGh0bWxfYTc3ZjczZTQ2M2FlNGY3YTkwM2ZhMWQ1OWVlNjMyNjYpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzJkNDRlNjc0YWU2YjQ5MWZiZGI3YjJmM2FjOGY2YWUxLmJpbmRQb3B1cChwb3B1cF80ZTA5NGRhZTBjN2E0MjM5ODM2MWY0NGMzNWRmZTNiNCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzcyMTkzNDU5YjU4NGI5ZmI3YmQxODc5ZTA4MDEwZGQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42OTY5NDc2LCAtNzkuNDExMzA3MjAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZGQ0OWJiYmVhZTFiNDVhNWE3OWNkZTBjMjEwYjRlMWEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzE4NjFhNzU0YjEyMzRlYTA4MjkzNWNlYjNlZjg1YTlkID0gJChgPGRpdiBpZD0iaHRtbF8xODYxYTc1NGIxMjM0ZWEwODI5MzVjZWIzZWY4NWE5ZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Rm9yZXN0IEhpbGwgTm9ydGgsRm9yZXN0IEhpbGwgV2VzdCwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2RkNDliYmJlYWUxYjQ1YTVhNzljZGUwYzIxMGI0ZTFhLnNldENvbnRlbnQoaHRtbF8xODYxYTc1NGIxMjM0ZWEwODI5MzVjZWIzZWY4NWE5ZCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMzcyMTkzNDU5YjU4NGI5ZmI3YmQxODc5ZTA4MDEwZGQuYmluZFBvcHVwKHBvcHVwX2RkNDliYmJlYWUxYjQ1YTVhNzljZGUwYzIxMGI0ZTFhKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mMGIwNDQ2ZDkxNjU0YTczYjM2MDRmNjc3ZTYyZTk4MiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY3MjcwOTcsIC03OS40MDU2Nzg0MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8zYmYzZWJhYmUyZWY0N2JkOTU0MzY3NmMyMmU0ZjkwZCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMDA4NmIzZmM0YjNkNDRmYjgyY2JiOTg2MTU3M2VlMWMgPSAkKGA8ZGl2IGlkPSJodG1sXzAwODZiM2ZjNGIzZDQ0ZmI4MmNiYjk4NjE1NzNlZTFjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UaGUgQW5uZXgsTm9ydGggTWlkdG93bixZb3JrdmlsbGUsIENlbnRyYWwgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8zYmYzZWJhYmUyZWY0N2JkOTU0MzY3NmMyMmU0ZjkwZC5zZXRDb250ZW50KGh0bWxfMDA4NmIzZmM0YjNkNDRmYjgyY2JiOTg2MTU3M2VlMWMpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2YwYjA0NDZkOTE2NTRhNzNiMzYwNGY2NzdlNjJlOTgyLmJpbmRQb3B1cChwb3B1cF8zYmYzZWJhYmUyZWY0N2JkOTU0MzY3NmMyMmU0ZjkwZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZTQzNDc2OWI2Yzk0NDIxNmFjMWQ2OGZlMzBiNGFjYzIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjI2OTU2LCAtNzkuNDAwMDQ5M10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9lMjg3ODQ3ZjNlMjY0NWQ2YjZiYTRkNmM2ODdkZjgwMCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNDgzMzgwMmY0ODdkNDY3ZmI4Y2UyMzZkOGU5NjM1MTggPSAkKGA8ZGl2IGlkPSJodG1sXzQ4MzM4MDJmNDg3ZDQ2N2ZiOGNlMjM2ZDhlOTYzNTE4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IYXJib3JkLFVuaXZlcnNpdHkgb2YgVG9yb250bywgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9lMjg3ODQ3ZjNlMjY0NWQ2YjZiYTRkNmM2ODdkZjgwMC5zZXRDb250ZW50KGh0bWxfNDgzMzgwMmY0ODdkNDY3ZmI4Y2UyMzZkOGU5NjM1MTgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2U0MzQ3NjliNmM5NDQyMTZhYzFkNjhmZTMwYjRhY2MyLmJpbmRQb3B1cChwb3B1cF9lMjg3ODQ3ZjNlMjY0NWQ2YjZiYTRkNmM2ODdkZjgwMCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfY2U0ODE0OGQ0MDJhNGEyMjk5M2NhMmI0MDEwNTZiMzAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTMyMDU3LCAtNzkuNDAwMDQ5M10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF80ZTIyMjJmNzc0NTE0NDYxODEwOGEzMjM1OTY0ZWVlZiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMGJhYTY3OWU5OGM1NDYxN2I0NGMwMjIyMzIwOTdlNDAgPSAkKGA8ZGl2IGlkPSJodG1sXzBiYWE2NzllOThjNTQ2MTdiNDRjMDIyMjMyMDk3ZTQwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DaGluYXRvd24sR3JhbmdlIFBhcmssS2Vuc2luZ3RvbiBNYXJrZXQsIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNGUyMjIyZjc3NDUxNDQ2MTgxMDhhMzIzNTk2NGVlZWYuc2V0Q29udGVudChodG1sXzBiYWE2NzllOThjNTQ2MTdiNDRjMDIyMjMyMDk3ZTQwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9jZTQ4MTQ4ZDQwMmE0YTIyOTkzY2EyYjQwMTA1NmIzMC5iaW5kUG9wdXAocG9wdXBfNGUyMjIyZjc3NDUxNDQ2MTgxMDhhMzIzNTk2NGVlZWYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2RiYjMwNTk5ODAxZDRkYjBiZTA4NmY4MjdhM2YyMDgyID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjI4OTQ2NywgLTc5LjM5NDQxOTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfOTg5NDA4MjNiOTQ0NDE2MWIwM2IzNGI4YTNiNGQ0NzYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzliNTA5YzQwZDMwMzQyOTY4ZTRhYTJmN2MzNTJlODY5ID0gJChgPGRpdiBpZD0iaHRtbF85YjUwOWM0MGQzMDM0Mjk2OGU0YWEyZjdjMzUyZTg2OSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q04gVG93ZXIsQmF0aHVyc3QgUXVheSxJc2xhbmQgYWlycG9ydCxIYXJib3VyZnJvbnQgV2VzdCxLaW5nIGFuZCBTcGFkaW5hLFJhaWx3YXkgTGFuZHMsU291dGggTmlhZ2FyYSwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF85ODk0MDgyM2I5NDQ0MTYxYjAzYjM0YjhhM2I0ZDQ3Ni5zZXRDb250ZW50KGh0bWxfOWI1MDljNDBkMzAzNDI5NjhlNGFhMmY3YzM1MmU4NjkpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2RiYjMwNTk5ODAxZDRkYjBiZTA4NmY4MjdhM2YyMDgyLmJpbmRQb3B1cChwb3B1cF85ODk0MDgyM2I5NDQ0MTYxYjAzYjM0YjhhM2I0ZDQ3NikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYjc5ZDQzZDEzNjRkNDM2ZjliM2JhNWE2NWZhZjFhYzggPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDY0MzUyLCAtNzkuMzc0ODQ1OTk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNzRkZDA0OTMwNTc0NDJjMjk1ZWU1YWExMjkxYmE5MGEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzRhNDBiMGE1OTQ3YzRlZDg4ZjU0ZmJmMzNmZjQ3N2U4ID0gJChgPGRpdiBpZD0iaHRtbF80YTQwYjBhNTk0N2M0ZWQ4OGY1NGZiZjMzZmY0NzdlOCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+U3RuIEEgUE8gQm94ZXMgMjUgVGhlIEVzcGxhbmFkZSwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83NGRkMDQ5MzA1NzQ0MmMyOTVlZTVhYTEyOTFiYTkwYS5zZXRDb250ZW50KGh0bWxfNGE0MGIwYTU5NDdjNGVkODhmNTRmYmYzM2ZmNDc3ZTgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2I3OWQ0M2QxMzY0ZDQzNmY5YjNiYTVhNjVmYWYxYWM4LmJpbmRQb3B1cChwb3B1cF83NGRkMDQ5MzA1NzQ0MmMyOTVlZTVhYTEyOTFiYTkwYSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZGQ4YzgxYTI5ZTc2NGMxMmI4ZDUyMTdhY2VkNTMwMmQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDg0MjkyLCAtNzkuMzgyMjgwMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8zZTY1NTgzODVmMjM0ZWI3OWU5NTExNzIxNTMzMDQ3YiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYmU0MThiODFhMWY2NDQ4MGIwM2E4NWVkYmVmODY5M2EgPSAkKGA8ZGl2IGlkPSJodG1sX2JlNDE4YjgxYTFmNjQ0ODBiMDNhODVlZGJlZjg2OTNhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5GaXJzdCBDYW5hZGlhbiBQbGFjZSxVbmRlcmdyb3VuZCBjaXR5LCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzNlNjU1ODM4NWYyMzRlYjc5ZTk1MTE3MjE1MzMwNDdiLnNldENvbnRlbnQoaHRtbF9iZTQxOGI4MWExZjY0NDgwYjAzYTg1ZWRiZWY4NjkzYSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZGQ4YzgxYTI5ZTc2NGMxMmI4ZDUyMTdhY2VkNTMwMmQuYmluZFBvcHVwKHBvcHVwXzNlNjU1ODM4NWYyMzRlYjc5ZTk1MTE3MjE1MzMwNDdiKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl83MTIyMjI5M2JlMDA0YzE1OTY3MGZmZDc4NTZkYWM3YyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcxODUxNzk5OTk5OTk5NiwgLTc5LjQ2NDc2MzI5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzQ0ZGI5YTBhMmVmZTQxM2M5YTBhZTdiOGQ4ZDYzY2I3ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9kNWEyYjc4OTc0NzQ0MDI0YTc4YTlmMDVhZjQ1NWY1MCA9ICQoYDxkaXYgaWQ9Imh0bWxfZDVhMmI3ODk3NDc0NDAyNGE3OGE5ZjA1YWY0NTVmNTAiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkxhd3JlbmNlIEhlaWdodHMsTGF3cmVuY2UgTWFub3IsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNDRkYjlhMGEyZWZlNDEzYzlhMGFlN2I4ZDhkNjNjYjcuc2V0Q29udGVudChodG1sX2Q1YTJiNzg5NzQ3NDQwMjRhNzhhOWYwNWFmNDU1ZjUwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl83MTIyMjI5M2JlMDA0YzE1OTY3MGZmZDc4NTZkYWM3Yy5iaW5kUG9wdXAocG9wdXBfNDRkYjlhMGEyZWZlNDEzYzlhMGFlN2I4ZDhkNjNjYjcpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2VhOGEwMjFiMzkyNDQ5OTE5YjJlMTVlNjA5YmFhNjBjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzA5NTc3LCAtNzkuNDQ1MDcyNTk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZDU5ODU3ZjhjYzhlNGJjODg2OGY0OGNjODhjODlhYjQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQ0YTM5MGZhMzQwMTRiYmQ4NmE5NmQ5ODA0ZmVlMzA4ID0gJChgPGRpdiBpZD0iaHRtbF80NGEzOTBmYTM0MDE0YmJkODZhOTZkOTgwNGZlZTMwOCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+R2xlbmNhaXJuLCBOb3J0aCBZb3JrPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2Q1OTg1N2Y4Y2M4ZTRiYzg4NjhmNDhjYzg4Yzg5YWI0LnNldENvbnRlbnQoaHRtbF80NGEzOTBmYTM0MDE0YmJkODZhOTZkOTgwNGZlZTMwOCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZWE4YTAyMWIzOTI0NDk5MTliMmUxNWU2MDliYWE2MGMuYmluZFBvcHVwKHBvcHVwX2Q1OTg1N2Y4Y2M4ZTRiYzg4NjhmNDhjYzg4Yzg5YWI0KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl83ZjNiN2ExYTU1MzA0YzlhOGM2ZTE1MDkxMDhhYTI2NyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY5Mzc4MTMsIC03OS40MjgxOTE0MDAwMDAwMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8zNzE2MDhiODg1Y2Q0NjVhYTdjNmU2ZTYzOGYyMmMwZiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMmU4MjUyYTBiNTc0NGFiNTk5ZTZlNjk2MjEyZGQ1OTAgPSAkKGA8ZGl2IGlkPSJodG1sXzJlODI1MmEwYjU3NDRhYjU5OWU2ZTY5NjIxMmRkNTkwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IdW1ld29vZC1DZWRhcnZhbGUsIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMzcxNjA4Yjg4NWNkNDY1YWE3YzZlNmU2MzhmMjJjMGYuc2V0Q29udGVudChodG1sXzJlODI1MmEwYjU3NDRhYjU5OWU2ZTY5NjIxMmRkNTkwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl83ZjNiN2ExYTU1MzA0YzlhOGM2ZTE1MDkxMDhhYTI2Ny5iaW5kUG9wdXAocG9wdXBfMzcxNjA4Yjg4NWNkNDY1YWE3YzZlNmU2MzhmMjJjMGYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2EwNjVlZjEyOWZiNTQ5YjM5NDA3YjE0NDc4ODMwM2ZkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjg5MDI1NiwgLTc5LjQ1MzUxMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9kNGMzYTU0ZTY2ZWY0ZjM3OGNkODk5NjkxY2FlNDVmMiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNTkyYzZlOTU2MWFjNDY0NDlhM2QzYTU4MjJiNGU0NzAgPSAkKGA8ZGl2IGlkPSJodG1sXzU5MmM2ZTk1NjFhYzQ2NDQ5YTNkM2E1ODIyYjRlNDcwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DYWxlZG9uaWEtRmFpcmJhbmtzLCBZb3JrPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2Q0YzNhNTRlNjZlZjRmMzc4Y2Q4OTk2OTFjYWU0NWYyLnNldENvbnRlbnQoaHRtbF81OTJjNmU5NTYxYWM0NjQ0OWEzZDNhNTgyMmI0ZTQ3MCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYTA2NWVmMTI5ZmI1NDliMzk0MDdiMTQ0Nzg4MzAzZmQuYmluZFBvcHVwKHBvcHVwX2Q0YzNhNTRlNjZlZjRmMzc4Y2Q4OTk2OTFjYWU0NWYyKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl82OGVkNjg3YTY3MDA0NzFmYjkwNGVlMjI5NTZiZTc2MyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2OTU0MiwgLTc5LjQyMjU2MzddLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMjQ3MTc3YTI0MTJlNDExN2FiYzA0YzNkZTgzNjYzZDkgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzBmN2FhMTYzYmY2ZjRlNDE5ZTYyODIwYmJjMDc2M2ExID0gJChgPGRpdiBpZD0iaHRtbF8wZjdhYTE2M2JmNmY0ZTQxOWU2MjgyMGJiYzA3NjNhMSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2hyaXN0aWUsIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMjQ3MTc3YTI0MTJlNDExN2FiYzA0YzNkZTgzNjYzZDkuc2V0Q29udGVudChodG1sXzBmN2FhMTYzYmY2ZjRlNDE5ZTYyODIwYmJjMDc2M2ExKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl82OGVkNjg3YTY3MDA0NzFmYjkwNGVlMjI5NTZiZTc2My5iaW5kUG9wdXAocG9wdXBfMjQ3MTc3YTI0MTJlNDExN2FiYzA0YzNkZTgzNjYzZDkpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzlmZDcxYmQzMDZlYjQzYzhiNWU5ODk4MTVhZDNjZDVjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjY5MDA1MTAwMDAwMDEsIC03OS40NDIyNTkzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzFkMTNlOTEyYmUzNTQxZjVhNjZkZjBjNmIyYzU3N2U2ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF85ZTZlMTA1NWQ4Yzc0OWRlODIwMTZmOGQzMWIzM2IwNiA9ICQoYDxkaXYgaWQ9Imh0bWxfOWU2ZTEwNTVkOGM3NDlkZTgyMDE2ZjhkMzFiMzNiMDYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkRvdmVyY291cnQgVmlsbGFnZSxEdWZmZXJpbiwgV2VzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzFkMTNlOTEyYmUzNTQxZjVhNjZkZjBjNmIyYzU3N2U2LnNldENvbnRlbnQoaHRtbF85ZTZlMTA1NWQ4Yzc0OWRlODIwMTZmOGQzMWIzM2IwNik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfOWZkNzFiZDMwNmViNDNjOGI1ZTk4OTgxNWFkM2NkNWMuYmluZFBvcHVwKHBvcHVwXzFkMTNlOTEyYmUzNTQxZjVhNjZkZjBjNmIyYzU3N2U2KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80ZDdhMzNkZTFjNmI0NzU3YmI5YWJiZjhiNmM2NWVkYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0NzkyNjcwMDAwMDAwNiwgLTc5LjQxOTc0OTddLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNjJjYzM2NzliYzFhNDE5MDk3NjUzNDNlZTg1YWI3MWIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2M0NjhkMTZjMGY1NTQ2MGI5NmM1MmY4OGJjZjljYTZhID0gJChgPGRpdiBpZD0iaHRtbF9jNDY4ZDE2YzBmNTU0NjBiOTZjNTJmODhiY2Y5Y2E2YSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TGl0dGxlIFBvcnR1Z2FsLFRyaW5pdHksIFdlc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF82MmNjMzY3OWJjMWE0MTkwOTc2NTM0M2VlODVhYjcxYi5zZXRDb250ZW50KGh0bWxfYzQ2OGQxNmMwZjU1NDYwYjk2YzUyZjg4YmNmOWNhNmEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzRkN2EzM2RlMWM2YjQ3NTdiYjlhYmJmOGI2YzY1ZWRiLmJpbmRQb3B1cChwb3B1cF82MmNjMzY3OWJjMWE0MTkwOTc2NTM0M2VlODVhYjcxYikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOWZjMzc5ODQ4ZjQyNDA3Yjk5MTQ3ZWRkODdhMDJhODIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42MzY4NDcyLCAtNzkuNDI4MTkxNDAwMDAwMDJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMTM0Mjc0ODdjNmE5NDQ2ODlmMGI0NzUzMDgxNDQ4M2IgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzZjNjkxNDY3OTVhMDRmYzk4NGRiMDk2OGJhNzJlYTc0ID0gJChgPGRpdiBpZD0iaHRtbF82YzY5MTQ2Nzk1YTA0ZmM5ODRkYjA5NjhiYTcyZWE3NCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QnJvY2t0b24sRXhoaWJpdGlvbiBQbGFjZSxQYXJrZGFsZSBWaWxsYWdlLCBXZXN0IFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMTM0Mjc0ODdjNmE5NDQ2ODlmMGI0NzUzMDgxNDQ4M2Iuc2V0Q29udGVudChodG1sXzZjNjkxNDY3OTVhMDRmYzk4NGRiMDk2OGJhNzJlYTc0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl85ZmMzNzk4NDhmNDI0MDdiOTkxNDdlZGQ4N2EwMmE4Mi5iaW5kUG9wdXAocG9wdXBfMTM0Mjc0ODdjNmE5NDQ2ODlmMGI0NzUzMDgxNDQ4M2IpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzY3MDZmMzE4YjY3MDQ3ZmRiOTEzOGRhYjI1Mzg2YzM4ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzEzNzU2MjAwMDAwMDA2LCAtNzkuNDkwMDczOF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF83MGM1MjI3OTVlZDk0OWExYmEzNjc0YjQ5NWIxNzExNSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZjVmYzVlY2FiYTdlNGIwYmFjZDM5NDk2OTEwYTRiNzggPSAkKGA8ZGl2IGlkPSJodG1sX2Y1ZmM1ZWNhYmE3ZTRiMGJhY2QzOTQ5NjkxMGE0Yjc4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Eb3duc3ZpZXcsTm9ydGggUGFyayxVcHdvb2QgUGFyaywgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83MGM1MjI3OTVlZDk0OWExYmEzNjc0YjQ5NWIxNzExNS5zZXRDb250ZW50KGh0bWxfZjVmYzVlY2FiYTdlNGIwYmFjZDM5NDk2OTEwYTRiNzgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzY3MDZmMzE4YjY3MDQ3ZmRiOTEzOGRhYjI1Mzg2YzM4LmJpbmRQb3B1cChwb3B1cF83MGM1MjI3OTVlZDk0OWExYmEzNjc0YjQ5NWIxNzExNSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZTM4NjAzMWIyMTEyNDYyOWFhNmIzODcwNDk3ZjFkNjQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42OTExMTU4LCAtNzkuNDc2MDEzMjk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZTk2YjIxYjNmNTU5NGE3NGFkOTIxZDNjNmNjOTI1MDAgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2RhZTMyZDE2NDYwMDRhOTliYzI0ZGVkYzhjZDhmY2RhID0gJChgPGRpdiBpZD0iaHRtbF9kYWUzMmQxNjQ2MDA0YTk5YmMyNGRlZGM4Y2Q4ZmNkYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGVsIFJheSxLZWVsZXNkYWxlLE1vdW50IERlbm5pcyxTaWx2ZXJ0aG9ybiwgWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9lOTZiMjFiM2Y1NTk0YTc0YWQ5MjFkM2M2Y2M5MjUwMC5zZXRDb250ZW50KGh0bWxfZGFlMzJkMTY0NjAwNGE5OWJjMjRkZWRjOGNkOGZjZGEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2UzODYwMzFiMjExMjQ2MjlhYTZiMzg3MDQ5N2YxZDY0LmJpbmRQb3B1cChwb3B1cF9lOTZiMjFiM2Y1NTk0YTc0YWQ5MjFkM2M2Y2M5MjUwMCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTk2NTg5M2EwNjM4NGI0OGJiNDIwYjhlOGY5NTk2Y2YgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NzMxODUyOTk5OTk5OSwgLTc5LjQ4NzI2MTkwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzY0ZjNlYzc0NTA2NTQwNDliNDA5NTcyZjA1Yjc1YzQxID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9hYjk0YzJhOGZjNmU0MGU5ODBlMjExNzQ4MjVmZmI1NyA9ICQoYDxkaXYgaWQ9Imh0bWxfYWI5NGMyYThmYzZlNDBlOTgwZTIxMTc0ODI1ZmZiNTciIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRoZSBKdW5jdGlvbiBOb3J0aCxSdW5ueW1lZGUsIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNjRmM2VjNzQ1MDY1NDA0OWI0MDk1NzJmMDViNzVjNDEuc2V0Q29udGVudChodG1sX2FiOTRjMmE4ZmM2ZTQwZTk4MGUyMTE3NDgyNWZmYjU3KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9hOTY1ODkzYTA2Mzg0YjQ4YmI0MjBiOGU4Zjk1OTZjZi5iaW5kUG9wdXAocG9wdXBfNjRmM2VjNzQ1MDY1NDA0OWI0MDk1NzJmMDViNzVjNDEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2MyMGZkNWJkZGM0NTRhOWQ5NTgyYTAwMTVkYTdmYTEyID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjYxNjA4MywgLTc5LjQ2NDc2MzI5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzQ5ODZkNmQ0M2IwNjQxNTk4MzFiMDY1M2M5ZjcwYzhkID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF82MTdlNmNmOWRjYTA0OTYxODJkYzVjZDA4NDk5OTI1ZCA9ICQoYDxkaXYgaWQ9Imh0bWxfNjE3ZTZjZjlkY2EwNDk2MTgyZGM1Y2QwODQ5OTkyNWQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhpZ2ggUGFyayxUaGUgSnVuY3Rpb24gU291dGgsIFdlc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF80OTg2ZDZkNDNiMDY0MTU5ODMxYjA2NTNjOWY3MGM4ZC5zZXRDb250ZW50KGh0bWxfNjE3ZTZjZjlkY2EwNDk2MTgyZGM1Y2QwODQ5OTkyNWQpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2MyMGZkNWJkZGM0NTRhOWQ5NTgyYTAwMTVkYTdmYTEyLmJpbmRQb3B1cChwb3B1cF80OTg2ZDZkNDNiMDY0MTU5ODMxYjA2NTNjOWY3MGM4ZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDQ5N2IzODlmZWExNGY2ZThmM2ZhZTY0ZDNjZGFmMDYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDg5NTk3LCAtNzkuNDU2MzI1XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzM5NWM5NzJkNjUxZDRlMzdiOGFlOTdkYTA4MDE2YWUyID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8yYjI4OTkyOTQyMGU0ODMzODA3NTk4MmZjNzM4MWE3YyA9ICQoYDxkaXYgaWQ9Imh0bWxfMmIyODk5Mjk0MjBlNDgzMzgwNzU5ODJmYzczODFhN2MiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlBhcmtkYWxlLFJvbmNlc3ZhbGxlcywgV2VzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzM5NWM5NzJkNjUxZDRlMzdiOGFlOTdkYTA4MDE2YWUyLnNldENvbnRlbnQoaHRtbF8yYjI4OTkyOTQyMGU0ODMzODA3NTk4MmZjNzM4MWE3Yyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMDQ5N2IzODlmZWExNGY2ZThmM2ZhZTY0ZDNjZGFmMDYuYmluZFBvcHVwKHBvcHVwXzM5NWM5NzJkNjUxZDRlMzdiOGFlOTdkYTA4MDE2YWUyKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl82NmZmNjQwZGNkNGY0NWUxYWRjMDQ0ZTY2ZTY5MTViNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1MTU3MDYsIC03OS40ODQ0NDk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzZhZDk4MjZkMTgxMjQzY2M4MzMzOGZjODFlMTkwZGE3ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9kOWRjMGQzMjI5Yjc0NzA1YmM0Yzk5ZWIyZmFmMTM3MCA9ICQoYDxkaXYgaWQ9Imh0bWxfZDlkYzBkMzIyOWI3NDcwNWJjNGM5OWViMmZhZjEzNzAiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJ1bm55bWVkZSxTd2Fuc2VhLCBXZXN0IFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNmFkOTgyNmQxODEyNDNjYzgzMzM4ZmM4MWUxOTBkYTcuc2V0Q29udGVudChodG1sX2Q5ZGMwZDMyMjliNzQ3MDViYzRjOTllYjJmYWYxMzcwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl82NmZmNjQwZGNkNGY0NWUxYWRjMDQ0ZTY2ZTY5MTViNi5iaW5kUG9wdXAocG9wdXBfNmFkOTgyNmQxODEyNDNjYzgzMzM4ZmM4MWUxOTBkYTcpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzE2Mjk0MWY2NWMxYTQxY2E5ZjZlYWJlNDgxNDJjMTViID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjYyMzAxNSwgLTc5LjM4OTQ5MzhdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfM2U3MWMxNDFhNDEyNDg4NDg0MTZmMWQwMDY5YjkxZjggPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzk4MDgwY2Y0ZGM0NzRkZDM5ZGFjZmQ5YmQ4OTU1YjIyID0gJChgPGRpdiBpZD0iaHRtbF85ODA4MGNmNGRjNDc0ZGQzOWRhY2ZkOWJkODk1NWIyMiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UXVlZW4mIzM5O3MgUGFyaywgUXVlZW4mIzM5O3MgUGFyazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8zZTcxYzE0MWE0MTI0ODg0ODQxNmYxZDAwNjliOTFmOC5zZXRDb250ZW50KGh0bWxfOTgwODBjZjRkYzQ3NGRkMzlkYWNmZDliZDg5NTViMjIpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzE2Mjk0MWY2NWMxYTQxY2E5ZjZlYWJlNDgxNDJjMTViLmJpbmRQb3B1cChwb3B1cF8zZTcxYzE0MWE0MTI0ODg0ODQxNmYxZDAwNjliOTFmOCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMGJkYTQ3ODlkYTNmNDQ4Y2EzOWY3YmZiYWFmMTZiN2EgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42MzY5NjU2LCAtNzkuNjE1ODE4OTk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYmFjNjcyOTA3NjM2NDUxNjliOTBhOWYzZmQ4MjY3OGUgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2E5NWYzOWMxZDA2MzRkOTI4MzI3YzhmMzJlMWNhODBhID0gJChgPGRpdiBpZD0iaHRtbF9hOTVmMzljMWQwNjM0ZDkyODMyN2M4ZjMyZTFjYTgwYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2FuYWRhIFBvc3QgR2F0ZXdheSBQcm9jZXNzaW5nIENlbnRyZSwgTWlzc2lzc2F1Z2E8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfYmFjNjcyOTA3NjM2NDUxNjliOTBhOWYzZmQ4MjY3OGUuc2V0Q29udGVudChodG1sX2E5NWYzOWMxZDA2MzRkOTI4MzI3YzhmMzJlMWNhODBhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8wYmRhNDc4OWRhM2Y0NDhjYTM5ZjdiZmJhYWYxNmI3YS5iaW5kUG9wdXAocG9wdXBfYmFjNjcyOTA3NjM2NDUxNjliOTBhOWYzZmQ4MjY3OGUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2I1NjJkMWQ2NWU5ZjRiYWE4Zjc0NTQ5YTg1OTcwYzc1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjYyNzQzOSwgLTc5LjMyMTU1OF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8yNGViYjQ1MzY4MGI0NGE4OGZiNjEzZmI0MmY2ODE5MSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfM2I0MWEyOTkwNWVjNDk0NTk1M2MxODQxZmRkYWUwMjYgPSAkKGA8ZGl2IGlkPSJodG1sXzNiNDFhMjk5MDVlYzQ5NDU5NTNjMTg0MWZkZGFlMDI2IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CdXNpbmVzcyBSZXBseSBNYWlsIFByb2Nlc3NpbmcgQ2VudHJlIDk2OSBFYXN0ZXJuLCBFYXN0IFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMjRlYmI0NTM2ODBiNDRhODhmYjYxM2ZiNDJmNjgxOTEuc2V0Q29udGVudChodG1sXzNiNDFhMjk5MDVlYzQ5NDU5NTNjMTg0MWZkZGFlMDI2KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9iNTYyZDFkNjVlOWY0YmFhOGY3NDU0OWE4NTk3MGM3NS5iaW5kUG9wdXAocG9wdXBfMjRlYmI0NTM2ODBiNDRhODhmYjYxM2ZiNDJmNjgxOTEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2UwYzY5MjNiMTU3ZDRmNjNhZjUyMmViZTQ4M2RiZDVlID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjA1NjQ2NiwgLTc5LjUwMTMyMDcwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2E1OThhYjBhNjBkNDQwZWQ4MzhhNWFkZWNkYWVlNjg1ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9kOGE3MTQ3ZGViMzA0YTdlOTRiOGM2NTAxZjg5NTk1MiA9ICQoYDxkaXYgaWQ9Imh0bWxfZDhhNzE0N2RlYjMwNGE3ZTk0YjhjNjUwMWY4OTU5NTIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkh1bWJlciBCYXkgU2hvcmVzLE1pbWljbyBTb3V0aCxOZXcgVG9yb250bywgRXRvYmljb2tlPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2E1OThhYjBhNjBkNDQwZWQ4MzhhNWFkZWNkYWVlNjg1LnNldENvbnRlbnQoaHRtbF9kOGE3MTQ3ZGViMzA0YTdlOTRiOGM2NTAxZjg5NTk1Mik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZTBjNjkyM2IxNTdkNGY2M2FmNTIyZWJlNDgzZGJkNWUuYmluZFBvcHVwKHBvcHVwX2E1OThhYjBhNjBkNDQwZWQ4MzhhNWFkZWNkYWVlNjg1KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81MjhjNmFlM2VhZjA0MzdhOGU4YjZjNDdjYzU4NGFkNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjYwMjQxMzcwMDAwMDAxLCAtNzkuNTQzNDg0MDk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMGM3OTM4YzgxZGI5NDhlOWEwZThmMTgxZTRlYjFhZTIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzZhZGY2NzA5NjEzODRhMTdiYzY1ZTgzMTU3YzdmMmY0ID0gJChgPGRpdiBpZD0iaHRtbF82YWRmNjcwOTYxMzg0YTE3YmM2NWU4MzE1N2M3ZjJmNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QWxkZXJ3b29kLExvbmcgQnJhbmNoLCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMGM3OTM4YzgxZGI5NDhlOWEwZThmMTgxZTRlYjFhZTIuc2V0Q29udGVudChodG1sXzZhZGY2NzA5NjEzODRhMTdiYzY1ZTgzMTU3YzdmMmY0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl81MjhjNmFlM2VhZjA0MzdhOGU4YjZjNDdjYzU4NGFkNi5iaW5kUG9wdXAocG9wdXBfMGM3OTM4YzgxZGI5NDhlOWEwZThmMTgxZTRlYjFhZTIpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzM1OTkzYWQyZGI0NDRiM2Q4MGVjMjkxYWY5ODlhOGU2ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjUzNjUzNjAwMDAwMDA1LCAtNzkuNTA2OTQzNl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8xZTU0MDlhZDM3YmQ0ZDVkODU5ZTY4ZmVjMzIzOTgwNSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfOGUxNDA4MzFiYTc5NGE0N2E2OThiZDI2ZjVkNjI4YjYgPSAkKGA8ZGl2IGlkPSJodG1sXzhlMTQwODMxYmE3OTRhNDdhNjk4YmQyNmY1ZDYyOGI2IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UaGUgS2luZ3N3YXksTW9udGdvbWVyeSBSb2FkLE9sZCBNaWxsIE5vcnRoLCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMWU1NDA5YWQzN2JkNGQ1ZDg1OWU2OGZlYzMyMzk4MDUuc2V0Q29udGVudChodG1sXzhlMTQwODMxYmE3OTRhNDdhNjk4YmQyNmY1ZDYyOGI2KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8zNTk5M2FkMmRiNDQ0YjNkODBlYzI5MWFmOTg5YThlNi5iaW5kUG9wdXAocG9wdXBfMWU1NDA5YWQzN2JkNGQ1ZDg1OWU2OGZlYzMyMzk4MDUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzU3MGY0NzZhNWM3NzQyNzhiNjRlNTI1ZDYzZTg3NTc4ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjM2MjU3OSwgLTc5LjQ5ODUwOTA5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzNmYjRjNWUwNzBhMzQyYmU4NjM4MGQxNTkyOTA3YTdlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9iNmZkMDdiM2IzNWU0YWEzOWYxY2E3NDQxNDE2NjFlMCA9ICQoYDxkaXYgaWQ9Imh0bWxfYjZmZDA3YjNiMzVlNGFhMzlmMWNhNzQ0MTQxNjYxZTAiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkh1bWJlciBCYXksS2luZyYjMzk7cyBNaWxsIFBhcmssS2luZ3N3YXkgUGFyayBTb3V0aCBFYXN0LE1pbWljbyBORSxPbGQgTWlsbCBTb3V0aCxUaGUgUXVlZW5zd2F5IEVhc3QsUm95YWwgWW9yayBTb3V0aCBFYXN0LFN1bm55bGVhLCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfM2ZiNGM1ZTA3MGEzNDJiZTg2MzgwZDE1OTI5MDdhN2Uuc2V0Q29udGVudChodG1sX2I2ZmQwN2IzYjM1ZTRhYTM5ZjFjYTc0NDE0MTY2MWUwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl81NzBmNDc2YTVjNzc0Mjc4YjY0ZTUyNWQ2M2U4NzU3OC5iaW5kUG9wdXAocG9wdXBfM2ZiNGM1ZTA3MGEzNDJiZTg2MzgwZDE1OTI5MDdhN2UpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzIzOGU0ZGU1ZWJhMzRjODlhMWIyY2I4YWJjYzU2NTU3ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjI4ODQwOCwgLTc5LjUyMDk5OTQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2QwZWU4MzM1ZWZjYTQ0MzdiYmIwZTg2MGQxNThhZjc3ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9hMmZlOWRiMmFhMzI0NDU3YTk2YjBiOWQ2MjI4MTAwZSA9ICQoYDxkaXYgaWQ9Imh0bWxfYTJmZTlkYjJhYTMyNDQ1N2E5NmIwYjlkNjIyODEwMGUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPktpbmdzd2F5IFBhcmsgU291dGggV2VzdCxNaW1pY28gTlcsVGhlIFF1ZWVuc3dheSBXZXN0LFJveWFsIFlvcmsgU291dGggV2VzdCxTb3V0aCBvZiBCbG9vciwgRXRvYmljb2tlPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2QwZWU4MzM1ZWZjYTQ0MzdiYmIwZTg2MGQxNThhZjc3LnNldENvbnRlbnQoaHRtbF9hMmZlOWRiMmFhMzI0NDU3YTk2YjBiOWQ2MjI4MTAwZSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMjM4ZTRkZTVlYmEzNGM4OWExYjJjYjhhYmNjNTY1NTcuYmluZFBvcHVwKHBvcHVwX2QwZWU4MzM1ZWZjYTQ0MzdiYmIwZTg2MGQxNThhZjc3KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80ZTdkYTc5OTU2YzY0MmQyYTQ1ZTU5NTI2NGM3MzhhNSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2Nzg1NTYsIC03OS41MzIyNDI0MDAwMDAwMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF81NmYwYmIwMzU2OTA0MzYxYTk3NGQ5YjA0OGU4MTVhZSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZGQ2YjM5ZjE4MjIyNGM1MGFiMzVmYzRiNWVmMmY5ZTUgPSAkKGA8ZGl2IGlkPSJodG1sX2RkNmIzOWYxODIyMjRjNTBhYjM1ZmM0YjVlZjJmOWU1IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Jc2xpbmd0b24gQXZlbnVlLCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNTZmMGJiMDM1NjkwNDM2MWE5NzRkOWIwNDhlODE1YWUuc2V0Q29udGVudChodG1sX2RkNmIzOWYxODIyMjRjNTBhYjM1ZmM0YjVlZjJmOWU1KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl80ZTdkYTc5OTU2YzY0MmQyYTQ1ZTU5NTI2NGM3MzhhNS5iaW5kUG9wdXAocG9wdXBfNTZmMGJiMDM1NjkwNDM2MWE5NzRkOWIwNDhlODE1YWUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzkyMjJlZGU4MjE3NjQzODRiODFiNmE0NzI5MjUwOWUwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjUwOTQzMiwgLTc5LjU1NDcyNDQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzA4NjI1YmY1YmZkMjQyNjVhNDQxZjI4NjZhODM3OTI4ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9hNjdjMjA2YTRjNWI0ZDFlOThkY2ZjZGQ0OWUyMWExZCA9ICQoYDxkaXYgaWQ9Imh0bWxfYTY3YzIwNmE0YzViNGQxZTk4ZGNmY2RkNDllMjFhMWQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNsb3ZlcmRhbGUsSXNsaW5ndG9uLE1hcnRpbiBHcm92ZSxQcmluY2VzcyBHYXJkZW5zLFdlc3QgRGVhbmUgUGFyaywgRXRvYmljb2tlPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzA4NjI1YmY1YmZkMjQyNjVhNDQxZjI4NjZhODM3OTI4LnNldENvbnRlbnQoaHRtbF9hNjdjMjA2YTRjNWI0ZDFlOThkY2ZjZGQ0OWUyMWExZCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfOTIyMmVkZTgyMTc2NDM4NGI4MWI2YTQ3MjkyNTA5ZTAuYmluZFBvcHVwKHBvcHVwXzA4NjI1YmY1YmZkMjQyNjVhNDQxZjI4NjZhODM3OTI4KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl83OGU3NTcwYjIwNTU0N2U1YTVlZWJkYmZmYTEwMGMzMSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0MzUxNTIsIC03OS41NzcyMDA3OTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF83MjZmZDc2YjlmNWM0ZDI5ODAzZDYxOWMxN2Q3MWFhNiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZWI5MzRmMmQzY2IyNGZiNmJmMDVmNjYzZmU0MjgyNzggPSAkKGA8ZGl2IGlkPSJodG1sX2ViOTM0ZjJkM2NiMjRmYjZiZjA1ZjY2M2ZlNDI4Mjc4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CbG9vcmRhbGUgR2FyZGVucyxFcmluZ2F0ZSxNYXJrbGFuZCBXb29kLE9sZCBCdXJuaGFtdGhvcnBlLCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNzI2ZmQ3NmI5ZjVjNGQyOTgwM2Q2MTljMTdkNzFhYTYuc2V0Q29udGVudChodG1sX2ViOTM0ZjJkM2NiMjRmYjZiZjA1ZjY2M2ZlNDI4Mjc4KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl83OGU3NTcwYjIwNTU0N2U1YTVlZWJkYmZmYTEwMGMzMS5iaW5kUG9wdXAocG9wdXBfNzI2ZmQ3NmI5ZjVjNGQyOTgwM2Q2MTljMTdkNzFhYTYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzA2N2I0OThiZDkxYTRmMmY4ODkwMzE5MmU4YWIwYzcwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzU2MzAzMywgLTc5LjU2NTk2MzI5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzgwMDAyMTZjZmE2ZDQ4YTViZDJkZjJkZmY1OTI5NTQ4ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8zMjJjNjY3YzczODE0OGIyOGM5ZjYxMjhmYmJiY2YyYSA9ICQoYDxkaXYgaWQ9Imh0bWxfMzIyYzY2N2M3MzgxNDhiMjhjOWY2MTI4ZmJiYmNmMmEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkh1bWJlciBTdW1taXQsIE5vcnRoIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfODAwMDIxNmNmYTZkNDhhNWJkMmRmMmRmZjU5Mjk1NDguc2V0Q29udGVudChodG1sXzMyMmM2NjdjNzM4MTQ4YjI4YzlmNjEyOGZiYmJjZjJhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8wNjdiNDk4YmQ5MWE0ZjJmODg5MDMxOTJlOGFiMGM3MC5iaW5kUG9wdXAocG9wdXBfODAwMDIxNmNmYTZkNDhhNWJkMmRmMmRmZjU5Mjk1NDgpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2QwOWYwMThhMmRjZTQ2Y2JhYTIzZTcxNmU1MTQ4M2QwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzI0NzY1OSwgLTc5LjUzMjI0MjQwMDAwMDAyXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzdjODgzYzgzNWJkMDQ0N2ZiNTZjZjE5YWU3MmJiYWU1ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9lYjc5OWRiYWQ4ZTU0ZDY1YTI5Zjk1ZDU4OGYwNTcwZSA9ICQoYDxkaXYgaWQ9Imh0bWxfZWI3OTlkYmFkOGU1NGQ2NWEyOWY5NWQ1ODhmMDU3MGUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkVtZXJ5LEh1bWJlcmxlYSwgTm9ydGggWW9yazwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83Yzg4M2M4MzViZDA0NDdmYjU2Y2YxOWFlNzJiYmFlNS5zZXRDb250ZW50KGh0bWxfZWI3OTlkYmFkOGU1NGQ2NWEyOWY5NWQ1ODhmMDU3MGUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2QwOWYwMThhMmRjZTQ2Y2JhYTIzZTcxNmU1MTQ4M2QwLmJpbmRQb3B1cChwb3B1cF83Yzg4M2M4MzViZDA0NDdmYjU2Y2YxOWFlNzJiYmFlNSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOGUwMjdjMjQxMTBmNDhkNzkwMGY5NTViZmFhNTE4NTUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MDY4NzYsIC03OS41MTgxODg0MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF84NjIyZTdmZjExNDY0MWQ4OTc4Y2U2ODRmZTZjNmZmZSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNTRjMzI0YzExMmFmNGY0NDhlMDhiYWZmYjliMWFkMjMgPSAkKGA8ZGl2IGlkPSJodG1sXzU0YzMyNGMxMTJhZjRmNDQ4ZTA4YmFmZmI5YjFhZDIzIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5XZXN0b24sIFlvcms8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfODYyMmU3ZmYxMTQ2NDFkODk3OGNlNjg0ZmU2YzZmZmUuc2V0Q29udGVudChodG1sXzU0YzMyNGMxMTJhZjRmNDQ4ZTA4YmFmZmI5YjFhZDIzKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl84ZTAyN2MyNDExMGY0OGQ3OTAwZjk1NWJmYWE1MTg1NS5iaW5kUG9wdXAocG9wdXBfODYyMmU3ZmYxMTQ2NDFkODk3OGNlNjg0ZmU2YzZmZmUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzZlYTY1M2JlMzlhNTQ2ODRiMGZmNWYzNDQ3Y2I1NGNiID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjk2MzE5LCAtNzkuNTMyMjQyNDAwMDAwMDJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF82NGNkZTAwMTY2YjM0ZThhYmFiOWRkOGJkMmVmOGU5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZWUwOWZhYTdkNDUxNDY2Nzg4ZDQ4OWJjOTRlNWM1ZWEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzEzMzNiNWQ4YTQ1NjQ3MWVhNDMxOTg5M2Y0MjBjNjRkID0gJChgPGRpdiBpZD0iaHRtbF8xMzMzYjVkOGE0NTY0NzFlYTQzMTk4OTNmNDIwYzY0ZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+V2VzdG1vdW50LCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfZWUwOWZhYTdkNDUxNDY2Nzg4ZDQ4OWJjOTRlNWM1ZWEuc2V0Q29udGVudChodG1sXzEzMzNiNWQ4YTQ1NjQ3MWVhNDMxOTg5M2Y0MjBjNjRkKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl82ZWE2NTNiZTM5YTU0Njg0YjBmZjVmMzQ0N2NiNTRjYi5iaW5kUG9wdXAocG9wdXBfZWUwOWZhYTdkNDUxNDY2Nzg4ZDQ4OWJjOTRlNWM1ZWEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2MxNzAzNWZiMjI5ZTQyMDM4ZjAzNzY5MzZhMjY2MDM5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjg4OTA1NCwgLTc5LjU1NDcyNDQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzEwNGQyYmZlYjVjODQwOTg4YmE1ZTNiM2QzYTJmNDcwID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9hMDQzODAwZjE4ZTM0NTYyYTZkZWRjZjA4NDNjYzNlMiA9ICQoYDxkaXYgaWQ9Imh0bWxfYTA0MzgwMGYxOGUzNDU2MmE2ZGVkY2YwODQzY2MzZTIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPktpbmdzdmlldyBWaWxsYWdlLE1hcnRpbiBHcm92ZSBHYXJkZW5zLFJpY2h2aWV3IEdhcmRlbnMsU3QuIFBoaWxsaXBzLCBFdG9iaWNva2U8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMTA0ZDJiZmViNWM4NDA5ODhiYTVlM2IzZDNhMmY0NzAuc2V0Q29udGVudChodG1sX2EwNDM4MDBmMThlMzQ1NjJhNmRlZGNmMDg0M2NjM2UyKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9jMTcwMzVmYjIyOWU0MjAzOGYwMzc2OTM2YTI2NjAzOS5iaW5kUG9wdXAocG9wdXBfMTA0ZDJiZmViNWM4NDA5ODhiYTVlM2IzZDNhMmY0NzApCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2I5YjQwN2RlOTc1ZjRjYzc4ZWY2ODU1NGQwNzkyN2VjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzM5NDE2Mzk5OTk5OTk2LCAtNzkuNTg4NDM2OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzY0Y2RlMDAxNjZiMzRlOGFiYWI5ZGQ4YmQyZWY4ZTlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF82ODJkZjE4NjMwNzM0ODYwYjliNzI5ZjljOTFkZDZiNSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNzBjNjNlZTYyNWY4NDM2NThlMmQ4YjlhMGEyYTc0ZmEgPSAkKGA8ZGl2IGlkPSJodG1sXzcwYzYzZWU2MjVmODQzNjU4ZTJkOGI5YTBhMmE3NGZhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5BbGJpb24gR2FyZGVucyxCZWF1bW9uZCBIZWlnaHRzLEh1bWJlcmdhdGUsSmFtZXN0b3duLE1vdW50IE9saXZlLFNpbHZlcnN0b25lLFNvdXRoIFN0ZWVsZXMsVGhpc3RsZXRvd24sIEV0b2JpY29rZTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF82ODJkZjE4NjMwNzM0ODYwYjliNzI5ZjljOTFkZDZiNS5zZXRDb250ZW50KGh0bWxfNzBjNjNlZTYyNWY4NDM2NThlMmQ4YjlhMGEyYTc0ZmEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2I5YjQwN2RlOTc1ZjRjYzc4ZWY2ODU1NGQwNzkyN2VjLmJpbmRQb3B1cChwb3B1cF82ODJkZjE4NjMwNzM0ODYwYjliNzI5ZjljOTFkZDZiNSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZGY0YzlkY2ZlZmNlNGEzMzlkODcyZDg4ZTY1NWI2OGUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MDY3NDgyOTk5OTk5OTQsIC03OS41OTQwNTQ0XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfNjRjZGUwMDE2NmIzNGU4YWJhYjlkZDhiZDJlZjhlOWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2NkMTg4MGM2ODNmMDQ0YzZhNDAzNGNjMmNmMTZjY2JmID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF85MGMzY2UxMTM2ZGE0MDVlYjBhZWE2YTRjOWE0MmMxZSA9ICQoYDxkaXYgaWQ9Imh0bWxfOTBjM2NlMTEzNmRhNDA1ZWIwYWVhNmE0YzlhNDJjMWUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk5vcnRod2VzdCwgRXRvYmljb2tlPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2NkMTg4MGM2ODNmMDQ0YzZhNDAzNGNjMmNmMTZjY2JmLnNldENvbnRlbnQoaHRtbF85MGMzY2UxMTM2ZGE0MDVlYjBhZWE2YTRjOWE0MmMxZSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZGY0YzlkY2ZlZmNlNGEzMzlkODcyZDg4ZTY1NWI2OGUuYmluZFBvcHVwKHBvcHVwX2NkMTg4MGM2ODNmMDQ0YzZhNDAzNGNjMmNmMTZjY2JmKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKPC9zY3JpcHQ+" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```bash
%%bash
pip install folium
```

    Collecting folium
      Downloading https://files.pythonhosted.org/packages/72/ff/004bfe344150a064e558cb2aedeaa02ecbf75e60e148a55a9198f0c41765/folium-0.10.0-py2.py3-none-any.whl (91kB)
    Requirement already satisfied: requests in /anaconda3/lib/python3.7/site-packages (from folium) (2.22.0)
    Requirement already satisfied: jinja2>=2.9 in /anaconda3/lib/python3.7/site-packages (from folium) (2.10.1)
    Requirement already satisfied: numpy in /anaconda3/lib/python3.7/site-packages (from folium) (1.16.4)
    Collecting branca>=0.3.0 (from folium)
      Downloading https://files.pythonhosted.org/packages/63/36/1c93318e9653f4e414a2e0c3b98fc898b4970e939afeedeee6075dd3b703/branca-0.3.1-py3-none-any.whl
    Requirement already satisfied: idna<2.9,>=2.5 in /anaconda3/lib/python3.7/site-packages (from requests->folium) (2.8)
    Requirement already satisfied: certifi>=2017.4.17 in /anaconda3/lib/python3.7/site-packages (from requests->folium) (2019.6.16)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /anaconda3/lib/python3.7/site-packages (from requests->folium) (1.24.2)
    Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /anaconda3/lib/python3.7/site-packages (from requests->folium) (3.0.4)
    Requirement already satisfied: MarkupSafe>=0.23 in /anaconda3/lib/python3.7/site-packages (from jinja2>=2.9->folium) (1.1.1)
    Requirement already satisfied: six in /anaconda3/lib/python3.7/site-packages (from branca>=0.3.0->folium) (1.12.0)
    Installing collected packages: branca, folium
    Successfully installed branca-0.3.1 folium-0.10.0



```python

```
