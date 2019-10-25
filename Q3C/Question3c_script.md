
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




```python
###Filter where borough contains 'toronto'


visualise_df = geo_df[geo_df['Borough'].str.contains("Toronto")].reset_index(drop=True)
```

### First initial visual look at the locations


```python
# create map of Toronto using latitude and longitude values
import folium
map_test = folium.Map(location=["43.6532", "-79.3832"])

# add markers to map
for lat, lng, borough, neighborhood in zip(visualise_df['Latitude'], visualise_df['Longitude'], visualise_df['Borough'], visualise_df['Neighbourhood']):
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




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgCiAgICAgICAgPHNjcmlwdD4KICAgICAgICAgICAgTF9OT19UT1VDSCA9IGZhbHNlOwogICAgICAgICAgICBMX0RJU0FCTEVfM0QgPSBmYWxzZTsKICAgICAgICA8L3NjcmlwdD4KICAgIAogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuanMiPjwvc2NyaXB0PgogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY29kZS5qcXVlcnkuY29tL2pxdWVyeS0xLjEyLjQubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9qcy9ib290c3RyYXAubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5qcyI+PC9zY3JpcHQ+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vYm9vdHN0cmFwLzMuMi4wL2Nzcy9ib290c3RyYXAubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLXRoZW1lLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9mb250LWF3ZXNvbWUvNC42LjMvY3NzL2ZvbnQtYXdlc29tZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuanMuY2xvdWRmbGFyZS5jb20vYWpheC9saWJzL0xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLzIuMC4yL2xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL3Jhd2Nkbi5naXRoYWNrLmNvbS9weXRob24tdmlzdWFsaXphdGlvbi9mb2xpdW0vbWFzdGVyL2ZvbGl1bS90ZW1wbGF0ZXMvbGVhZmxldC5hd2Vzb21lLnJvdGF0ZS5jc3MiLz4KICAgIDxzdHlsZT5odG1sLCBib2R5IHt3aWR0aDogMTAwJTtoZWlnaHQ6IDEwMCU7bWFyZ2luOiAwO3BhZGRpbmc6IDA7fTwvc3R5bGU+CiAgICA8c3R5bGU+I21hcCB7cG9zaXRpb246YWJzb2x1dGU7dG9wOjA7Ym90dG9tOjA7cmlnaHQ6MDtsZWZ0OjA7fTwvc3R5bGU+CiAgICAKICAgICAgICAgICAgPG1ldGEgbmFtZT0idmlld3BvcnQiIGNvbnRlbnQ9IndpZHRoPWRldmljZS13aWR0aCwKICAgICAgICAgICAgICAgIGluaXRpYWwtc2NhbGU9MS4wLCBtYXhpbXVtLXNjYWxlPTEuMCwgdXNlci1zY2FsYWJsZT1ubyIgLz4KICAgICAgICAgICAgPHN0eWxlPgogICAgICAgICAgICAgICAgI21hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSB7CiAgICAgICAgICAgICAgICAgICAgcG9zaXRpb246IHJlbGF0aXZlOwogICAgICAgICAgICAgICAgICAgIHdpZHRoOiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgbGVmdDogMC4wJTsKICAgICAgICAgICAgICAgICAgICB0b3A6IDAuMCU7CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIDwvc3R5bGU+CiAgICAgICAgCjwvaGVhZD4KPGJvZHk+ICAgIAogICAgCiAgICAgICAgICAgIDxkaXYgY2xhc3M9ImZvbGl1bS1tYXAiIGlkPSJtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUiID48L2Rpdj4KICAgICAgICAKPC9ib2R5Pgo8c2NyaXB0PiAgICAKICAgIAogICAgICAgICAgICB2YXIgbWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlID0gTC5tYXAoCiAgICAgICAgICAgICAgICAibWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlIiwKICAgICAgICAgICAgICAgIHsKICAgICAgICAgICAgICAgICAgICBjZW50ZXI6IFs0My42NTMyLCAtNzkuMzgzMl0sCiAgICAgICAgICAgICAgICAgICAgY3JzOiBMLkNSUy5FUFNHMzg1NywKICAgICAgICAgICAgICAgICAgICB6b29tOiAxMCwKICAgICAgICAgICAgICAgICAgICB6b29tQ29udHJvbDogdHJ1ZSwKICAgICAgICAgICAgICAgICAgICBwcmVmZXJDYW52YXM6IGZhbHNlLAogICAgICAgICAgICAgICAgfQogICAgICAgICAgICApOwoKICAgICAgICAgICAgCgogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyXzY3MWUxMDE3OTAwMTQ2NjhiYzlhODU5NmE4M2RmYWJiID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAiaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmciLAogICAgICAgICAgICAgICAgeyJhdHRyaWJ1dGlvbiI6ICJEYXRhIGJ5IFx1MDAyNmNvcHk7IFx1MDAzY2EgaHJlZj1cImh0dHA6Ly9vcGVuc3RyZWV0bWFwLm9yZ1wiXHUwMDNlT3BlblN0cmVldE1hcFx1MDAzYy9hXHUwMDNlLCB1bmRlciBcdTAwM2NhIGhyZWY9XCJodHRwOi8vd3d3Lm9wZW5zdHJlZXRtYXAub3JnL2NvcHlyaWdodFwiXHUwMDNlT0RiTFx1MDAzYy9hXHUwMDNlLiIsICJkZXRlY3RSZXRpbmEiOiBmYWxzZSwgIm1heE5hdGl2ZVpvb20iOiAxOCwgIm1heFpvb20iOiAxOCwgIm1pblpvb20iOiAwLCAibm9XcmFwIjogZmFsc2UsICJvcGFjaXR5IjogMSwgInN1YmRvbWFpbnMiOiAiYWJjIiwgInRtcyI6IGZhbHNlfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYzkzOGY0OTg0NTJkNDMwZGI3Mzg2ZWQzM2Y3N2IyNjAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NzYzNTczOTk5OTk5OSwgLTc5LjI5MzAzMTJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfODlkNWI5Y2FjMjZmNDNiZWJjNjRjYjIwNDRlMjgyODQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2FlNDA0YjQ3MjYzOTRjN2RhNDBkNzM2MjM2MzNmY2VhID0gJChgPGRpdiBpZD0iaHRtbF9hZTQwNGI0NzI2Mzk0YzdkYTQwZDczNjIzNjMzZmNlYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+VGhlIEJlYWNoZXMsIEVhc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF84OWQ1YjljYWMyNmY0M2JlYmM2NGNiMjA0NGUyODI4NC5zZXRDb250ZW50KGh0bWxfYWU0MDRiNDcyNjM5NGM3ZGE0MGQ3MzYyMzYzM2ZjZWEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2M5MzhmNDk4NDUyZDQzMGRiNzM4NmVkMzNmNzdiMjYwLmJpbmRQb3B1cChwb3B1cF84OWQ1YjljYWMyNmY0M2JlYmM2NGNiMjA0NGUyODI4NCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNzY5MTliYTRjNmNkNGE3OGExOGJiMDY3ODRjMDM5ODggPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Nzk1NTcxLCAtNzkuMzUyMTg4XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzUyOWMzZmUwMGEwZDRjOTg5M2Q5Y2M0N2I2MGViYTQ2ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83NTM3ZWU5MGY4MmI0YWFkOGIyYTlmNDliMjNiOGZkYSA9ICQoYDxkaXYgaWQ9Imh0bWxfNzUzN2VlOTBmODJiNGFhZDhiMmE5ZjQ5YjIzYjhmZGEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRoZSBEYW5mb3J0aCBXZXN0LFJpdmVyZGFsZSwgRWFzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzUyOWMzZmUwMGEwZDRjOTg5M2Q5Y2M0N2I2MGViYTQ2LnNldENvbnRlbnQoaHRtbF83NTM3ZWU5MGY4MmI0YWFkOGIyYTlmNDliMjNiOGZkYSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNzY5MTliYTRjNmNkNGE3OGExOGJiMDY3ODRjMDM5ODguYmluZFBvcHVwKHBvcHVwXzUyOWMzZmUwMGEwZDRjOTg5M2Q5Y2M0N2I2MGViYTQ2KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl85YmI1NDQ2YWQ5MDg0ZGNkYjNiMzRiZWRhZDU0MDBkYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2ODk5ODUsIC03OS4zMTU1NzE1OTk5OTk5OF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9kY2UyODc0N2QwZTM0Yjk5YTQ3ZDVlNmQyZTZmNzRmNCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfY2RlMDhhNmU0NDcyNGZiNWFlMzU2NTA3ZmZkNmNlNjIgPSAkKGA8ZGl2IGlkPSJodG1sX2NkZTA4YTZlNDQ3MjRmYjVhZTM1NjUwN2ZmZDZjZTYyIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UaGUgQmVhY2hlcyBXZXN0LEluZGlhIEJhemFhciwgRWFzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2RjZTI4NzQ3ZDBlMzRiOTlhNDdkNWU2ZDJlNmY3NGY0LnNldENvbnRlbnQoaHRtbF9jZGUwOGE2ZTQ0NzI0ZmI1YWUzNTY1MDdmZmQ2Y2U2Mik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfOWJiNTQ0NmFkOTA4NGRjZGIzYjM0YmVkYWQ1NDAwZGIuYmluZFBvcHVwKHBvcHVwX2RjZTI4NzQ3ZDBlMzRiOTlhNDdkNWU2ZDJlNmY3NGY0KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9iODZhMTQ5MmM3ZDM0YzE2ODAzYmY2MzhiZmFhOWQzMSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1OTUyNTUsIC03OS4zNDA5MjNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfN2Y1ZTFlYzkxZDRiNGI5MmFlNGY4N2ExZWZlYWUwOWQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2Y5Y2RlMWQ0MzY1MzQ0ZWFhMmJkNGFlNjUyOWU2ZjcyID0gJChgPGRpdiBpZD0iaHRtbF9mOWNkZTFkNDM2NTM0NGVhYTJiZDRhZTY1MjllNmY3MiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+U3R1ZGlvIERpc3RyaWN0LCBFYXN0IFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfN2Y1ZTFlYzkxZDRiNGI5MmFlNGY4N2ExZWZlYWUwOWQuc2V0Q29udGVudChodG1sX2Y5Y2RlMWQ0MzY1MzQ0ZWFhMmJkNGFlNjUyOWU2ZjcyKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9iODZhMTQ5MmM3ZDM0YzE2ODAzYmY2MzhiZmFhOWQzMS5iaW5kUG9wdXAocG9wdXBfN2Y1ZTFlYzkxZDRiNGI5MmFlNGY4N2ExZWZlYWUwOWQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2RjYTVkYTkzMjEwMTQwYjg5MWZiZGEwZGRhZDdiMTM1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzI4MDIwNSwgLTc5LjM4ODc5MDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZmMyZjYxMWUwMGU2NGJlZWEzNTU5Yjc5NzlmZDNmYWEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzk4MjE5MzI4ZmI0ODRhODE4YmJiMTZmY2NhYzFmMjU0ID0gJChgPGRpdiBpZD0iaHRtbF85ODIxOTMyOGZiNDg0YTgxOGJiYjE2ZmNjYWMxZjI1NCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TGF3cmVuY2UgUGFyaywgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2ZjMmY2MTFlMDBlNjRiZWVhMzU1OWI3OTc5ZmQzZmFhLnNldENvbnRlbnQoaHRtbF85ODIxOTMyOGZiNDg0YTgxOGJiYjE2ZmNjYWMxZjI1NCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZGNhNWRhOTMyMTAxNDBiODkxZmJkYTBkZGFkN2IxMzUuYmluZFBvcHVwKHBvcHVwX2ZjMmY2MTFlMDBlNjRiZWVhMzU1OWI3OTc5ZmQzZmFhKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8wODA2YWFiZmQyNTU0ZWFkYWU5ZGUwYjdjNzM1ZDcyNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcxMjc1MTEsIC03OS4zOTAxOTc1XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2Y4NzUwNmNjYzg0YjQxMjJhYWFhMDg2NDNkOWIzNmE2ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8wNWRlYmM5NjhjZDc0NDdlYTZjNTUwYzEyZmY1ZjExNCA9ICQoYDxkaXYgaWQ9Imh0bWxfMDVkZWJjOTY4Y2Q3NDQ3ZWE2YzU1MGMxMmZmNWYxMTQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkRhdmlzdmlsbGUgTm9ydGgsIENlbnRyYWwgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9mODc1MDZjY2M4NGI0MTIyYWFhYTA4NjQzZDliMzZhNi5zZXRDb250ZW50KGh0bWxfMDVkZWJjOTY4Y2Q3NDQ3ZWE2YzU1MGMxMmZmNWYxMTQpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzA4MDZhYWJmZDI1NTRlYWRhZTlkZTBiN2M3MzVkNzI2LmJpbmRQb3B1cChwb3B1cF9mODc1MDZjY2M4NGI0MTIyYWFhYTA4NjQzZDliMzZhNikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNGQ1MTRjZmU3YmUwNGUzMDk3OTU0MDJiNzBkNDFlOWIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My43MTUzODM0LCAtNzkuNDA1Njc4NDAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfODA3NzY1MzI1NWFlNGRmNWFlNGZlN2QyN2IzZTUwMjQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzc0ZjVmYzNjMzM0MzQwYjdhYmYzYmI2MmEyZTU5ZjE5ID0gJChgPGRpdiBpZD0iaHRtbF83NGY1ZmMzYzMzNDM0MGI3YWJmM2JiNjJhMmU1OWYxOSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Tm9ydGggVG9yb250byBXZXN0LCBDZW50cmFsIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfODA3NzY1MzI1NWFlNGRmNWFlNGZlN2QyN2IzZTUwMjQuc2V0Q29udGVudChodG1sXzc0ZjVmYzNjMzM0MzQwYjdhYmYzYmI2MmEyZTU5ZjE5KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl80ZDUxNGNmZTdiZTA0ZTMwOTc5NTQwMmI3MGQ0MWU5Yi5iaW5kUG9wdXAocG9wdXBfODA3NzY1MzI1NWFlNGRmNWFlNGZlN2QyN2IzZTUwMjQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2MyNGE0NTZiNDk0ZDQ5MjY5NmZkNTYzNTRkMjdhODFhID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzA0MzI0NCwgLTc5LjM4ODc5MDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZThlMzI0ZmM0N2QwNGM2NTllNjI2YjJiOTVkYjY0MTUgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzY0OWNiMDZmNDQ2NzRlNGE5OTc4Y2M0YTM2OTRkYjZkID0gJChgPGRpdiBpZD0iaHRtbF82NDljYjA2ZjQ0Njc0ZTRhOTk3OGNjNGEzNjk0ZGI2ZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGF2aXN2aWxsZSwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2U4ZTMyNGZjNDdkMDRjNjU5ZTYyNmIyYjk1ZGI2NDE1LnNldENvbnRlbnQoaHRtbF82NDljYjA2ZjQ0Njc0ZTRhOTk3OGNjNGEzNjk0ZGI2ZCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYzI0YTQ1NmI0OTRkNDkyNjk2ZmQ1NjM1NGQyN2E4MWEuYmluZFBvcHVwKHBvcHVwX2U4ZTMyNGZjNDdkMDRjNjU5ZTYyNmIyYjk1ZGI2NDE1KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81YTI5NzlkYmM5NjQ0ODliOTRmY2NlMDkzZDFhMWZjYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY4OTU3NDMsIC03OS4zODMxNTk5MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF85NDIxY2NiZWY2N2U0ZWQ5ODc5ZTBiN2U1OWY3OWQ5ZSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYjdkM2E5MzNmZGEyNDZjY2JiMzZiZjRiNzI1YjU4NmMgPSAkKGA8ZGl2IGlkPSJodG1sX2I3ZDNhOTMzZmRhMjQ2Y2NiYjM2YmY0YjcyNWI1ODZjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Nb29yZSBQYXJrLFN1bW1lcmhpbGwgRWFzdCwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzk0MjFjY2JlZjY3ZTRlZDk4NzllMGI3ZTU5Zjc5ZDllLnNldENvbnRlbnQoaHRtbF9iN2QzYTkzM2ZkYTI0NmNjYmIzNmJmNGI3MjViNTg2Yyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNWEyOTc5ZGJjOTY0NDg5Yjk0ZmNjZTA5M2QxYTFmY2IuYmluZFBvcHVwKHBvcHVwXzk0MjFjY2JlZjY3ZTRlZDk4NzllMGI3ZTU5Zjc5ZDllKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl85Zjg5ZTY5YjBkNzI0ODA3OTkzM2E4MWQwM2ZmOGExMyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY4NjQxMjI5OTk5OTk5LCAtNzkuNDAwMDQ5M10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9jODY4NDIwZDNlZWQ0NGUwYTZmMTMwNzI5ZTUyMzI1MSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNmVkODc0ZTc2ZGE0NDFlYThhYWVhNTVkODAyYjU0ODQgPSAkKGA8ZGl2IGlkPSJodG1sXzZlZDg3NGU3NmRhNDQxZWE4YWFlYTU1ZDgwMmI1NDg0IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5EZWVyIFBhcmssRm9yZXN0IEhpbGwgU0UsUmF0aG5lbGx5LFNvdXRoIEhpbGwsU3VtbWVyaGlsbCBXZXN0LCBDZW50cmFsIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfYzg2ODQyMGQzZWVkNDRlMGE2ZjEzMDcyOWU1MjMyNTEuc2V0Q29udGVudChodG1sXzZlZDg3NGU3NmRhNDQxZWE4YWFlYTU1ZDgwMmI1NDg0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl85Zjg5ZTY5YjBkNzI0ODA3OTkzM2E4MWQwM2ZmOGExMy5iaW5kUG9wdXAocG9wdXBfYzg2ODQyMGQzZWVkNDRlMGE2ZjEzMDcyOWU1MjMyNTEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzMzY2FmY2JkZmIwMTRkZWRiOTMyODdjNDA0ZmNhNDczID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjc5NTYyNiwgLTc5LjM3NzUyOTQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2ZiYjFiNDAxZTg2NjRkODRhODNlNDVkNjk2MjhiNDJjID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9lMzM3N2I4ZGFiYjE0MTE2YjlkN2NjNWU1NzFhNjY1ZSA9ICQoYDxkaXYgaWQ9Imh0bWxfZTMzNzdiOGRhYmIxNDExNmI5ZDdjYzVlNTcxYTY2NWUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJvc2VkYWxlLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2ZiYjFiNDAxZTg2NjRkODRhODNlNDVkNjk2MjhiNDJjLnNldENvbnRlbnQoaHRtbF9lMzM3N2I4ZGFiYjE0MTE2YjlkN2NjNWU1NzFhNjY1ZSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMzNjYWZjYmRmYjAxNGRlZGI5MzI4N2M0MDRmY2E0NzMuYmluZFBvcHVwKHBvcHVwX2ZiYjFiNDAxZTg2NjRkODRhODNlNDVkNjk2MjhiNDJjKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8zNDA1YmZkZWY4MDU0NmZjYTIzZjQ1ODhlNWM1ZjY2NiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2Nzk2NywgLTc5LjM2NzY3NTNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMWI3NmRmOWVlM2MxNGUzZWI2NTFjNzMzMGU1MDA3ZDggPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQ2YzhjOTE0YjA1YTQwNzZhZjAxMWZiZjEwOGY1OWJjID0gJChgPGRpdiBpZD0iaHRtbF80NmM4YzkxNGIwNWE0MDc2YWYwMTFmYmYxMDhmNTliYyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2FiYmFnZXRvd24sU3QuIEphbWVzIFRvd24sIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMWI3NmRmOWVlM2MxNGUzZWI2NTFjNzMzMGU1MDA3ZDguc2V0Q29udGVudChodG1sXzQ2YzhjOTE0YjA1YTQwNzZhZjAxMWZiZjEwOGY1OWJjKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8zNDA1YmZkZWY4MDU0NmZjYTIzZjQ1ODhlNWM1ZjY2Ni5iaW5kUG9wdXAocG9wdXBfMWI3NmRmOWVlM2MxNGUzZWI2NTFjNzMzMGU1MDA3ZDgpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzhmMjJkZmJhMGNmNTQ4NWRhYjYwNjU5ZDJiNzFkNTQ0ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjY1ODU5OSwgLTc5LjM4MzE1OTkwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzM4OTQxMWVhYzRkZjRiMTJiY2U2OGUyMzM2MDg0ZmMyID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF85OGZkYmY2NzE5MzI0MTdiOGM4ZTgxNTc5MTYwYjRmYiA9ICQoYDxkaXYgaWQ9Imh0bWxfOThmZGJmNjcxOTMyNDE3YjhjOGU4MTU3OTE2MGI0ZmIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNodXJjaCBhbmQgV2VsbGVzbGV5LCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzM4OTQxMWVhYzRkZjRiMTJiY2U2OGUyMzM2MDg0ZmMyLnNldENvbnRlbnQoaHRtbF85OGZkYmY2NzE5MzI0MTdiOGM4ZTgxNTc5MTYwYjRmYik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfOGYyMmRmYmEwY2Y1NDg1ZGFiNjA2NTlkMmI3MWQ1NDQuYmluZFBvcHVwKHBvcHVwXzM4OTQxMWVhYzRkZjRiMTJiY2U2OGUyMzM2MDg0ZmMyKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9iMjJhZDk1ZjM0MGU0N2IwYjcwNzc5OGVlMjU0Y2FjMyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1NDI1OTksIC03OS4zNjA2MzU5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzdmMjFiZjQxMGYwMjQ4MWRiYzU2MGI5NmE5YTRhYWJkID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF82NTQ3YTRiMzZjMmE0N2FjODljOTE5NzIwNmE0Zjg3YSA9ICQoYDxkaXYgaWQ9Imh0bWxfNjU0N2E0YjM2YzJhNDdhYzg5YzkxOTcyMDZhNGY4N2EiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhhcmJvdXJmcm9udCxSZWdlbnQgUGFyaywgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83ZjIxYmY0MTBmMDI0ODFkYmM1NjBiOTZhOWE0YWFiZC5zZXRDb250ZW50KGh0bWxfNjU0N2E0YjM2YzJhNDdhYzg5YzkxOTcyMDZhNGY4N2EpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2IyMmFkOTVmMzQwZTQ3YjBiNzA3Nzk4ZWUyNTRjYWMzLmJpbmRQb3B1cChwb3B1cF83ZjIxYmY0MTBmMDI0ODFkYmM1NjBiOTZhOWE0YWFiZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzQ3MTFhMWZiZTllNDUwZWE2ZjVjOGZjMjUzZWI5MTEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTcxNjE4LCAtNzkuMzc4OTM3MDk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNjMwZmVlNDQ0MDlkNGE0ZThmNjg1NTc0NTIwZTNmZGMgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzMwNzRiY2QzOTMwZjQ4YjNhODU1NzFlZTc5NTc0NWZkID0gJChgPGRpdiBpZD0iaHRtbF8zMDc0YmNkMzkzMGY0OGIzYTg1NTcxZWU3OTU3NDVmZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UnllcnNvbixHYXJkZW4gRGlzdHJpY3QsIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNjMwZmVlNDQ0MDlkNGE0ZThmNjg1NTc0NTIwZTNmZGMuc2V0Q29udGVudChodG1sXzMwNzRiY2QzOTMwZjQ4YjNhODU1NzFlZTc5NTc0NWZkKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8zNDcxMWExZmJlOWU0NTBlYTZmNWM4ZmMyNTNlYjkxMS5iaW5kUG9wdXAocG9wdXBfNjMwZmVlNDQ0MDlkNGE0ZThmNjg1NTc0NTIwZTNmZGMpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzFiNDNhZTVhODBjMzQ1NWM5NjE5NmNlYWM4YjQ1MDdjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjUxNDkzOSwgLTc5LjM3NTQxNzldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZGFhYzc1ZDBhY2U2NGQ2YzljZjc0MDM1NGQ0MWE0ODUgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2FmNDk5MzBiNzgwZjRmMjE5NzcxN2YwOTVmMmM4ODg0ID0gJChgPGRpdiBpZD0iaHRtbF9hZjQ5OTMwYjc4MGY0ZjIxOTc3MTdmMDk1ZjJjODg4NCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+U3QuIEphbWVzIFRvd24sIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfZGFhYzc1ZDBhY2U2NGQ2YzljZjc0MDM1NGQ0MWE0ODUuc2V0Q29udGVudChodG1sX2FmNDk5MzBiNzgwZjRmMjE5NzcxN2YwOTVmMmM4ODg0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8xYjQzYWU1YTgwYzM0NTVjOTYxOTZjZWFjOGI0NTA3Yy5iaW5kUG9wdXAocG9wdXBfZGFhYzc1ZDBhY2U2NGQ2YzljZjc0MDM1NGQ0MWE0ODUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzJmZDZiMGJkYmIyMjQzODY4Yzg5ZDk4OWI4YjA1NzNmID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQ0NzcwNzk5OTk5OTk2LCAtNzkuMzczMzA2NF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8zMzBmNzZiZjliYmY0NTlhYTFhMzMwMTk3MWNiNGEzNiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYTA2YWY2OGZjZTgyNGFjMjkyYjAzYTdmMzAwY2RkZTggPSAkKGA8ZGl2IGlkPSJodG1sX2EwNmFmNjhmY2U4MjRhYzI5MmIwM2E3ZjMwMGNkZGU4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CZXJjenkgUGFyaywgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8zMzBmNzZiZjliYmY0NTlhYTFhMzMwMTk3MWNiNGEzNi5zZXRDb250ZW50KGh0bWxfYTA2YWY2OGZjZTgyNGFjMjkyYjAzYTdmMzAwY2RkZTgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzJmZDZiMGJkYmIyMjQzODY4Yzg5ZDk4OWI4YjA1NzNmLmJpbmRQb3B1cChwb3B1cF8zMzBmNzZiZjliYmY0NTlhYTFhMzMwMTk3MWNiNGEzNikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZmI2MGZiOWE0OTI5NDZjY2IzOWYzOWJiNjE4YmVmMjggPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTc5NTI0LCAtNzkuMzg3MzgyNl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF83ZmRiYjBlYjYwZWU0MWJmOWRhYTZhNjU1MWY2YTViYiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMzM5YTdmMTc0NzYyNGY3YjhiMGI5MjQxZjMyMjUwMzkgPSAkKGA8ZGl2IGlkPSJodG1sXzMzOWE3ZjE3NDc2MjRmN2I4YjBiOTI0MWYzMjI1MDM5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DZW50cmFsIEJheSBTdHJlZXQsIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfN2ZkYmIwZWI2MGVlNDFiZjlkYWE2YTY1NTFmNmE1YmIuc2V0Q29udGVudChodG1sXzMzOWE3ZjE3NDc2MjRmN2I4YjBiOTI0MWYzMjI1MDM5KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9mYjYwZmI5YTQ5Mjk0NmNjYjM5ZjM5YmI2MThiZWYyOC5iaW5kUG9wdXAocG9wdXBfN2ZkYmIwZWI2MGVlNDFiZjlkYWE2YTY1NTFmNmE1YmIpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2NmN2I3OTE1Y2NhZTQzNGVhMTU3MGY0Y2VkYTQzNTk5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjUwNTcxMjAwMDAwMDEsIC03OS4zODQ1Njc1XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzFiODhmMzY2M2M5OTRhY2Y4YWVlN2RlY2Y3NzZjNTgzID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83MTMzYWM2YmJkMjk0NDgzODc0OTNkMTk5YWQzYTc3YSA9ICQoYDxkaXYgaWQ9Imh0bWxfNzEzM2FjNmJiZDI5NDQ4Mzg3NDkzZDE5OWFkM2E3N2EiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkFkZWxhaWRlLEtpbmcsUmljaG1vbmQsIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMWI4OGYzNjYzYzk5NGFjZjhhZWU3ZGVjZjc3NmM1ODMuc2V0Q29udGVudChodG1sXzcxMzNhYzZiYmQyOTQ0ODM4NzQ5M2QxOTlhZDNhNzdhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9jZjdiNzkxNWNjYWU0MzRlYTE1NzBmNGNlZGE0MzU5OS5iaW5kUG9wdXAocG9wdXBfMWI4OGYzNjYzYzk5NGFjZjhhZWU3ZGVjZjc3NmM1ODMpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2ZiNmQwYzU4ZWRmMzQwMTU5YzkyNWE0ODVlOGU3YWM5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQwODE1NywgLTc5LjM4MTc1MjI5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzliOGQ0M2Q2NjZhNzQ1ZTBiZjk0ZDU0NGEzY2RjMzRiID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9jMzM5MDZlNjdlZTU0MTQyOTI2YjkxOTVlN2Q5MWJhOSA9ICQoYDxkaXYgaWQ9Imh0bWxfYzMzOTA2ZTY3ZWU1NDE0MjkyNmI5MTk1ZTdkOTFiYTkiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhhcmJvdXJmcm9udCBFYXN0LFRvcm9udG8gSXNsYW5kcyxVbmlvbiBTdGF0aW9uLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzliOGQ0M2Q2NjZhNzQ1ZTBiZjk0ZDU0NGEzY2RjMzRiLnNldENvbnRlbnQoaHRtbF9jMzM5MDZlNjdlZTU0MTQyOTI2YjkxOTVlN2Q5MWJhOSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZmI2ZDBjNThlZGYzNDAxNTljOTI1YTQ4NWU4ZTdhYzkuYmluZFBvcHVwKHBvcHVwXzliOGQ0M2Q2NjZhNzQ1ZTBiZjk0ZDU0NGEzY2RjMzRiKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lYWNkYzFiMTM3ODQ0MDk5YmRiYzQ5NDAxMjU4OTI2ZSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0NzE3NjgsIC03OS4zODE1NzY0MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF82ZjYzMmQyZGExZjQ0YjEyYjNmNTUyZjg3NGM5YmMwYSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNzJjNTgxMGJjMGZlNDZlNzk1MjI2YjBhMWI4MGI2ZTUgPSAkKGA8ZGl2IGlkPSJodG1sXzcyYzU4MTBiYzBmZTQ2ZTc5NTIyNmIwYTFiODBiNmU1IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5EZXNpZ24gRXhjaGFuZ2UsVG9yb250byBEb21pbmlvbiBDZW50cmUsIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNmY2MzJkMmRhMWY0NGIxMmIzZjU1MmY4NzRjOWJjMGEuc2V0Q29udGVudChodG1sXzcyYzU4MTBiYzBmZTQ2ZTc5NTIyNmIwYTFiODBiNmU1KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9lYWNkYzFiMTM3ODQ0MDk5YmRiYzQ5NDAxMjU4OTI2ZS5iaW5kUG9wdXAocG9wdXBfNmY2MzJkMmRhMWY0NGIxMmIzZjU1MmY4NzRjOWJjMGEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzczMmMwMTQ3YjY1MTRhMjg5YmQ0OTc4MGE3Nzg2Nzg5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQ4MTk4NSwgLTc5LjM3OTgxNjkwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzk3MTc0NzI5OTIwZDQ1YTk5N2YzMDIwNjU3MzdjYzY0ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8zNzE2OWUwOGU0MjE0NjIyODNiMDU2ZDYxMjVlYjA4NSA9ICQoYDxkaXYgaWQ9Imh0bWxfMzcxNjllMDhlNDIxNDYyMjgzYjA1NmQ2MTI1ZWIwODUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNvbW1lcmNlIENvdXJ0LFZpY3RvcmlhIEhvdGVsLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzk3MTc0NzI5OTIwZDQ1YTk5N2YzMDIwNjU3MzdjYzY0LnNldENvbnRlbnQoaHRtbF8zNzE2OWUwOGU0MjE0NjIyODNiMDU2ZDYxMjVlYjA4NSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNzMyYzAxNDdiNjUxNGEyODliZDQ5NzgwYTc3ODY3ODkuYmluZFBvcHVwKHBvcHVwXzk3MTc0NzI5OTIwZDQ1YTk5N2YzMDIwNjU3MzdjYzY0KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9kNTE1MzAwMTExMjU0MWQ0ODAxMDRiMGVhMzkzMjgxNCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcxMTY5NDgsIC03OS40MTY5MzU1OTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF81YzQ5ZjY1NTFlZWM0N2I1ODY4YzFkM2QyNDUzYWQ0YyA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNmRlMDMzZTRmNjU5NDJkOTkwNTE3OTVhMzdkYzIwMjggPSAkKGA8ZGl2IGlkPSJodG1sXzZkZTAzM2U0ZjY1OTQyZDk5MDUxNzk1YTM3ZGMyMDI4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Sb3NlbGF3biwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzVjNDlmNjU1MWVlYzQ3YjU4NjhjMWQzZDI0NTNhZDRjLnNldENvbnRlbnQoaHRtbF82ZGUwMzNlNGY2NTk0MmQ5OTA1MTc5NWEzN2RjMjAyOCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZDUxNTMwMDExMTI1NDFkNDgwMTA0YjBlYTM5MzI4MTQuYmluZFBvcHVwKHBvcHVwXzVjNDlmNjU1MWVlYzQ3YjU4NjhjMWQzZDI0NTNhZDRjKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8yMGNiNTk1M2I4NTQ0MjgyOGE2MTQ4OGU1YWQ0NjdiMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY5Njk0NzYsIC03OS40MTEzMDcyMDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8yZTJmZDc4ZWYyZjk0MWY2OTkwNmJmZThjZWI4YjMzOSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfOWEwZmE1ZWU5OThiNDE5NDg5MmY4MWJjZTdmOGNjYTQgPSAkKGA8ZGl2IGlkPSJodG1sXzlhMGZhNWVlOTk4YjQxOTQ4OTJmODFiY2U3ZjhjY2E0IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Gb3Jlc3QgSGlsbCBOb3J0aCxGb3Jlc3QgSGlsbCBXZXN0LCBDZW50cmFsIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMmUyZmQ3OGVmMmY5NDFmNjk5MDZiZmU4Y2ViOGIzMzkuc2V0Q29udGVudChodG1sXzlhMGZhNWVlOTk4YjQxOTQ4OTJmODFiY2U3ZjhjY2E0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8yMGNiNTk1M2I4NTQ0MjgyOGE2MTQ4OGU1YWQ0NjdiMi5iaW5kUG9wdXAocG9wdXBfMmUyZmQ3OGVmMmY5NDFmNjk5MDZiZmU4Y2ViOGIzMzkpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzFhMzAyY2NlMGIxMDRiMThhM2EzNDVkZDhhZWMwMjlkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjcyNzA5NywgLTc5LjQwNTY3ODQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2IwMGZjNTkxMDlmZDQwNTFhM2QxY2ZiN2I1ZDc1YmYxID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9mNThhYzY2OGFjYjM0MjBkYWE2NTg3MDI0Mjk3NzJkNSA9ICQoYDxkaXYgaWQ9Imh0bWxfZjU4YWM2NjhhY2IzNDIwZGFhNjU4NzAyNDI5NzcyZDUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRoZSBBbm5leCxOb3J0aCBNaWR0b3duLFlvcmt2aWxsZSwgQ2VudHJhbCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2IwMGZjNTkxMDlmZDQwNTFhM2QxY2ZiN2I1ZDc1YmYxLnNldENvbnRlbnQoaHRtbF9mNThhYzY2OGFjYjM0MjBkYWE2NTg3MDI0Mjk3NzJkNSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMWEzMDJjY2UwYjEwNGIxOGEzYTM0NWRkOGFlYzAyOWQuYmluZFBvcHVwKHBvcHVwX2IwMGZjNTkxMDlmZDQwNTFhM2QxY2ZiN2I1ZDc1YmYxKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81MmE1N2FlMDJjNzE0ODgwYTlmMDhhYTMyMzhiOTMyYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2MjY5NTYsIC03OS40MDAwNDkzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzkzNGU3ODA3YTlhZjQ5MGZhMmU5NjBlZjY3ZGFjMThmID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF81ZmJhMWE1NWU5M2I0NTY3YjI1ZjdjYTg3ZjBkN2VlYiA9ICQoYDxkaXYgaWQ9Imh0bWxfNWZiYTFhNTVlOTNiNDU2N2IyNWY3Y2E4N2YwZDdlZWIiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhhcmJvcmQsVW5pdmVyc2l0eSBvZiBUb3JvbnRvLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzkzNGU3ODA3YTlhZjQ5MGZhMmU5NjBlZjY3ZGFjMThmLnNldENvbnRlbnQoaHRtbF81ZmJhMWE1NWU5M2I0NTY3YjI1ZjdjYTg3ZjBkN2VlYik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNTJhNTdhZTAyYzcxNDg4MGE5ZjA4YWEzMjM4YjkzMmIuYmluZFBvcHVwKHBvcHVwXzkzNGU3ODA3YTlhZjQ5MGZhMmU5NjBlZjY3ZGFjMThmKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lZGU2MWIwNzg3Yzc0Njc3ODQyNDllYzFkNzY0NTUxMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1MzIwNTcsIC03OS40MDAwNDkzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzU4Mjg0ZDQ0NDU2YzQwNDg5NjgyOGJlNGJkMmNmOGIwID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9jM2I3YmY2ODg5ZDU0NDVhODM5YjRhMDc3YWVjMDMwMCA9ICQoYDxkaXYgaWQ9Imh0bWxfYzNiN2JmNjg4OWQ1NDQ1YTgzOWI0YTA3N2FlYzAzMDAiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNoaW5hdG93bixHcmFuZ2UgUGFyayxLZW5zaW5ndG9uIE1hcmtldCwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81ODI4NGQ0NDQ1NmM0MDQ4OTY4MjhiZTRiZDJjZjhiMC5zZXRDb250ZW50KGh0bWxfYzNiN2JmNjg4OWQ1NDQ1YTgzOWI0YTA3N2FlYzAzMDApOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2VkZTYxYjA3ODdjNzQ2Nzc4NDI0OWVjMWQ3NjQ1NTEyLmJpbmRQb3B1cChwb3B1cF81ODI4NGQ0NDQ1NmM0MDQ4OTY4MjhiZTRiZDJjZjhiMCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNzRmMDQ0MzU0MGM1NDk5N2IxNGE3YzM0NjlhYmFjYzYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Mjg5NDY3LCAtNzkuMzk0NDE5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF80M2FlMDRjOTVlMTM0YWI2ODgyMjY3MmYyMDU0Y2EwNCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMGJhMTk4MzdlODM0NDA4MjlhOGJkYzNmNGQzMTFkZDUgPSAkKGA8ZGl2IGlkPSJodG1sXzBiYTE5ODM3ZTgzNDQwODI5YThiZGMzZjRkMzExZGQ1IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DTiBUb3dlcixCYXRodXJzdCBRdWF5LElzbGFuZCBhaXJwb3J0LEhhcmJvdXJmcm9udCBXZXN0LEtpbmcgYW5kIFNwYWRpbmEsUmFpbHdheSBMYW5kcyxTb3V0aCBOaWFnYXJhLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzQzYWUwNGM5NWUxMzRhYjY4ODIyNjcyZjIwNTRjYTA0LnNldENvbnRlbnQoaHRtbF8wYmExOTgzN2U4MzQ0MDgyOWE4YmRjM2Y0ZDMxMWRkNSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNzRmMDQ0MzU0MGM1NDk5N2IxNGE3YzM0NjlhYmFjYzYuYmluZFBvcHVwKHBvcHVwXzQzYWUwNGM5NWUxMzRhYjY4ODIyNjcyZjIwNTRjYTA0KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mZTM3NTQwZWYzNGY0N2E5OWMzYmM3Y2M1ZmFhMmM1YyA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0NjQzNTIsIC03OS4zNzQ4NDU5OTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF9hMWM3YzczY2Q3OWQ0ODA2YWUwNjgxMTBhMDJkZWE4NCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNmI2NjQwODJjZWNiNDdlYThlODkyYTJmYThkMDg3MzMgPSAkKGA8ZGl2IGlkPSJodG1sXzZiNjY0MDgyY2VjYjQ3ZWE4ZTg5MmEyZmE4ZDA4NzMzIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TdG4gQSBQTyBCb3hlcyAyNSBUaGUgRXNwbGFuYWRlLCBEb3dudG93biBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2ExYzdjNzNjZDc5ZDQ4MDZhZTA2ODExMGEwMmRlYTg0LnNldENvbnRlbnQoaHRtbF82YjY2NDA4MmNlY2I0N2VhOGU4OTJhMmZhOGQwODczMyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZmUzNzU0MGVmMzRmNDdhOTljM2JjN2NjNWZhYTJjNWMuYmluZFBvcHVwKHBvcHVwX2ExYzdjNzNjZDc5ZDQ4MDZhZTA2ODExMGEwMmRlYTg0KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8xYjU1Zjc2YzE5OWM0NzVjOTUyYmUwM2FkNmFjN2ZmZSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0ODQyOTIsIC03OS4zODIyODAyXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzBiMDNiMjk0Y2JjMDQwYzZiMWFiMmRjODhlYzI3OWYzID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83MGU0MDE1ZGUxYzY0MmExODM1OTFhNDMzODk1MjVhMSA9ICQoYDxkaXYgaWQ9Imh0bWxfNzBlNDAxNWRlMWM2NDJhMTgzNTkxYTQzMzg5NTI1YTEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkZpcnN0IENhbmFkaWFuIFBsYWNlLFVuZGVyZ3JvdW5kIGNpdHksIERvd250b3duIFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMGIwM2IyOTRjYmMwNDBjNmIxYWIyZGM4OGVjMjc5ZjMuc2V0Q29udGVudChodG1sXzcwZTQwMTVkZTFjNjQyYTE4MzU5MWE0MzM4OTUyNWExKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8xYjU1Zjc2YzE5OWM0NzVjOTUyYmUwM2FkNmFjN2ZmZS5iaW5kUG9wdXAocG9wdXBfMGIwM2IyOTRjYmMwNDBjNmIxYWIyZGM4OGVjMjc5ZjMpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzQwMmNiOWViNTlkODQwN2Y5YzlkNmI0MTQ1NTU4MjgzID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjY5NTQyLCAtNzkuNDIyNTYzN10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF84YTUwMjk4NjliZjM0MGMwYjFjYmIxOTUxZGY1YTE1YSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfODA2Y2I3NWMyNTRkNDZkMDhmMTdiYTBmYTUyODY3YzggPSAkKGA8ZGl2IGlkPSJodG1sXzgwNmNiNzVjMjU0ZDQ2ZDA4ZjE3YmEwZmE1Mjg2N2M4IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DaHJpc3RpZSwgRG93bnRvd24gVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF84YTUwMjk4NjliZjM0MGMwYjFjYmIxOTUxZGY1YTE1YS5zZXRDb250ZW50KGh0bWxfODA2Y2I3NWMyNTRkNDZkMDhmMTdiYTBmYTUyODY3YzgpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzQwMmNiOWViNTlkODQwN2Y5YzlkNmI0MTQ1NTU4MjgzLmJpbmRQb3B1cChwb3B1cF84YTUwMjk4NjliZjM0MGMwYjFjYmIxOTUxZGY1YTE1YSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZmYzZDUyOWI3ZTgyNGQyOGIzMTdmNGMyMjI4YWMxMjIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjkwMDUxMDAwMDAwMSwgLTc5LjQ0MjI1OTNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYzQ3YTQxOGE3YWJjNDAyMDkwOTI1OWIwZmQwNzU3NGYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzJjODIyZTZiZDg5ZDQ4NDliNGZkOThmMDg3ZTZjN2YxID0gJChgPGRpdiBpZD0iaHRtbF8yYzgyMmU2YmQ4OWQ0ODQ5YjRmZDk4ZjA4N2U2YzdmMSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RG92ZXJjb3VydCBWaWxsYWdlLER1ZmZlcmluLCBXZXN0IFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfYzQ3YTQxOGE3YWJjNDAyMDkwOTI1OWIwZmQwNzU3NGYuc2V0Q29udGVudChodG1sXzJjODIyZTZiZDg5ZDQ4NDliNGZkOThmMDg3ZTZjN2YxKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9mZjNkNTI5YjdlODI0ZDI4YjMxN2Y0YzIyMjhhYzEyMi5iaW5kUG9wdXAocG9wdXBfYzQ3YTQxOGE3YWJjNDAyMDkwOTI1OWIwZmQwNzU3NGYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2IxMmNiMmYyNzcxNzRhOWViM2YyODljOWYxMWE1MmU5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQ3OTI2NzAwMDAwMDA2LCAtNzkuNDE5NzQ5N10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF81NzI1MmQwMGY2OWE0NDUyYWFlZmMxOGFlYzFmODI4OCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfODVlNmM3ZTYwYWQwNGJjNzhiYTRhYTRmM2ZiOTliNjAgPSAkKGA8ZGl2IGlkPSJodG1sXzg1ZTZjN2U2MGFkMDRiYzc4YmE0YWE0ZjNmYjk5YjYwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5MaXR0bGUgUG9ydHVnYWwsVHJpbml0eSwgV2VzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzU3MjUyZDAwZjY5YTQ0NTJhYWVmYzE4YWVjMWY4Mjg4LnNldENvbnRlbnQoaHRtbF84NWU2YzdlNjBhZDA0YmM3OGJhNGFhNGYzZmI5OWI2MCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfYjEyY2IyZjI3NzE3NGE5ZWIzZjI4OWM5ZjExYTUyZTkuYmluZFBvcHVwKHBvcHVwXzU3MjUyZDAwZjY5YTQ0NTJhYWVmYzE4YWVjMWY4Mjg4KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81Y2NjOGM4NjhjYzc0NDgwOGI1MzYyY2E2ODJkYWUwMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjYzNjg0NzIsIC03OS40MjgxOTE0MDAwMDAwMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiYmx1ZSIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjMzE4NmNjIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzJjYjI4OGM2YjU1YTRmYjFiOWZiMzA2ZDhlNGRjOWRlKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8yNWZlZTczMzUzNjY0OWM4OWZjOTZhY2NjOTA4ZWQyZiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYWVlNWEwNGM5NjE1NDE3N2EyYWUyNDdlMmJjNGQ5N2QgPSAkKGA8ZGl2IGlkPSJodG1sX2FlZTVhMDRjOTYxNTQxNzdhMmFlMjQ3ZTJiYzRkOTdkIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Ccm9ja3RvbixFeGhpYml0aW9uIFBsYWNlLFBhcmtkYWxlIFZpbGxhZ2UsIFdlc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8yNWZlZTczMzUzNjY0OWM4OWZjOTZhY2NjOTA4ZWQyZi5zZXRDb250ZW50KGh0bWxfYWVlNWEwNGM5NjE1NDE3N2EyYWUyNDdlMmJjNGQ5N2QpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzVjY2M4Yzg2OGNjNzQ0ODA4YjUzNjJjYTY4MmRhZTAyLmJpbmRQb3B1cChwb3B1cF8yNWZlZTczMzUzNjY0OWM4OWZjOTZhY2NjOTA4ZWQyZikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDNmNjJkNWM4NWJlNDZmNGIzYjdjOWZiNzdmZTAzODEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjE2MDgzLCAtNzkuNDY0NzYzMjk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfN2YzNjkyZDNhODVjNDBhYzk0NzcyODNiMDk2MmRjYWQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2Y0OGI0MGYxMGYyMTQyYWI4MjdiYTI1YmM4YmZlMzc2ID0gJChgPGRpdiBpZD0iaHRtbF9mNDhiNDBmMTBmMjE0MmFiODI3YmEyNWJjOGJmZTM3NiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+SGlnaCBQYXJrLFRoZSBKdW5jdGlvbiBTb3V0aCwgV2VzdCBUb3JvbnRvPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzdmMzY5MmQzYTg1YzQwYWM5NDc3MjgzYjA5NjJkY2FkLnNldENvbnRlbnQoaHRtbF9mNDhiNDBmMTBmMjE0MmFiODI3YmEyNWJjOGJmZTM3Nik7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMDNmNjJkNWM4NWJlNDZmNGIzYjdjOWZiNzdmZTAzODEuYmluZFBvcHVwKHBvcHVwXzdmMzY5MmQzYTg1YzQwYWM5NDc3MjgzYjA5NjJkY2FkKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8xZDc3ZmJhZTRkYzU0NzZiOWY4ZjhhNmJhYjc0MzFhMCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0ODk1OTcsIC03OS40NTYzMjVdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNWEwZDMzMWY2MGY4NDY2MWI5YWMzMzhlNDViNDA1Y2UgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQxZDJmNTg3Mzk2MjQ3NGM5ODY2MjE1ZTQwYmQ1ZTBlID0gJChgPGRpdiBpZD0iaHRtbF80MWQyZjU4NzM5NjI0NzRjOTg2NjIxNWU0MGJkNWUwZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UGFya2RhbGUsUm9uY2VzdmFsbGVzLCBXZXN0IFRvcm9udG88L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNWEwZDMzMWY2MGY4NDY2MWI5YWMzMzhlNDViNDA1Y2Uuc2V0Q29udGVudChodG1sXzQxZDJmNTg3Mzk2MjQ3NGM5ODY2MjE1ZTQwYmQ1ZTBlKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8xZDc3ZmJhZTRkYzU0NzZiOWY4ZjhhNmJhYjc0MzFhMC5iaW5kUG9wdXAocG9wdXBfNWEwZDMzMWY2MGY4NDY2MWI5YWMzMzhlNDViNDA1Y2UpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzdhMzRiN2E0OTI2YTQ5ZGNiZDAyNWMxZjU3NDExM2RiID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjUxNTcwNiwgLTc5LjQ4NDQ0OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogImJsdWUiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzMxODZjYyIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8yY2IyODhjNmI1NWE0ZmIxYjlmYjMwNmQ4ZTRkYzlkZSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYTdiM2RmYjY1OWZhNGM5Nzk1MDY5MzFhOGJlZjBjYTIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzdiNDE0MGQxZTk3MzRhODQ4ZDgwNTg2MDQ3MzMyMjZhID0gJChgPGRpdiBpZD0iaHRtbF83YjQxNDBkMWU5NzM0YTg0OGQ4MDU4NjA0NzMzMjI2YSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UnVubnltZWRlLFN3YW5zZWEsIFdlc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9hN2IzZGZiNjU5ZmE0Yzk3OTUwNjkzMWE4YmVmMGNhMi5zZXRDb250ZW50KGh0bWxfN2I0MTQwZDFlOTczNGE4NDhkODA1ODYwNDczMzIyNmEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzdhMzRiN2E0OTI2YTQ5ZGNiZDAyNWMxZjU3NDExM2RiLmJpbmRQb3B1cChwb3B1cF9hN2IzZGZiNjU5ZmE0Yzk3OTUwNjkzMWE4YmVmMGNhMikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTU3ZTk5YjNiMTU1NDRhY2IwY2E3NjZhOGUzODljOTAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjI3NDM5LCAtNzkuMzIxNTU4XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICJibHVlIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMzMTg2Y2MiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMmNiMjg4YzZiNTVhNGZiMWI5ZmIzMDZkOGU0ZGM5ZGUpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzM3OTYyNmE4NDUzMzQ4MTJiZDc3YzE2NWY5Yjg1Zjk2ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83YTVjNzVkMWZhZmI0MTA2YmM2MjE0Njc5OWUxYWJhNiA9ICQoYDxkaXYgaWQ9Imh0bWxfN2E1Yzc1ZDFmYWZiNDEwNmJjNjIxNDY3OTllMWFiYTYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJ1c2luZXNzIFJlcGx5IE1haWwgUHJvY2Vzc2luZyBDZW50cmUgOTY5IEVhc3Rlcm4sIEVhc3QgVG9yb250bzwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8zNzk2MjZhODQ1MzM0ODEyYmQ3N2MxNjVmOWI4NWY5Ni5zZXRDb250ZW50KGh0bWxfN2E1Yzc1ZDFmYWZiNDEwNmJjNjIxNDY3OTllMWFiYTYpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2E1N2U5OWIzYjE1NTQ0YWNiMGNhNzY2YThlMzg5YzkwLmJpbmRQb3B1cChwb3B1cF8zNzk2MjZhODQ1MzM0ODEyYmQ3N2MxNjVmOWI4NWY5NikKICAgICAgICA7CgogICAgICAgIAogICAgCjwvc2NyaXB0Pg==" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```python
CLIENT_ID = 'NR0R1IZ4DS1Y3U5QMZN2EHIWQNNR1XA4453ZRBIFDLEQF0NS' # your Foursquare ID
CLIENT_SECRET = 'AT2GTM11V15V2NBTXJAY1BUPE0M0Y1UD4E0UGF5KHFXTK1M4' # your Foursquare Secret
VERSION = '20180605' # Foursquare API version

print('Your credentails:')
print('CLIENT_ID: ' + CLIENT_ID)
print('CLIENT_SECRET:' + CLIENT_SECRET)
```

    Your credentails:
    CLIENT_ID: NR0R1IZ4DS1Y3U5QMZN2EHIWQNNR1XA4453ZRBIFDLEQF0NS
    CLIENT_SECRET:AT2GTM11V15V2NBTXJAY1BUPE0M0Y1UD4E0UGF5KHFXTK1M4


### Explore first neighborhood in dataframe


```python
visualise_df.loc[0,'Neighbourhood']
```




    'The Beaches'



### Get Lat and Long of 'The Beaches'


```python
neighborhood_latitude = visualise_df.loc[0, 'Latitude'] # neighborhood latitude value
neighborhood_longitude = visualise_df.loc[0, 'Longitude'] # neighborhood longitude value

neighborhood_name = visualise_df.loc[0, 'Neighbourhood'] # neighborhood name

print('Latitude and longitude values of {} are {}, {}.'.format(neighborhood_name, 
                                                               neighborhood_latitude, 
                                                               neighborhood_longitude))
```

    Latitude and longitude values of The Beaches are 43.67635739999999, -79.2930312.


### Get the top 100 venues in 'The beaches' within a radius of 500 metres


```python
# type your answer here
LIMIT = 100 # limit of number of venues returned by Foursquare API
radius = 500 # define radius
url = 'https://api.foursquare.com/v2/venues/explore?&client_id={}&client_secret={}&v={}&ll={},{}&radius={}&limit={}'.format(
    CLIENT_ID, 
    CLIENT_SECRET, 
    VERSION, 
    neighborhood_latitude, 
    neighborhood_longitude, 
    radius, 
    LIMIT)
url # display URL
```




    'https://api.foursquare.com/v2/venues/explore?&client_id=NR0R1IZ4DS1Y3U5QMZN2EHIWQNNR1XA4453ZRBIFDLEQF0NS&client_secret=AT2GTM11V15V2NBTXJAY1BUPE0M0Y1UD4E0UGF5KHFXTK1M4&v=20180605&ll=43.67635739999999,-79.2930312&radius=500&limit=100'




```python
results = requests.get(url).json()
results
```




    {'meta': {'code': 200, 'requestId': '5db2cad85315930039af6255'},
     'response': {'headerLocation': 'The Beaches',
      'headerFullLocation': 'The Beaches, Toronto',
      'headerLocationGranularity': 'neighborhood',
      'totalResults': 5,
      'suggestedBounds': {'ne': {'lat': 43.680857404499996,
        'lng': -79.28682091449052},
       'sw': {'lat': 43.67185739549999, 'lng': -79.29924148550948}},
      'groups': [{'type': 'Recommended Places',
        'name': 'recommended',
        'items': [{'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4bd461bc77b29c74a07d9282',
           'name': 'Glen Manor Ravine',
           'location': {'address': 'Glen Manor',
            'crossStreet': 'Queen St.',
            'lat': 43.67682094413784,
            'lng': -79.29394208780985,
            'labeledLatLngs': [{'label': 'display',
              'lat': 43.67682094413784,
              'lng': -79.29394208780985}],
            'distance': 89,
            'cc': 'CA',
            'city': 'Toronto',
            'state': 'ON',
            'country': 'Canada',
            'formattedAddress': ['Glen Manor (Queen St.)',
             'Toronto ON',
             'Canada']},
           'categories': [{'id': '4bf58dd8d48988d159941735',
             'name': 'Trail',
             'pluralName': 'Trails',
             'shortName': 'Trail',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/hikingtrail_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4bd461bc77b29c74a07d9282-0'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4ad4c062f964a52011f820e3',
           'name': 'The Big Carrot Natural Food Market',
           'location': {'address': '125 Southwood Dr',
            'lat': 43.678879,
            'lng': -79.297734,
            'labeledLatLngs': [{'label': 'display',
              'lat': 43.678879,
              'lng': -79.297734}],
            'distance': 471,
            'postalCode': 'M4E 0B8',
            'cc': 'CA',
            'city': 'Toronto',
            'state': 'ON',
            'country': 'Canada',
            'formattedAddress': ['125 Southwood Dr',
             'Toronto ON M4E 0B8',
             'Canada']},
           'categories': [{'id': '50aa9e744b90af0d42d5de0e',
             'name': 'Health Food Store',
             'pluralName': 'Health Food Stores',
             'shortName': 'Health Food Store',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/food_grocery_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []},
           'venuePage': {'id': '75150878'}},
          'referralId': 'e-0-4ad4c062f964a52011f820e3-1'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4b8daea1f964a520480833e3',
           'name': 'Grover Pub and Grub',
           'location': {'address': '676 Kingston Rd.',
            'crossStreet': 'at Main St.',
            'lat': 43.679181434941015,
            'lng': -79.29721535878515,
            'labeledLatLngs': [{'label': 'display',
              'lat': 43.679181434941015,
              'lng': -79.29721535878515}],
            'distance': 460,
            'postalCode': 'M4E 1R4',
            'cc': 'CA',
            'city': 'Toronto',
            'state': 'ON',
            'country': 'Canada',
            'formattedAddress': ['676 Kingston Rd. (at Main St.)',
             'Toronto ON M4E 1R4',
             'Canada']},
           'categories': [{'id': '4bf58dd8d48988d11b941735',
             'name': 'Pub',
             'pluralName': 'Pubs',
             'shortName': 'Pub',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/nightlife/pub_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4b8daea1f964a520480833e3-2'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '56afcad6498e05333bf42031',
           'name': 'Glen Stewart Ravine',
           'location': {'lat': 43.67629984029563,
            'lng': -79.2947841389563,
            'labeledLatLngs': [{'label': 'display',
              'lat': 43.67629984029563,
              'lng': -79.2947841389563}],
            'distance': 141,
            'cc': 'CA',
            'country': 'Canada',
            'formattedAddress': ['Canada']},
           'categories': [{'id': '4bf58dd8d48988d162941735',
             'name': 'Other Great Outdoors',
             'pluralName': 'Other Great Outdoors',
             'shortName': 'Other Outdoors',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/outdoors_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-56afcad6498e05333bf42031-3'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4df91c4bae60f95f82229ad5',
           'name': 'Upper Beaches',
           'location': {'lat': 43.68056321147582,
            'lng': -79.2928688743688,
            'labeledLatLngs': [{'label': 'display',
              'lat': 43.68056321147582,
              'lng': -79.2928688743688}],
            'distance': 468,
            'cc': 'CA',
            'city': 'Toronto',
            'state': 'ON',
            'country': 'Canada',
            'formattedAddress': ['Toronto ON', 'Canada']},
           'categories': [{'id': '4f2a25ac4b909258e854f55f',
             'name': 'Neighborhood',
             'pluralName': 'Neighborhoods',
             'shortName': 'Neighborhood',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/neighborhood_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4df91c4bae60f95f82229ad5-4'}]}]}}




```python
# function that extracts the category of the venue
def get_category_type(row):
    try:
        categories_list = row['categories']
    except:
        categories_list = row['venue.categories']
        
    if len(categories_list) == 0:
        return None
    else:
        return categories_list[0]['name']
```


```python
import requests # library to handle requests
from pandas.io.json import json_normalize # tranform JSON file into a pandas dataframe

venues = results['response']['groups'][0]['items']
    
nearby_venues = json_normalize(venues) # flatten JSON

# filter columns
filtered_columns = ['venue.name', 'venue.categories', 'venue.location.lat', 'venue.location.lng']
nearby_venues =nearby_venues.loc[:, filtered_columns]

# filter the category for each row
nearby_venues['venue.categories'] = nearby_venues.apply(get_category_type, axis=1)

# clean columns
nearby_venues.columns = [col.split(".")[-1] for col in nearby_venues.columns]

nearby_venues.head()
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
      <th>name</th>
      <th>categories</th>
      <th>lat</th>
      <th>lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Glen Manor Ravine</td>
      <td>Trail</td>
      <td>43.676821</td>
      <td>-79.293942</td>
    </tr>
    <tr>
      <th>1</th>
      <td>The Big Carrot Natural Food Market</td>
      <td>Health Food Store</td>
      <td>43.678879</td>
      <td>-79.297734</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Grover Pub and Grub</td>
      <td>Pub</td>
      <td>43.679181</td>
      <td>-79.297215</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Glen Stewart Ravine</td>
      <td>Other Great Outdoors</td>
      <td>43.676300</td>
      <td>-79.294784</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Upper Beaches</td>
      <td>Neighborhood</td>
      <td>43.680563</td>
      <td>-79.292869</td>
    </tr>
  </tbody>
</table>
</div>




```python
print('{} venues were returned by Foursquare.'.format(nearby_venues.shape[0]))
```

    5 venues were returned by Foursquare.


### Repeat for all Neighbourhoods in Toronto


```python
def getNearbyVenues(names, latitudes, longitudes, radius=500):
    
    venues_list=[]
    for name, lat, lng in zip(names, latitudes, longitudes):
        print(name)
            
        # create the API request URL
        url = 'https://api.foursquare.com/v2/venues/explore?&client_id={}&client_secret={}&v={}&ll={},{}&radius={}&limit={}'.format(
            CLIENT_ID, 
            CLIENT_SECRET, 
            VERSION, 
            lat, 
            lng, 
            radius, 
            LIMIT)
            
        # make the GET request
        results = requests.get(url).json()["response"]['groups'][0]['items']
        
        # return only relevant information for each nearby venue
        venues_list.append([(
            name, 
            lat, 
            lng, 
            v['venue']['name'], 
            v['venue']['location']['lat'], 
            v['venue']['location']['lng'],  
            v['venue']['categories'][0]['name']) for v in results])

    nearby_venues = pd.DataFrame([item for venue_list in venues_list for item in venue_list])
    nearby_venues.columns = ['Neighborhood', 
                  'Neighborhood Latitude', 
                  'Neighborhood Longitude', 
                  'Venue', 
                  'Venue Latitude', 
                  'Venue Longitude', 
                  'Venue Category']
    
    return(nearby_venues)
```


```python
toronto_venues = getNearbyVenues(names=visualise_df['Neighbourhood'],
                                   latitudes=visualise_df['Latitude'],
                                   longitudes=visualise_df['Longitude']
                                  )

```

    The Beaches
    The Danforth West,Riverdale
    The Beaches West,India Bazaar
    Studio District
    Lawrence Park
    Davisville North
    North Toronto West
    Davisville
    Moore Park,Summerhill East
    Deer Park,Forest Hill SE,Rathnelly,South Hill,Summerhill West
    Rosedale
    Cabbagetown,St. James Town
    Church and Wellesley
    Harbourfront,Regent Park
    Ryerson,Garden District
    St. James Town
    Berczy Park
    Central Bay Street
    Adelaide,King,Richmond
    Harbourfront East,Toronto Islands,Union Station
    Design Exchange,Toronto Dominion Centre
    Commerce Court,Victoria Hotel
    Roselawn
    Forest Hill North,Forest Hill West
    The Annex,North Midtown,Yorkville
    Harbord,University of Toronto
    Chinatown,Grange Park,Kensington Market
    CN Tower,Bathurst Quay,Island airport,Harbourfront West,King and Spadina,Railway Lands,South Niagara
    Stn A PO Boxes 25 The Esplanade
    First Canadian Place,Underground city
    Christie
    Dovercourt Village,Dufferin
    Little Portugal,Trinity
    Brockton,Exhibition Place,Parkdale Village
    High Park,The Junction South
    Parkdale,Roncesvalles
    Runnymede,Swansea
    Business Reply Mail Processing Centre 969 Eastern


### Analyze Neighborhoods


```python
# one hot encoding
toronto_onehot = pd.get_dummies(toronto_venues[['Venue Category']], prefix="", prefix_sep="")

# add neighborhood column back to dataframe
toronto_onehot['Neighborhood'] = toronto_venues['Neighborhood'] 

# move neighborhood column to the first column
fixed_columns = [toronto_onehot.columns[-1]] + list(toronto_onehot.columns[:-1])
toronto_onehot = toronto_onehot[fixed_columns]

toronto_onehot.head()
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
      <th>Yoga Studio</th>
      <th>Airport</th>
      <th>Airport Food Court</th>
      <th>Airport Gate</th>
      <th>Airport Lounge</th>
      <th>Airport Terminal</th>
      <th>American Restaurant</th>
      <th>Arts &amp; Crafts Store</th>
      <th>Asian Restaurant</th>
      <th>Auto Workshop</th>
      <th>...</th>
      <th>Supermarket</th>
      <th>Sushi Restaurant</th>
      <th>Swim School</th>
      <th>Tea Room</th>
      <th>Thai Restaurant</th>
      <th>Theater</th>
      <th>Theme Restaurant</th>
      <th>Trail</th>
      <th>Vegetarian / Vegan Restaurant</th>
      <th>Wine Bar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 114 columns</p>
</div>




```python
toronto_grouped = toronto_onehot.groupby('Neighborhood').mean().reset_index()
toronto_grouped
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
      <th>Neighborhood</th>
      <th>Yoga Studio</th>
      <th>Airport</th>
      <th>Airport Food Court</th>
      <th>Airport Gate</th>
      <th>Airport Lounge</th>
      <th>Airport Terminal</th>
      <th>American Restaurant</th>
      <th>Arts &amp; Crafts Store</th>
      <th>Asian Restaurant</th>
      <th>...</th>
      <th>Supermarket</th>
      <th>Sushi Restaurant</th>
      <th>Swim School</th>
      <th>Tea Room</th>
      <th>Thai Restaurant</th>
      <th>Theater</th>
      <th>Theme Restaurant</th>
      <th>Trail</th>
      <th>Vegetarian / Vegan Restaurant</th>
      <th>Wine Bar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adelaide,King,Richmond</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Berczy Park</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brockton,Exhibition Place,Parkdale Village</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Business Reply Mail Processing Centre 969 Eastern</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CN Tower,Bathurst Quay,Island airport,Harbourf...</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.1</td>
      <td>0.1</td>
      <td>0.2</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cabbagetown,St. James Town</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Central Bay Street</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chinatown,Grange Park,Kensington Market</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Christie</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Church and Wellesley</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Commerce Court,Victoria Hotel</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Davisville</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Davisville North</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Deer Park,Forest Hill SE,Rathnelly,South Hill,...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.1</td>
      <td>0.10</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Design Exchange,Toronto Dominion Centre</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Dovercourt Village,Dufferin</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.1</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>First Canadian Place,Underground city</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Forest Hill North,Forest Hill West</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.25</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.25</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Harbord,University of Toronto</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Harbourfront East,Toronto Islands,Union Station</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.1</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Harbourfront,Regent Park</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>High Park,The Junction South</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Lawrence Park</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Little Portugal,Trinity</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Moore Park,Summerhill East</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>North Toronto West</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Parkdale,Roncesvalles</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Rosedale</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.25</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Roselawn</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Runnymede,Swansea</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.20</td>
      <td>0.000000</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Ryerson,Garden District</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>St. James Town</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Stn A PO Boxes 25 The Esplanade</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.1</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Studio District</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>34</th>
      <td>The Annex,North Midtown,Yorkville</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>The Beaches</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.20</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>36</th>
      <td>The Beaches West,India Bazaar</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>37</th>
      <td>The Danforth West,Riverdale</td>
      <td>0.1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>38 rows × 114 columns</p>
</div>



### Top 5 most common venues per Neighbourhood


```python
num_top_venues = 5

for hood in toronto_grouped['Neighborhood']:
    print("----"+hood+"----")
    temp = toronto_grouped[toronto_grouped['Neighborhood'] == hood].T.reset_index()
    temp.columns = ['venue','freq']
    temp = temp.iloc[1:]
    temp['freq'] = temp['freq'].astype(float)
    temp = temp.round({'freq': 2})
    print(temp.sort_values('freq', ascending=False).reset_index(drop=True).head(num_top_venues))
    print('\n')
```

    ----Adelaide,King,Richmond----
                  venue  freq
    0             Hotel   0.1
    1  Asian Restaurant   0.1
    2      Concert Hall   0.1
    3         Speakeasy   0.1
    4        Steakhouse   0.1
    
    
    ----Berczy Park----
                venue  freq
    0    Concert Hall   0.1
    1    Liquor Store   0.1
    2  Farmers Market   0.1
    3            Park   0.1
    4      Steakhouse   0.1
    
    
    ----Brockton,Exhibition Place,Parkdale Village----
                        venue  freq
    0             Coffee Shop   0.2
    1  Furniture / Home Store   0.1
    2                     Gym   0.1
    3    Caribbean Restaurant   0.1
    4                    Café   0.1
    
    
    ----Business Reply Mail Processing Centre 969 Eastern----
                      venue  freq
    0         Auto Workshop   0.1
    1         Garden Center   0.1
    2         Burrito Place   0.1
    3  Fast Food Restaurant   0.1
    4        Farmers Market   0.1
    
    
    ----CN Tower,Bathurst Quay,Island airport,Harbourfront West,King and Spadina,Railway Lands,South Niagara----
                    venue  freq
    0      Airport Lounge   0.2
    1     Harbor / Marina   0.1
    2  Airport Food Court   0.1
    3        Airport Gate   0.1
    4    Airport Terminal   0.1
    
    
    ----Cabbagetown,St. James Town----
                     venue  freq
    0                 Café   0.2
    1    Indian Restaurant   0.1
    2                Diner   0.1
    3        Jewelry Store   0.1
    4  Japanese Restaurant   0.1
    
    
    ----Central Bay Street----
                            venue  freq
    0                 Coffee Shop   0.3
    1            Sushi Restaurant   0.1
    2            Ramen Restaurant   0.1
    3  Modern European Restaurant   0.1
    4                        Park   0.1
    
    
    ----Chinatown,Grange Park,Kensington Market----
                     venue  freq
    0                 Café   0.3
    1          Coffee Shop   0.1
    2  Arts & Crafts Store   0.1
    3                  Bar   0.1
    4               Bakery   0.1
    
    
    ----Christie----
                    venue  freq
    0                Café   0.3
    1       Grocery Store   0.2
    2         Coffee Shop   0.1
    3         Candy Store   0.1
    4  Italian Restaurant   0.1
    
    
    ----Church and Wellesley----
                    venue  freq
    0      Breakfast Spot   0.1
    1  Mexican Restaurant   0.1
    2        Dance Studio   0.1
    3    Theme Restaurant   0.1
    4           Bookstore   0.1
    
    
    ----Commerce Court,Victoria Hotel----
                      venue  freq
    0                  Café   0.2
    1           Coffee Shop   0.1
    2  Gym / Fitness Center   0.1
    3             Gastropub   0.1
    4                Museum   0.1
    
    
    ----Davisville----
                  venue  freq
    0      Dessert Shop   0.2
    1       Coffee Shop   0.1
    2  Sushi Restaurant   0.1
    3       Pizza Place   0.1
    4              Café   0.1
    
    
    ----Davisville North----
                   venue  freq
    0                Gym  0.12
    1  Food & Drink Shop  0.12
    2     Clothing Store  0.12
    3       Dance Studio  0.12
    4     Sandwich Place  0.12
    
    
    ----Deer Park,Forest Hill SE,Rathnelly,South Hill,Summerhill West----
                  venue  freq
    0               Pub   0.2
    1       Coffee Shop   0.2
    2  Sushi Restaurant   0.1
    3        Restaurant   0.1
    4        Sports Bar   0.1
    
    
    ----Design Exchange,Toronto Dominion Centre----
                      venue  freq
    0           Coffee Shop   0.2
    1              Beer Bar   0.1
    2  Gym / Fitness Center   0.1
    3             Gastropub   0.1
    4                 Hotel   0.1
    
    
    ----Dovercourt Village,Dufferin----
                           venue  freq
    0                     Bakery   0.2
    1                   Pharmacy   0.1
    2                Music Venue   0.1
    3  Middle Eastern Restaurant   0.1
    4                       Café   0.1
    
    
    ----First Canadian Place,Underground city----
                      venue  freq
    0                  Café   0.2
    1           Coffee Shop   0.1
    2            Steakhouse   0.1
    3  Gym / Fitness Center   0.1
    4             Gastropub   0.1
    
    
    ----Forest Hill North,Forest Hill West----
                   venue  freq
    0               Park  0.25
    1              Trail  0.25
    2   Sushi Restaurant  0.25
    3      Jewelry Store  0.25
    4  Korean Restaurant  0.00
    
    
    ----Harbord,University of Toronto----
                    venue  freq
    0         College Gym   0.1
    1  Italian Restaurant   0.1
    2           Bookstore   0.1
    3            Beer Bar   0.1
    4                 Bar   0.1
    
    
    ----Harbourfront East,Toronto Islands,Union Station----
                     venue  freq
    0                 Park   0.1
    1                Plaza   0.1
    2          Salad Place   0.1
    3  Sporting Goods Shop   0.1
    4          Supermarket   0.1
    
    
    ----Harbourfront,Regent Park----
                venue  freq
    0  Breakfast Spot   0.2
    1     Coffee Shop   0.1
    2          Bakery   0.1
    3             Pub   0.1
    4      Restaurant   0.1
    
    
    ----High Park,The Junction South----
                     venue  freq
    0                 Park   0.1
    1  Arts & Crafts Store   0.1
    2            Speakeasy   0.1
    3                 Café   0.1
    4            Bookstore   0.1
    
    
    ----Lawrence Park----
                      venue  freq
    0                  Park  0.33
    1           Swim School  0.33
    2              Bus Line  0.33
    3     Korean Restaurant  0.00
    4  Other Great Outdoors  0.00
    
    
    ----Little Portugal,Trinity----
                   venue  freq
    0        Yoga Studio   0.1
    1                Bar   0.1
    2        Pizza Place   0.1
    3  Korean Restaurant   0.1
    4     Ice Cream Shop   0.1
    
    
    ----Moore Park,Summerhill East----
                      venue  freq
    0                   Gym   1.0
    1           Yoga Studio   0.0
    2                  Lake   0.0
    3                  Park   0.0
    4  Other Great Outdoors   0.0
    
    
    ----North Toronto West----
                     venue  freq
    0          Yoga Studio   0.1
    1  Sporting Goods Shop   0.1
    2   Mexican Restaurant   0.1
    3                Diner   0.1
    4         Dessert Shop   0.1
    
    
    ----Parkdale,Roncesvalles----
                    venue  freq
    0           Gift Shop   0.2
    1         Coffee Shop   0.1
    2    Cuban Restaurant   0.1
    3        Dessert Shop   0.1
    4  Italian Restaurant   0.1
    
    
    ----Rosedale----
                      venue  freq
    0                  Park  0.50
    1                 Trail  0.25
    2            Playground  0.25
    3     Korean Restaurant  0.00
    4  Other Great Outdoors  0.00
    
    
    ----Roselawn----
                      venue  freq
    0                Garden   1.0
    1           Yoga Studio   0.0
    2     Korean Restaurant   0.0
    3  Other Great Outdoors   0.0
    4       Organic Grocery   0.0
    
    
    ----Runnymede,Swansea----
                  venue  freq
    0  Sushi Restaurant   0.2
    1               Pub   0.1
    2     Burrito Place   0.1
    3              Food   0.1
    4              Café   0.1
    
    
    ----Ryerson,Garden District----
                  venue  freq
    0              Café   0.2
    1       Pizza Place   0.1
    2          Tea Room   0.1
    3     Burrito Place   0.1
    4  Ramen Restaurant   0.1
    
    
    ----St. James Town----
                    venue  freq
    0         Coffee Shop   0.2
    1           BBQ Joint   0.1
    2           Gastropub   0.1
    3  Italian Restaurant   0.1
    4          Food Truck   0.1
    
    
    ----Stn A PO Boxes 25 The Esplanade----
                               venue  freq
    0                           Park   0.1
    1                       Fountain   0.1
    2  Vegetarian / Vegan Restaurant   0.1
    3                   Concert Hall   0.1
    4                   Cocktail Bar   0.1
    
    
    ----Studio District----
                venue  freq
    0     Coffee Shop   0.1
    1  Ice Cream Shop   0.1
    2  Sandwich Place   0.1
    3       Bookstore   0.1
    4          Bakery   0.1
    
    
    ----The Annex,North Midtown,Yorkville----
                     venue  freq
    0                 Café   0.2
    1          Coffee Shop   0.1
    2  American Restaurant   0.1
    3    Indian Restaurant   0.1
    4            BBQ Joint   0.1
    
    
    ----The Beaches----
                      venue  freq
    0  Other Great Outdoors   0.2
    1                 Trail   0.2
    2     Health Food Store   0.2
    3                   Pub   0.2
    4           Yoga Studio   0.0
    
    
    ----The Beaches West,India Bazaar----
                    venue  freq
    0           Pet Store   0.1
    1      Ice Cream Shop   0.1
    2             Brewery   0.1
    3   Fish & Chips Shop   0.1
    4  Italian Restaurant   0.1
    
    
    ----The Danforth West,Riverdale----
                  venue  freq
    0  Greek Restaurant   0.3
    1    Ice Cream Shop   0.2
    2       Yoga Studio   0.1
    3    Cosmetics Shop   0.1
    4               Pub   0.1
    
    


### Convert to dataframe


```python
def return_most_common_venues(row, num_top_venues):
    row_categories = row.iloc[1:]
    row_categories_sorted = row_categories.sort_values(ascending=False)
    
    return row_categories_sorted.index.values[0:num_top_venues]

num_top_venues = 10

indicators = ['st', 'nd', 'rd']

# create columns according to number of top venues
columns = ['Neighborhood']
for ind in np.arange(num_top_venues):
    try:
        columns.append('{}{} Most Common Venue'.format(ind+1, indicators[ind]))
    except:
        columns.append('{}th Most Common Venue'.format(ind+1))

# create a new dataframe
neighborhoods_venues_sorted = pd.DataFrame(columns=columns)
neighborhoods_venues_sorted['Neighborhood'] = toronto_grouped['Neighborhood']

for ind in np.arange(toronto_grouped.shape[0]):
    neighborhoods_venues_sorted.iloc[ind, 1:] = return_most_common_venues(toronto_grouped.iloc[ind, :], num_top_venues)

neighborhoods_venues_sorted.head()
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
      <th>Neighborhood</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adelaide,King,Richmond</td>
      <td>Seafood Restaurant</td>
      <td>Asian Restaurant</td>
      <td>Concert Hall</td>
      <td>Plaza</td>
      <td>Hotel</td>
      <td>Speakeasy</td>
      <td>Steakhouse</td>
      <td>Opera House</td>
      <td>Greek Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Berczy Park</td>
      <td>Park</td>
      <td>Steakhouse</td>
      <td>Museum</td>
      <td>Concert Hall</td>
      <td>Liquor Store</td>
      <td>Farmers Market</td>
      <td>Cocktail Bar</td>
      <td>French Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Thai Restaurant</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Brockton,Exhibition Place,Parkdale Village</td>
      <td>Coffee Shop</td>
      <td>Gym</td>
      <td>Italian Restaurant</td>
      <td>Bar</td>
      <td>Café</td>
      <td>Pet Store</td>
      <td>Caribbean Restaurant</td>
      <td>Furniture / Home Store</td>
      <td>Breakfast Spot</td>
      <td>Cosmetics Shop</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Business Reply Mail Processing Centre 969 Eastern</td>
      <td>Garden Center</td>
      <td>Pizza Place</td>
      <td>Restaurant</td>
      <td>Skate Park</td>
      <td>Farmers Market</td>
      <td>Fast Food Restaurant</td>
      <td>Auto Workshop</td>
      <td>Burrito Place</td>
      <td>Comic Shop</td>
      <td>Brewery</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CN Tower,Bathurst Quay,Island airport,Harbourf...</td>
      <td>Airport Lounge</td>
      <td>Boutique</td>
      <td>Bar</td>
      <td>Airport</td>
      <td>Airport Food Court</td>
      <td>Airport Gate</td>
      <td>Airport Terminal</td>
      <td>Coffee Shop</td>
      <td>Harbor / Marina</td>
      <td>Farmers Market</td>
    </tr>
  </tbody>
</table>
</div>



### Cluster


```python
# import k-means from clustering stage
from sklearn.cluster import KMeans

# set number of clusters
kclusters = 5

toronto_grouped_clustering = toronto_grouped.drop('Neighborhood', 1)

# run k-means clustering
kmeans = KMeans(n_clusters=kclusters, random_state=0).fit(toronto_grouped_clustering)

# check cluster labels generated for each row in the dataframe
kmeans.labels_[0:10] 
```




    array([1, 1, 0, 1, 1, 1, 0, 1, 1, 1], dtype=int32)




```python
# add clustering labels
neighborhoods_venues_sorted.insert(0, 'Cluster Labels', kmeans.labels_)

toronto_merged = visualise_df

# merge toronto_grouped with toronto_data to add latitude/longitude for each neighborhood
toronto_merged = toronto_merged.join(neighborhoods_venues_sorted.set_index('Neighborhood'), on='Neighbourhood')

toronto_merged.head() # check the last columns!
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
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
      <td>0</td>
      <td>Trail</td>
      <td>Pub</td>
      <td>Health Food Store</td>
      <td>Other Great Outdoors</td>
      <td>Wine Bar</td>
      <td>Diner</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West,Riverdale</td>
      <td>43.679557</td>
      <td>-79.352188</td>
      <td>1</td>
      <td>Greek Restaurant</td>
      <td>Ice Cream Shop</td>
      <td>Yoga Studio</td>
      <td>Cosmetics Shop</td>
      <td>Pub</td>
      <td>Italian Restaurant</td>
      <td>Brewery</td>
      <td>Dog Run</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4L</td>
      <td>East Toronto</td>
      <td>The Beaches West,India Bazaar</td>
      <td>43.668999</td>
      <td>-79.315572</td>
      <td>1</td>
      <td>Gym</td>
      <td>Sushi Restaurant</td>
      <td>Ice Cream Shop</td>
      <td>Burger Joint</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Liquor Store</td>
      <td>Brewery</td>
      <td>Italian Restaurant</td>
      <td>Pet Store</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4M</td>
      <td>East Toronto</td>
      <td>Studio District</td>
      <td>43.659526</td>
      <td>-79.340923</td>
      <td>1</td>
      <td>Gay Bar</td>
      <td>Fish Market</td>
      <td>Cheese Shop</td>
      <td>Sandwich Place</td>
      <td>Seafood Restaurant</td>
      <td>Coffee Shop</td>
      <td>Ice Cream Shop</td>
      <td>Bakery</td>
      <td>Bookstore</td>
      <td>Flea Market</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M4N</td>
      <td>Central Toronto</td>
      <td>Lawrence Park</td>
      <td>43.728020</td>
      <td>-79.388790</td>
      <td>2</td>
      <td>Park</td>
      <td>Swim School</td>
      <td>Bus Line</td>
      <td>Dog Run</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
      <td>Concert Hall</td>
      <td>Cosmetics Shop</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Matplotlib and associated plotting modules
import matplotlib.cm as cm
import matplotlib.colors as colors

# create map
map_clusters = folium.Map(location=[neighborhood_latitude, neighborhood_longitude], zoom_start=11)

# set color scheme for the clusters
x = np.arange(kclusters)
ys = [i + x + (i*x)**2 for i in range(kclusters)]
colors_array = cm.rainbow(np.linspace(0, 1, len(ys)))
rainbow = [colors.rgb2hex(i) for i in colors_array]

# add markers to the map
markers_colors = []
for lat, lon, poi, cluster in zip(toronto_merged['Latitude'], toronto_merged['Longitude'], toronto_merged['Neighbourhood'], toronto_merged['Cluster Labels']):
    label = folium.Popup(str(poi) + ' Cluster ' + str(cluster), parse_html=True)
    folium.CircleMarker(
        [lat, lon],
        radius=5,
        popup=label,
        color=rainbow[cluster-1],
        fill=True,
        fill_color=rainbow[cluster-1],
        fill_opacity=0.7).add_to(map_clusters)
       
map_clusters
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><iframe src="data:text/html;charset=utf-8;base64,PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgCiAgICAgICAgPHNjcmlwdD4KICAgICAgICAgICAgTF9OT19UT1VDSCA9IGZhbHNlOwogICAgICAgICAgICBMX0RJU0FCTEVfM0QgPSBmYWxzZTsKICAgICAgICA8L3NjcmlwdD4KICAgIAogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuanMiPjwvc2NyaXB0PgogICAgPHNjcmlwdCBzcmM9Imh0dHBzOi8vY29kZS5qcXVlcnkuY29tL2pxdWVyeS0xLjEyLjQubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9qcy9ib290c3RyYXAubWluLmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5qcyI+PC9zY3JpcHQ+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuLmpzZGVsaXZyLm5ldC9ucG0vbGVhZmxldEAxLjUuMS9kaXN0L2xlYWZsZXQuY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vYm9vdHN0cmFwLzMuMi4wL2Nzcy9ib290c3RyYXAubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLXRoZW1lLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9mb250LWF3ZXNvbWUvNC42LjMvY3NzL2ZvbnQtYXdlc29tZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vY2RuanMuY2xvdWRmbGFyZS5jb20vYWpheC9saWJzL0xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLzIuMC4yL2xlYWZsZXQuYXdlc29tZS1tYXJrZXJzLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL3Jhd2Nkbi5naXRoYWNrLmNvbS9weXRob24tdmlzdWFsaXphdGlvbi9mb2xpdW0vbWFzdGVyL2ZvbGl1bS90ZW1wbGF0ZXMvbGVhZmxldC5hd2Vzb21lLnJvdGF0ZS5jc3MiLz4KICAgIDxzdHlsZT5odG1sLCBib2R5IHt3aWR0aDogMTAwJTtoZWlnaHQ6IDEwMCU7bWFyZ2luOiAwO3BhZGRpbmc6IDA7fTwvc3R5bGU+CiAgICA8c3R5bGU+I21hcCB7cG9zaXRpb246YWJzb2x1dGU7dG9wOjA7Ym90dG9tOjA7cmlnaHQ6MDtsZWZ0OjA7fTwvc3R5bGU+CiAgICAKICAgICAgICAgICAgPG1ldGEgbmFtZT0idmlld3BvcnQiIGNvbnRlbnQ9IndpZHRoPWRldmljZS13aWR0aCwKICAgICAgICAgICAgICAgIGluaXRpYWwtc2NhbGU9MS4wLCBtYXhpbXVtLXNjYWxlPTEuMCwgdXNlci1zY2FsYWJsZT1ubyIgLz4KICAgICAgICAgICAgPHN0eWxlPgogICAgICAgICAgICAgICAgI21hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSB7CiAgICAgICAgICAgICAgICAgICAgcG9zaXRpb246IHJlbGF0aXZlOwogICAgICAgICAgICAgICAgICAgIHdpZHRoOiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICAgICAgbGVmdDogMC4wJTsKICAgICAgICAgICAgICAgICAgICB0b3A6IDAuMCU7CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIDwvc3R5bGU+CiAgICAgICAgCjwvaGVhZD4KPGJvZHk+ICAgIAogICAgCiAgICAgICAgICAgIDxkaXYgY2xhc3M9ImZvbGl1bS1tYXAiIGlkPSJtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEiID48L2Rpdj4KICAgICAgICAKPC9ib2R5Pgo8c2NyaXB0PiAgICAKICAgIAogICAgICAgICAgICB2YXIgbWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhID0gTC5tYXAoCiAgICAgICAgICAgICAgICAibWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhIiwKICAgICAgICAgICAgICAgIHsKICAgICAgICAgICAgICAgICAgICBjZW50ZXI6IFs0My42NzYzNTczOTk5OTk5OSwgLTc5LjI5MzAzMTJdLAogICAgICAgICAgICAgICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcsCiAgICAgICAgICAgICAgICAgICAgem9vbTogMTEsCiAgICAgICAgICAgICAgICAgICAgem9vbUNvbnRyb2w6IHRydWUsCiAgICAgICAgICAgICAgICAgICAgcHJlZmVyQ2FudmFzOiBmYWxzZSwKICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgKTsKCiAgICAgICAgICAgIAoKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgdGlsZV9sYXllcl80NTg0YWU1ZjA3YzM0MDYzOTFmMDI0ZTQ4ZDJlZGIzMyA9IEwudGlsZUxheWVyKAogICAgICAgICAgICAgICAgImh0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nIiwKICAgICAgICAgICAgICAgIHsiYXR0cmlidXRpb24iOiAiRGF0YSBieSBcdTAwMjZjb3B5OyBcdTAwM2NhIGhyZWY9XCJodHRwOi8vb3BlbnN0cmVldG1hcC5vcmdcIlx1MDAzZU9wZW5TdHJlZXRNYXBcdTAwM2MvYVx1MDAzZSwgdW5kZXIgXHUwMDNjYSBocmVmPVwiaHR0cDovL3d3dy5vcGVuc3RyZWV0bWFwLm9yZy9jb3B5cmlnaHRcIlx1MDAzZU9EYkxcdTAwM2MvYVx1MDAzZS4iLCAiZGV0ZWN0UmV0aW5hIjogZmFsc2UsICJtYXhOYXRpdmVab29tIjogMTgsICJtYXhab29tIjogMTgsICJtaW5ab29tIjogMCwgIm5vV3JhcCI6IGZhbHNlLCAib3BhY2l0eSI6IDEsICJzdWJkb21haW5zIjogImFiYyIsICJ0bXMiOiBmYWxzZX0KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzVjZTBmYWI4ZmZiMTQxYjFhY2M0MTUyMGRjZjYxMmFjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjc2MzU3Mzk5OTk5OTksIC03OS4yOTMwMzEyXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjZmYwMDAwIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiNmZjAwMDAiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzM4MjZmYmIxMTc1ZjQ0ZGY4ZTZhNDU4ODZmNTQ0MjMxID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9jY2EyMzcyMmE3ODk0ZTBkOTljYmM2ZmM4MTY4ZTczYSA9ICQoYDxkaXYgaWQ9Imh0bWxfY2NhMjM3MjJhNzg5NGUwZDk5Y2JjNmZjODE2OGU3M2EiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRoZSBCZWFjaGVzIENsdXN0ZXIgMDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8zODI2ZmJiMTE3NWY0NGRmOGU2YTQ1ODg2ZjU0NDIzMS5zZXRDb250ZW50KGh0bWxfY2NhMjM3MjJhNzg5NGUwZDk5Y2JjNmZjODE2OGU3M2EpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzVjZTBmYWI4ZmZiMTQxYjFhY2M0MTUyMGRjZjYxMmFjLmJpbmRQb3B1cChwb3B1cF8zODI2ZmJiMTE3NWY0NGRmOGU2YTQ1ODg2ZjU0NDIzMSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYWQwZDgxOTllNTM4NDE2MThkOGVlOGRmZjZiYTEwY2QgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Nzk1NTcxLCAtNzkuMzUyMTg4XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzU1NWE4ZmUzNDYzMzRhZjZhOWJlYWIxOTQ5ODE3MGJkID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8wOTFlOGE2OWRiMjA0ZDIzODdmNzVmNDRlOTEwNmE5ZSA9ICQoYDxkaXYgaWQ9Imh0bWxfMDkxZThhNjlkYjIwNGQyMzg3Zjc1ZjQ0ZTkxMDZhOWUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRoZSBEYW5mb3J0aCBXZXN0LFJpdmVyZGFsZSBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNTU1YThmZTM0NjMzNGFmNmE5YmVhYjE5NDk4MTcwYmQuc2V0Q29udGVudChodG1sXzA5MWU4YTY5ZGIyMDRkMjM4N2Y3NWY0NGU5MTA2YTllKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9hZDBkODE5OWU1Mzg0MTYxOGQ4ZWU4ZGZmNmJhMTBjZC5iaW5kUG9wdXAocG9wdXBfNTU1YThmZTM0NjMzNGFmNmE5YmVhYjE5NDk4MTcwYmQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2ZkOGNhNTViN2MwYTRjNWViMmU0ZTVjZTE0ZDY3YWY2ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjY4OTk4NSwgLTc5LjMxNTU3MTU5OTk5OTk4XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzVmNTA4ODQ5NjRkYTQxNmJhNDY3NjZlM2NjMmIyYzQzID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9kYjEwZGQ3ZjA4YmU0ZDgyODM1Mzg5MGVkMmY0Nzc4ZCA9ICQoYDxkaXYgaWQ9Imh0bWxfZGIxMGRkN2YwOGJlNGQ4MjgzNTM4OTBlZDJmNDc3OGQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRoZSBCZWFjaGVzIFdlc3QsSW5kaWEgQmF6YWFyIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81ZjUwODg0OTY0ZGE0MTZiYTQ2NzY2ZTNjYzJiMmM0My5zZXRDb250ZW50KGh0bWxfZGIxMGRkN2YwOGJlNGQ4MjgzNTM4OTBlZDJmNDc3OGQpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2ZkOGNhNTViN2MwYTRjNWViMmU0ZTVjZTE0ZDY3YWY2LmJpbmRQb3B1cChwb3B1cF81ZjUwODg0OTY0ZGE0MTZiYTQ2NzY2ZTNjYzJiMmM0MykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODBkYzQxNDk4NWMwNDA1YTlhYzVmOWYyZjcwNjI4MGEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTk1MjU1LCAtNzkuMzQwOTIzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzc0NWYyOTI1YmFmOTRkODY5ZGJmNGY1ZWQ1YTI2NjQ4ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9mMzM5YzhjYjM2ZWQ0NDQyOTUxMzZiZmQ2OTQ5YTM1MCA9ICQoYDxkaXYgaWQ9Imh0bWxfZjMzOWM4Y2IzNmVkNDQ0Mjk1MTM2YmZkNjk0OWEzNTAiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlN0dWRpbyBEaXN0cmljdCBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNzQ1ZjI5MjViYWY5NGQ4NjlkYmY0ZjVlZDVhMjY2NDguc2V0Q29udGVudChodG1sX2YzMzljOGNiMzZlZDQ0NDI5NTEzNmJmZDY5NDlhMzUwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl84MGRjNDE0OTg1YzA0MDVhOWFjNWY5ZjJmNzA2MjgwYS5iaW5kUG9wdXAocG9wdXBfNzQ1ZjI5MjViYWY5NGQ4NjlkYmY0ZjVlZDVhMjY2NDgpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzhjNjRhOTA5MzRlYjRhYTU4MzlmZTg0ZmI0MjhlNGJkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzI4MDIwNSwgLTc5LjM4ODc5MDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiMwMGI1ZWIiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzAwYjVlYiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfODVjMGIyMGNkYThmNGZkZThjY2MwYzE2OTViNmY4YmUgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2IzMGQ3MDk3NDIyYTQxNDI4NmZkMDNkMjcxOWU1NTMwID0gJChgPGRpdiBpZD0iaHRtbF9iMzBkNzA5NzQyMmE0MTQyODZmZDAzZDI3MTllNTUzMCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TGF3cmVuY2UgUGFyayBDbHVzdGVyIDI8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfODVjMGIyMGNkYThmNGZkZThjY2MwYzE2OTViNmY4YmUuc2V0Q29udGVudChodG1sX2IzMGQ3MDk3NDIyYTQxNDI4NmZkMDNkMjcxOWU1NTMwKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl84YzY0YTkwOTM0ZWI0YWE1ODM5ZmU4NGZiNDI4ZTRiZC5iaW5kUG9wdXAocG9wdXBfODVjMGIyMGNkYThmNGZkZThjY2MwYzE2OTViNmY4YmUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2FiOTZiNDY3OGNjZDQ1ZjE5Y2YxMWNlYzY3ZTA4MmJjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzEyNzUxMSwgLTc5LjM5MDE5NzVdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiM4MDAwZmYiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNzcxODgzZjIzM2Q3NDQ4NGIxY2FhYjE0OGNmNzlhYzQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzY4ODBlN2I3ZWIwZDQwNmViYjg5MThlNDEyZjgxOWZhID0gJChgPGRpdiBpZD0iaHRtbF82ODgwZTdiN2ViMGQ0MDZlYmI4OTE4ZTQxMmY4MTlmYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGF2aXN2aWxsZSBOb3J0aCBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNzcxODgzZjIzM2Q3NDQ4NGIxY2FhYjE0OGNmNzlhYzQuc2V0Q29udGVudChodG1sXzY4ODBlN2I3ZWIwZDQwNmViYjg5MThlNDEyZjgxOWZhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9hYjk2YjQ2NzhjY2Q0NWYxOWNmMTFjZWM2N2UwODJiYy5iaW5kUG9wdXAocG9wdXBfNzcxODgzZjIzM2Q3NDQ4NGIxY2FhYjE0OGNmNzlhYzQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2U0NWJkZWI4Njg2YzQyY2M4ZWI1MDNhNjRhZTUwNDA0ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzE1MzgzNCwgLTc5LjQwNTY3ODQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzQyM2JlNDk0NzY2MzQwY2VhOTBmOGI1MjkwMDU5MGFlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8xOGEzODRhNDkwYWQ0NDZjYTJmZWM0ZjQwYTE2MjNlNCA9ICQoYDxkaXYgaWQ9Imh0bWxfMThhMzg0YTQ5MGFkNDQ2Y2EyZmVjNGY0MGExNjIzZTQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk5vcnRoIFRvcm9udG8gV2VzdCBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNDIzYmU0OTQ3NjYzNDBjZWE5MGY4YjUyOTAwNTkwYWUuc2V0Q29udGVudChodG1sXzE4YTM4NGE0OTBhZDQ0NmNhMmZlYzRmNDBhMTYyM2U0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9lNDViZGViODY4NmM0MmNjOGViNTAzYTY0YWU1MDQwNC5iaW5kUG9wdXAocG9wdXBfNDIzYmU0OTQ3NjYzNDBjZWE5MGY4YjUyOTAwNTkwYWUpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2JiYjkzMDQ3YTJmYzQ2MDM5NjA0MzEzZDFmYTk1OTk2ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNzA0MzI0NCwgLTc5LjM4ODc5MDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiM4MDAwZmYiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMDQ5YWM1NTgwZjdlNDk1YTg4NGE3NGUwMzlmYmI2ZWQgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzA0Mzg4MzkxOTU3NTRhMzZiMjYzMTAwZTEzZjMyZWU5ID0gJChgPGRpdiBpZD0iaHRtbF8wNDM4ODM5MTk1NzU0YTM2YjI2MzEwMGUxM2YzMmVlOSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGF2aXN2aWxsZSBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMDQ5YWM1NTgwZjdlNDk1YTg4NGE3NGUwMzlmYmI2ZWQuc2V0Q29udGVudChodG1sXzA0Mzg4MzkxOTU3NTRhMzZiMjYzMTAwZTEzZjMyZWU5KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9iYmI5MzA0N2EyZmM0NjAzOTYwNDMxM2QxZmE5NTk5Ni5iaW5kUG9wdXAocG9wdXBfMDQ5YWM1NTgwZjdlNDk1YTg4NGE3NGUwMzlmYmI2ZWQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzliOWMyNGEwNGMyNzRmOTY5ODdjYTc3OTQ1MjNiODRkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjg5NTc0MywgLTc5LjM4MzE1OTkwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjZmZiMzYwIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiNmZmIzNjAiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzUzODczNmY1M2FhNDRlYmE5ZmQxY2I5Zjc2Zjg3ZTFlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9jZDA5OTExNWViMDg0NjRhYTg1ZmM2OTc5NWE5ZTgyYSA9ICQoYDxkaXYgaWQ9Imh0bWxfY2QwOTkxMTVlYjA4NDY0YWE4NWZjNjk3OTVhOWU4MmEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk1vb3JlIFBhcmssU3VtbWVyaGlsbCBFYXN0IENsdXN0ZXIgNDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81Mzg3MzZmNTNhYTQ0ZWJhOWZkMWNiOWY3NmY4N2UxZS5zZXRDb250ZW50KGh0bWxfY2QwOTkxMTVlYjA4NDY0YWE4NWZjNjk3OTVhOWU4MmEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzliOWMyNGEwNGMyNzRmOTY5ODdjYTc3OTQ1MjNiODRkLmJpbmRQb3B1cChwb3B1cF81Mzg3MzZmNTNhYTQ0ZWJhOWZkMWNiOWY3NmY4N2UxZSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOWM4MzAyZWNkOTU2NDhjZGJkYTA2YzFjNTQ1MjMwMjEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42ODY0MTIyOTk5OTk5OSwgLTc5LjQwMDA0OTNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiNmZjAwMDAiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfYjJiZmJjMDI1ZTFlNDJiNzgxM2M1OGZkMzdjMDU4ODEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2U1ZWQ4MjkzNTFkMzRkOWQ4Y2FhODcwNWQxZDliNmU3ID0gJChgPGRpdiBpZD0iaHRtbF9lNWVkODI5MzUxZDM0ZDlkOGNhYTg3MDVkMWQ5YjZlNyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGVlciBQYXJrLEZvcmVzdCBIaWxsIFNFLFJhdGhuZWxseSxTb3V0aCBIaWxsLFN1bW1lcmhpbGwgV2VzdCBDbHVzdGVyIDA8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfYjJiZmJjMDI1ZTFlNDJiNzgxM2M1OGZkMzdjMDU4ODEuc2V0Q29udGVudChodG1sX2U1ZWQ4MjkzNTFkMzRkOWQ4Y2FhODcwNWQxZDliNmU3KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl85YzgzMDJlY2Q5NTY0OGNkYmRhMDZjMWM1NDUyMzAyMS5iaW5kUG9wdXAocG9wdXBfYjJiZmJjMDI1ZTFlNDJiNzgxM2M1OGZkMzdjMDU4ODEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzA3ODEwMjUwOGQ3ZDRiMTg4NWRiOWJmYTRhY2RhMGU5ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjc5NTYyNiwgLTc5LjM3NzUyOTQwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjMDBiNWViIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMwMGI1ZWIiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzU0YzBhNzFjMDgwMDQ2NGU5NWRjMGMzMDNiOTc1ODVlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9lMjAyOTBkYTg1NmM0ZTczYjI5ODJhMjU0MTVkZjQ5MyA9ICQoYDxkaXYgaWQ9Imh0bWxfZTIwMjkwZGE4NTZjNGU3M2IyOTgyYTI1NDE1ZGY0OTMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJvc2VkYWxlIENsdXN0ZXIgMjwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81NGMwYTcxYzA4MDA0NjRlOTVkYzBjMzAzYjk3NTg1ZS5zZXRDb250ZW50KGh0bWxfZTIwMjkwZGE4NTZjNGU3M2IyOTgyYTI1NDE1ZGY0OTMpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzA3ODEwMjUwOGQ3ZDRiMTg4NWRiOWJmYTRhY2RhMGU5LmJpbmRQb3B1cChwb3B1cF81NGMwYTcxYzA4MDA0NjRlOTVkYzBjMzAzYjk3NTg1ZSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDkzODMwMjBhMzA4NDIyYjgwNDBmNWQ2YjljODVhNzkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Njc5NjcsIC03OS4zNjc2NzUzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzUxZTdjYmQ3ZTUwMDQ3YTE5NDM0ZjgyZjUzYTYwZWRhID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83ZTM0NmE1OTI4ZGY0MmIwYWQxYTYxMmUwNzBkZWNlNCA9ICQoYDxkaXYgaWQ9Imh0bWxfN2UzNDZhNTkyOGRmNDJiMGFkMWE2MTJlMDcwZGVjZTQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNhYmJhZ2V0b3duLFN0LiBKYW1lcyBUb3duIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81MWU3Y2JkN2U1MDA0N2ExOTQzNGY4MmY1M2E2MGVkYS5zZXRDb250ZW50KGh0bWxfN2UzNDZhNTkyOGRmNDJiMGFkMWE2MTJlMDcwZGVjZTQpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzA5MzgzMDIwYTMwODQyMmI4MDQwZjVkNmI5Yzg1YTc5LmJpbmRQb3B1cChwb3B1cF81MWU3Y2JkN2U1MDA0N2ExOTQzNGY4MmY1M2E2MGVkYSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNzMzZWI0YjJjNjI2NDhmZThkZTg4OTc1MWFiZGJkMWUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjU4NTk5LCAtNzkuMzgzMTU5OTAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiM4MDAwZmYiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMWU5OWM5ZWUwYzNiNDhiNjhjNDA1NTRhMWI3NWNkNTggPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2U4YTNjNzFmYWEzMjRiOGNhOWUyNjJkNTEzOTI3ZmJkID0gJChgPGRpdiBpZD0iaHRtbF9lOGEzYzcxZmFhMzI0YjhjYTllMjYyZDUxMzkyN2ZiZCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2h1cmNoIGFuZCBXZWxsZXNsZXkgQ2x1c3RlciAxPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzFlOTljOWVlMGMzYjQ4YjY4YzQwNTU0YTFiNzVjZDU4LnNldENvbnRlbnQoaHRtbF9lOGEzYzcxZmFhMzI0YjhjYTllMjYyZDUxMzkyN2ZiZCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNzMzZWI0YjJjNjI2NDhmZThkZTg4OTc1MWFiZGJkMWUuYmluZFBvcHVwKHBvcHVwXzFlOTljOWVlMGMzYjQ4YjY4YzQwNTU0YTFiNzVjZDU4KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8xNTcxMmU4N2MwMTI0YjAwOGYwNzgzZjNmMTVhZjdjYiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1NDI1OTksIC03OS4zNjA2MzU5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjZmYwMDAwIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiNmZjAwMDAiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzEzY2Q1M2Y2YmI4NjQ2ZTI5MjU2ZjJjMTQ1Y2JmNjI0ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8wYzI3NjliYzRjOTc0NTY3YjQwNDg5ZjJiNzhlMGY4ZiA9ICQoYDxkaXYgaWQ9Imh0bWxfMGMyNzY5YmM0Yzk3NDU2N2I0MDQ4OWYyYjc4ZTBmOGYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhhcmJvdXJmcm9udCxSZWdlbnQgUGFyayBDbHVzdGVyIDA8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMTNjZDUzZjZiYjg2NDZlMjkyNTZmMmMxNDVjYmY2MjQuc2V0Q29udGVudChodG1sXzBjMjc2OWJjNGM5NzQ1NjdiNDA0ODlmMmI3OGUwZjhmKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8xNTcxMmU4N2MwMTI0YjAwOGYwNzgzZjNmMTVhZjdjYi5iaW5kUG9wdXAocG9wdXBfMTNjZDUzZjZiYjg2NDZlMjkyNTZmMmMxNDVjYmY2MjQpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzUwMTgxMzgxZDZkZDQwZWQ5Mjc3ODBmYTgyOTRjNjcxID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjU3MTYxOCwgLTc5LjM3ODkzNzA5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzQ0ODhlOWVjYTE2NTQyZWFiMWU5M2M2ZmE3NjA1YTk3ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF8wOTNmNGM2YTk4MzI0MDFlYmMyMzIyYjVjNWEzZDJjNyA9ICQoYDxkaXYgaWQ9Imh0bWxfMDkzZjRjNmE5ODMyNDAxZWJjMjMyMmI1YzVhM2QyYzciIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJ5ZXJzb24sR2FyZGVuIERpc3RyaWN0IENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF80NDg4ZTllY2ExNjU0MmVhYjFlOTNjNmZhNzYwNWE5Ny5zZXRDb250ZW50KGh0bWxfMDkzZjRjNmE5ODMyNDAxZWJjMjMyMmI1YzVhM2QyYzcpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzUwMTgxMzgxZDZkZDQwZWQ5Mjc3ODBmYTgyOTRjNjcxLmJpbmRQb3B1cChwb3B1cF80NDg4ZTllY2ExNjU0MmVhYjFlOTNjNmZhNzYwNWE5NykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMmJmZGQxNWI0YTY0NDExYzliNDA1OTA0MWFiNTkyZWYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTE0OTM5LCAtNzkuMzc1NDE3OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiI2ZmMDAwMCIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8wNDlhYjk3ZmU1YTk0MjdiYmIyMWFkMThmYzk5YWE1YSA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMDJlM2I0OTdhZGYxNDFiMTlkOTljM2E0NGIyZmI3ZjIgPSAkKGA8ZGl2IGlkPSJodG1sXzAyZTNiNDk3YWRmMTQxYjE5ZDk5YzNhNDRiMmZiN2YyIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TdC4gSmFtZXMgVG93biBDbHVzdGVyIDA8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfMDQ5YWI5N2ZlNWE5NDI3YmJiMjFhZDE4ZmM5OWFhNWEuc2V0Q29udGVudChodG1sXzAyZTNiNDk3YWRmMTQxYjE5ZDk5YzNhNDRiMmZiN2YyKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8yYmZkZDE1YjRhNjQ0MTFjOWI0MDU5MDQxYWI1OTJlZi5iaW5kUG9wdXAocG9wdXBfMDQ5YWI5N2ZlNWE5NDI3YmJiMjFhZDE4ZmM5OWFhNWEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2I3ZjY5MjUyMjAyZjQ0ZTk4YTc1MDgxZWRhOTExYTJhID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQ0NzcwNzk5OTk5OTk2LCAtNzkuMzczMzA2NF0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiIzgwMDBmZiIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjODAwMGZmIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF83YmVmODU5M2EwNDk0Yzk0YTkzZWY1MjA3NmM3ZDk2ZiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNmVlYmNkMGIyOWFjNDgyNWE1ZGNiZDZhY2NiZjNjODMgPSAkKGA8ZGl2IGlkPSJodG1sXzZlZWJjZDBiMjlhYzQ4MjVhNWRjYmQ2YWNjYmYzYzgzIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CZXJjenkgUGFyayBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfN2JlZjg1OTNhMDQ5NGM5NGE5M2VmNTIwNzZjN2Q5NmYuc2V0Q29udGVudChodG1sXzZlZWJjZDBiMjlhYzQ4MjVhNWRjYmQ2YWNjYmYzYzgzKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl9iN2Y2OTI1MjIwMmY0NGU5OGE3NTA4MWVkYTkxMWEyYS5iaW5kUG9wdXAocG9wdXBfN2JlZjg1OTNhMDQ5NGM5NGE5M2VmNTIwNzZjN2Q5NmYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzI3NDk1Mjk3MDU1OTQ1YmY4MTRhM2EyNzhlZDg1NDdjID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjU3OTUyNCwgLTc5LjM4NzM4MjZdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiNmZjAwMDAiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMjFlNjFkZTE2NTk0NGExYWI4YTZhOGFjMjhkNTg1YTIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2UxMDQwNDE2YTQxYjRjZDVhOGVjNmNlNTE1NzYwOGJiID0gJChgPGRpdiBpZD0iaHRtbF9lMTA0MDQxNmE0MWI0Y2Q1YThlYzZjZTUxNTc2MDhiYiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2VudHJhbCBCYXkgU3RyZWV0IENsdXN0ZXIgMDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8yMWU2MWRlMTY1OTQ0YTFhYjhhNmE4YWMyOGQ1ODVhMi5zZXRDb250ZW50KGh0bWxfZTEwNDA0MTZhNDFiNGNkNWE4ZWM2Y2U1MTU3NjA4YmIpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzI3NDk1Mjk3MDU1OTQ1YmY4MTRhM2EyNzhlZDg1NDdjLmJpbmRQb3B1cChwb3B1cF8yMWU2MWRlMTY1OTQ0YTFhYjhhNmE4YWMyOGQ1ODVhMikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMjRmNjI3NzBhMTVjNGNjMGJiNDc5NTYzNTZmNjMzNGYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTA1NzEyMDAwMDAwMSwgLTc5LjM4NDU2NzVdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiM4MDAwZmYiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNWZhOWI3NDE4MWFkNDVjNmI5YjUzZmE0OWNlNGMwYWYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2NiYzA2ZDc2NDNjZDRiYTM5MDU3YjA4NzM1MDI4MmJhID0gJChgPGRpdiBpZD0iaHRtbF9jYmMwNmQ3NjQzY2Q0YmEzOTA1N2IwODczNTAyODJiYSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QWRlbGFpZGUsS2luZyxSaWNobW9uZCBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNWZhOWI3NDE4MWFkNDVjNmI5YjUzZmE0OWNlNGMwYWYuc2V0Q29udGVudChodG1sX2NiYzA2ZDc2NDNjZDRiYTM5MDU3YjA4NzM1MDI4MmJhKTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl8yNGY2Mjc3MGExNWM0Y2MwYmI0Nzk1NjM1NmY2MzM0Zi5iaW5kUG9wdXAocG9wdXBfNWZhOWI3NDE4MWFkNDVjNmI5YjUzZmE0OWNlNGMwYWYpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2I0N2ZjODUxZTk2MDRiOGRhM2FmNTE1MTI1MzhlZDg2ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQwODE1NywgLTc5LjM4MTc1MjI5OTk5OTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzA5NzIzNWEwMGZlMzRmM2M5MWNlNTk1Yzg4Y2U0ZGFkID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9kMDZjNTUzMjdlZDY0NmQ2YjRmMjMyYjQ4ZDA5NWIzYyA9ICQoYDxkaXYgaWQ9Imh0bWxfZDA2YzU1MzI3ZWQ2NDZkNmI0ZjIzMmI0OGQwOTViM2MiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhhcmJvdXJmcm9udCBFYXN0LFRvcm9udG8gSXNsYW5kcyxVbmlvbiBTdGF0aW9uIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8wOTcyMzVhMDBmZTM0ZjNjOTFjZTU5NWM4OGNlNGRhZC5zZXRDb250ZW50KGh0bWxfZDA2YzU1MzI3ZWQ2NDZkNmI0ZjIzMmI0OGQwOTViM2MpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2I0N2ZjODUxZTk2MDRiOGRhM2FmNTE1MTI1MzhlZDg2LmJpbmRQb3B1cChwb3B1cF8wOTcyMzVhMDBmZTM0ZjNjOTFjZTU5NWM4OGNlNGRhZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZDE0ZTIxNTQyODk1NDM3MDg4MGI5OWI5NDBjMmE5OWYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDcxNzY4LCAtNzkuMzgxNTc2NDAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiNmZjAwMDAiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZWJjNDYwMjA1ZThkNDkzN2FjZWE1YjRhMGQ2ZTc0NjAgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2NjM2UyNWNlODJhNTQ4ZmRhNTkyZjc1ZTMwYmM4MDllID0gJChgPGRpdiBpZD0iaHRtbF9jYzNlMjVjZTgyYTU0OGZkYTU5MmY3NWUzMGJjODA5ZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RGVzaWduIEV4Y2hhbmdlLFRvcm9udG8gRG9taW5pb24gQ2VudHJlIENsdXN0ZXIgMDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9lYmM0NjAyMDVlOGQ0OTM3YWNlYTViNGEwZDZlNzQ2MC5zZXRDb250ZW50KGh0bWxfY2MzZTI1Y2U4MmE1NDhmZGE1OTJmNzVlMzBiYzgwOWUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2QxNGUyMTU0Mjg5NTQzNzA4ODBiOTliOTQwYzJhOTlmLmJpbmRQb3B1cChwb3B1cF9lYmM0NjAyMDVlOGQ0OTM3YWNlYTViNGEwZDZlNzQ2MCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMTM1NmJmNzEzOThkNDM0OGJjMGNhNjMxNmUyN2U4NWYgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDgxOTg1LCAtNzkuMzc5ODE2OTAwMDAwMDFdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiNmZjAwMDAiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfMjVmNWM1OGRmNTMxNGZhNzg1NzEyNTc1MTQzODY2YWYgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzQ4MGQyNjg1MzhiNjQ1ZDI4MWM2MDEyZDZiMjIyMDA3ID0gJChgPGRpdiBpZD0iaHRtbF80ODBkMjY4NTM4YjY0NWQyODFjNjAxMmQ2YjIyMjAwNyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q29tbWVyY2UgQ291cnQsVmljdG9yaWEgSG90ZWwgQ2x1c3RlciAwPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzI1ZjVjNThkZjUzMTRmYTc4NTcxMjU3NTE0Mzg2NmFmLnNldENvbnRlbnQoaHRtbF80ODBkMjY4NTM4YjY0NWQyODFjNjAxMmQ2YjIyMjAwNyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfMTM1NmJmNzEzOThkNDM0OGJjMGNhNjMxNmUyN2U4NWYuYmluZFBvcHVwKHBvcHVwXzI1ZjVjNThkZjUzMTRmYTc4NTcxMjU3NTE0Mzg2NmFmKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl82ZWQyOGMwYjU3YWE0MzUzYjQ1ODc0ZDNkYTliZTg3ZSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjcxMTY5NDgsIC03OS40MTY5MzU1OTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiIzgwZmZiNCIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjODBmZmI0IiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF81NTAwODFlODM3ODI0ZWFkYTA4OTk1YTkzOWUxNjM3MyA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfNWEwNzQ4N2M2NTYxNDZmZjhkMTgxZTA3M2NmNWExMTkgPSAkKGA8ZGl2IGlkPSJodG1sXzVhMDc0ODdjNjU2MTQ2ZmY4ZDE4MWUwNzNjZjVhMTE5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Sb3NlbGF3biBDbHVzdGVyIDM8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNTUwMDgxZTgzNzgyNGVhZGEwODk5NWE5MzllMTYzNzMuc2V0Q29udGVudChodG1sXzVhMDc0ODdjNjU2MTQ2ZmY4ZDE4MWUwNzNjZjVhMTE5KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl82ZWQyOGMwYjU3YWE0MzUzYjQ1ODc0ZDNkYTliZTg3ZS5iaW5kUG9wdXAocG9wdXBfNTUwMDgxZTgzNzgyNGVhZGEwODk5NWE5MzllMTYzNzMpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzY1OTQ2MWU2MDAwZDQ5YjliNGVjYzI0MDdkZGYzYzRiID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjk2OTQ3NiwgLTc5LjQxMTMwNzIwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjMDBiNWViIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiMwMGI1ZWIiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzc2YjRmNzc3Zjg4YzQ5ZGFiMzc4Y2NiNGUxMGE4ZjkzID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF80MGNlN2E1MzNkZjE0ZjNhOTJkYWM0Yjc1NGViMzBiMSA9ICQoYDxkaXYgaWQ9Imh0bWxfNDBjZTdhNTMzZGYxNGYzYTkyZGFjNGI3NTRlYjMwYjEiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkZvcmVzdCBIaWxsIE5vcnRoLEZvcmVzdCBIaWxsIFdlc3QgQ2x1c3RlciAyPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzc2YjRmNzc3Zjg4YzQ5ZGFiMzc4Y2NiNGUxMGE4ZjkzLnNldENvbnRlbnQoaHRtbF80MGNlN2E1MzNkZjE0ZjNhOTJkYWM0Yjc1NGViMzBiMSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNjU5NDYxZTYwMDBkNDliOWI0ZWNjMjQwN2RkZjNjNGIuYmluZFBvcHVwKHBvcHVwXzc2YjRmNzc3Zjg4YzQ5ZGFiMzc4Y2NiNGUxMGE4ZjkzKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mODI3YmUzOWM4Zjk0NTdhOTAxMTExZTlhM2VlMjQ5MiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY3MjcwOTcsIC03OS40MDU2Nzg0MDAwMDAwMV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiI2ZmMDAwMCIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF85NDQ5YjcyNGMzMzE0ZGNjODIyMjJjMTkyOTk0ZTI2NiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfOWZlYzIwM2Q0ZTI3NGJkZjliNzc2Mzg5NmMxYTcxODQgPSAkKGA8ZGl2IGlkPSJodG1sXzlmZWMyMDNkNGUyNzRiZGY5Yjc3NjM4OTZjMWE3MTg0IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UaGUgQW5uZXgsTm9ydGggTWlkdG93bixZb3JrdmlsbGUgQ2x1c3RlciAwPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzk0NDliNzI0YzMzMTRkY2M4MjIyMmMxOTI5OTRlMjY2LnNldENvbnRlbnQoaHRtbF85ZmVjMjAzZDRlMjc0YmRmOWI3NzYzODk2YzFhNzE4NCk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZjgyN2JlMzljOGY5NDU3YTkwMTExMWU5YTNlZTI0OTIuYmluZFBvcHVwKHBvcHVwXzk0NDliNzI0YzMzMTRkY2M4MjIyMmMxOTI5OTRlMjY2KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9mYWMyZTUzYmFjNTA0N2Q1OWI5YWQ5OTY1NzNmYmIzNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY2MjY5NTYsIC03OS40MDAwNDkzXSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzBlYTRiMDQ1ODY0ODQxYzliZGQ3YWU5M2Y5ZTIzOGJlID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF84ZjI4MTViY2Y4YTY0M2MxYmQ3YzJhNWNkNzFhOGFjOSA9ICQoYDxkaXYgaWQ9Imh0bWxfOGYyODE1YmNmOGE2NDNjMWJkN2MyYTVjZDcxYThhYzkiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhhcmJvcmQsVW5pdmVyc2l0eSBvZiBUb3JvbnRvIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8wZWE0YjA0NTg2NDg0MWM5YmRkN2FlOTNmOWUyMzhiZS5zZXRDb250ZW50KGh0bWxfOGYyODE1YmNmOGE2NDNjMWJkN2MyYTVjZDcxYThhYzkpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2ZhYzJlNTNiYWM1MDQ3ZDU5YjlhZDk5NjU3M2ZiYjM2LmJpbmRQb3B1cChwb3B1cF8wZWE0YjA0NTg2NDg0MWM5YmRkN2FlOTNmOWUyMzhiZSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZjM0MGM5NGIzZWUzNDkyYjkyMTZlZDFiYTdkNTUyNjQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NTMyMDU3LCAtNzkuNDAwMDQ5M10sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiIzgwMDBmZiIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjODAwMGZmIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF82ZjkxZDQyNzlmMTU0ZmE2YTE5ZjllYWYxYThkMmFiNiA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfYjc0ODM0MzEzNjNlNGZmZTk0ZjQ2YWI4Yjg2ZjIyNmMgPSAkKGA8ZGl2IGlkPSJodG1sX2I3NDgzNDMxMzYzZTRmZmU5NGY0NmFiOGI4NmYyMjZjIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5DaGluYXRvd24sR3JhbmdlIFBhcmssS2Vuc2luZ3RvbiBNYXJrZXQgQ2x1c3RlciAxPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzZmOTFkNDI3OWYxNTRmYTZhMTlmOWVhZjFhOGQyYWI2LnNldENvbnRlbnQoaHRtbF9iNzQ4MzQzMTM2M2U0ZmZlOTRmNDZhYjhiODZmMjI2Yyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfZjM0MGM5NGIzZWUzNDkyYjkyMTZlZDFiYTdkNTUyNjQuYmluZFBvcHVwKHBvcHVwXzZmOTFkNDI3OWYxNTRmYTZhMTlmOWVhZjFhOGQyYWI2KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl82NWY1M2M4MzExZTU0Y2IzYTAwNWNlNjNhNTFkNWZkZiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjYyODk0NjcsIC03OS4zOTQ0MTk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2RmN2E1YTcyYmU0MDQzYjg5Mjc2N2M3MWEyYjg1MmQ3ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9hYmY0ZmRhNjZhMmM0NTRhYWU2YzhmNWI2YzYwMDViYyA9ICQoYDxkaXYgaWQ9Imh0bWxfYWJmNGZkYTY2YTJjNDU0YWFlNmM4ZjViNmM2MDA1YmMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNOIFRvd2VyLEJhdGh1cnN0IFF1YXksSXNsYW5kIGFpcnBvcnQsSGFyYm91cmZyb250IFdlc3QsS2luZyBhbmQgU3BhZGluYSxSYWlsd2F5IExhbmRzLFNvdXRoIE5pYWdhcmEgQ2x1c3RlciAxPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2RmN2E1YTcyYmU0MDQzYjg5Mjc2N2M3MWEyYjg1MmQ3LnNldENvbnRlbnQoaHRtbF9hYmY0ZmRhNjZhMmM0NTRhYWU2YzhmNWI2YzYwMDViYyk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNjVmNTNjODMxMWU1NGNiM2EwMDVjZTYzYTUxZDVmZGYuYmluZFBvcHVwKHBvcHVwX2RmN2E1YTcyYmU0MDQzYjg5Mjc2N2M3MWEyYjg1MmQ3KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lYjk5MWI0NjIzYmI0NDdhYmM0N2Y1ODFmMzcyY2I4YSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY0NjQzNTIsIC03OS4zNzQ4NDU5OTk5OTk5OV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiIzgwMDBmZiIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjODAwMGZmIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8wM2FkYTk1ZTUwMzE0NmMxOTU4N2ExOTk3NGRjOGFlZCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfM2M0NmUzYmVlMzlkNDA0MTk2MDEwMTk3YmMyNmJhZDcgPSAkKGA8ZGl2IGlkPSJodG1sXzNjNDZlM2JlZTM5ZDQwNDE5NjAxMDE5N2JjMjZiYWQ3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5TdG4gQSBQTyBCb3hlcyAyNSBUaGUgRXNwbGFuYWRlIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF8wM2FkYTk1ZTUwMzE0NmMxOTU4N2ExOTk3NGRjOGFlZC5zZXRDb250ZW50KGh0bWxfM2M0NmUzYmVlMzlkNDA0MTk2MDEwMTk3YmMyNmJhZDcpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2ViOTkxYjQ2MjNiYjQ0N2FiYzQ3ZjU4MWYzNzJjYjhhLmJpbmRQb3B1cChwb3B1cF8wM2FkYTk1ZTUwMzE0NmMxOTU4N2ExOTk3NGRjOGFlZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODg0ZDNhYjU4NjNmNGRlMjg1NjdmY2Q5ZGZmZTY2MTIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDg0MjkyLCAtNzkuMzgyMjgwMl0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiI2ZmMDAwMCIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF83ZDliZjljZTUyODk0NzA2OTMzMmViZGQwNDk1MjQwZCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfMmFjODc4NjM5YzU5NDEwN2JhNWQzZDUzMmEwNTAyYjcgPSAkKGA8ZGl2IGlkPSJodG1sXzJhYzg3ODYzOWM1OTQxMDdiYTVkM2Q1MzJhMDUwMmI3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5GaXJzdCBDYW5hZGlhbiBQbGFjZSxVbmRlcmdyb3VuZCBjaXR5IENsdXN0ZXIgMDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83ZDliZjljZTUyODk0NzA2OTMzMmViZGQwNDk1MjQwZC5zZXRDb250ZW50KGh0bWxfMmFjODc4NjM5YzU5NDEwN2JhNWQzZDUzMmEwNTAyYjcpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzg4NGQzYWI1ODYzZjRkZTI4NTY3ZmNkOWRmZmU2NjEyLmJpbmRQb3B1cChwb3B1cF83ZDliZjljZTUyODk0NzA2OTMzMmViZGQwNDk1MjQwZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzdkZWM0MTA2YTU5NDI5OThkOGVlNTQ4YmZmNjVjZDcgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42Njk1NDIsIC03OS40MjI1NjM3XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzUzZDkwNDZlMjU2MDQ2Y2Q4YzE3NzYyMjc3MThhODdkID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF83ODU5MGUwOWY1OWY0MmIyYjI0ZGZjNTY1MTQ4YThhNCA9ICQoYDxkaXYgaWQ9Imh0bWxfNzg1OTBlMDlmNTlmNDJiMmIyNGRmYzU2NTE0OGE4YTQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNocmlzdGllIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF81M2Q5MDQ2ZTI1NjA0NmNkOGMxNzc2MjI3NzE4YTg3ZC5zZXRDb250ZW50KGh0bWxfNzg1OTBlMDlmNTlmNDJiMmIyNGRmYzU2NTE0OGE4YTQpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzM3ZGVjNDEwNmE1OTQyOTk4ZDhlZTU0OGJmZjY1Y2Q3LmJpbmRQb3B1cChwb3B1cF81M2Q5MDQ2ZTI1NjA0NmNkOGMxNzc2MjI3NzE4YTg3ZCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTM0MDFmNDExNTU2NDMyNmJkN2U0ODdmOTlhNDE4NWQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjkwMDUxMDAwMDAwMSwgLTc5LjQ0MjI1OTNdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiM4MDAwZmYiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNGNkZDQ5OTY5MDkxNGE0NmI2NjJiMDQxZTU1YjQ0YTIgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sXzFhMjVlY2Y5ZTMyZTQ1ZDQ4NzI3ZjM3YTg5YTNlZWMxID0gJChgPGRpdiBpZD0iaHRtbF8xYTI1ZWNmOWUzMmU0NWQ0ODcyN2YzN2E4OWEzZWVjMSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RG92ZXJjb3VydCBWaWxsYWdlLER1ZmZlcmluIENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF80Y2RkNDk5NjkwOTE0YTQ2YjY2MmIwNDFlNTViNDRhMi5zZXRDb250ZW50KGh0bWxfMWEyNWVjZjllMzJlNDVkNDg3MjdmMzdhODlhM2VlYzEpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyX2EzNDAxZjQxMTU1NjQzMjZiZDdlNDg3Zjk5YTQxODVkLmJpbmRQb3B1cChwb3B1cF80Y2RkNDk5NjkwOTE0YTQ2YjY2MmIwNDFlNTViNDRhMikKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMzEyZjkwMDliNDRjNGRmZGI3NDRjNzQxODQ0MmFjNjAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NDc5MjY3MDAwMDAwMDYsIC03OS40MTk3NDk3XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzczMjU5NzVhYzNhODRhZmE4ZDdhMWM3ZDIwZmM0NTU0ID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9lZmIzYjE3ZWY3MGI0OWNkODc3OTgyNWUzN2M1ZDk2ZCA9ICQoYDxkaXYgaWQ9Imh0bWxfZWZiM2IxN2VmNzBiNDljZDg3Nzk4MjVlMzdjNWQ5NmQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkxpdHRsZSBQb3J0dWdhbCxUcmluaXR5IENsdXN0ZXIgMTwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF83MzI1OTc1YWMzYTg0YWZhOGQ3YTFjN2QyMGZjNDU1NC5zZXRDb250ZW50KGh0bWxfZWZiM2IxN2VmNzBiNDljZDg3Nzk4MjVlMzdjNWQ5NmQpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzMxMmY5MDA5YjQ0YzRkZmRiNzQ0Yzc0MTg0NDJhYzYwLmJpbmRQb3B1cChwb3B1cF83MzI1OTc1YWMzYTg0YWZhOGQ3YTFjN2QyMGZjNDU1NCkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNjViMTlhOTNlNjg5NDUzOGJmMjk4ODFkNzNmNjVmMmQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42MzY4NDcyLCAtNzkuNDI4MTkxNDAwMDAwMDJdLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiNmZjAwMDAiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfZTJkZThlZGU2OWNhNDY4NmEwZDQyYjI0OTQxODNlNDcgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2E3OTVmYWNiNWJiODQzZTQ4YjZlZjhhOGY1NmVhMzNlID0gJChgPGRpdiBpZD0iaHRtbF9hNzk1ZmFjYjViYjg0M2U0OGI2ZWY4YThmNTZlYTMzZSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QnJvY2t0b24sRXhoaWJpdGlvbiBQbGFjZSxQYXJrZGFsZSBWaWxsYWdlIENsdXN0ZXIgMDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF9lMmRlOGVkZTY5Y2E0Njg2YTBkNDJiMjQ5NDE4M2U0Ny5zZXRDb250ZW50KGh0bWxfYTc5NWZhY2I1YmI4NDNlNDhiNmVmOGE4ZjU2ZWEzM2UpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzY1YjE5YTkzZTY4OTQ1MzhiZjI5ODgxZDczZjY1ZjJkLmJpbmRQb3B1cChwb3B1cF9lMmRlOGVkZTY5Y2E0Njg2YTBkNDJiMjQ5NDE4M2U0NykKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNTc3ZDI5ODg0ODg3NDU3Yjk0ZWY0YjlmMzA4Y2Q0MGEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjE2MDgzLCAtNzkuNDY0NzYzMjk5OTk5OTldLAogICAgICAgICAgICAgICAgeyJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwgImNvbG9yIjogIiM4MDAwZmYiLCAiZGFzaEFycmF5IjogbnVsbCwgImRhc2hPZmZzZXQiOiBudWxsLCAiZmlsbCI6IHRydWUsICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsICJmaWxsT3BhY2l0eSI6IDAuNywgImZpbGxSdWxlIjogImV2ZW5vZGQiLCAibGluZUNhcCI6ICJyb3VuZCIsICJsaW5lSm9pbiI6ICJyb3VuZCIsICJvcGFjaXR5IjogMS4wLCAicmFkaXVzIjogNSwgInN0cm9rZSI6IHRydWUsICJ3ZWlnaHQiOiAzfQogICAgICAgICAgICApLmFkZFRvKG1hcF8wNGI5ZTk4ZmI2Yzg0YjExODY4N2UwYTg3ZjUzYzc5YSk7CiAgICAgICAgCiAgICAKICAgICAgICB2YXIgcG9wdXBfNGJkODMyNDQ3OGVmNDczZjgxZDFiNjQ2YzUxMmUyOGEgPSBMLnBvcHVwKHsibWF4V2lkdGgiOiAiMTAwJSJ9KTsKCiAgICAgICAgCiAgICAgICAgICAgIHZhciBodG1sX2RiODAyYjE4N2Y4NzQyODE4YzI3NmZjZjVmNjY0YWM0ID0gJChgPGRpdiBpZD0iaHRtbF9kYjgwMmIxODdmODc0MjgxOGMyNzZmY2Y1ZjY2NGFjNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+SGlnaCBQYXJrLFRoZSBKdW5jdGlvbiBTb3V0aCBDbHVzdGVyIDE8L2Rpdj5gKVswXTsKICAgICAgICAgICAgcG9wdXBfNGJkODMyNDQ3OGVmNDczZjgxZDFiNjQ2YzUxMmUyOGEuc2V0Q29udGVudChodG1sX2RiODAyYjE4N2Y4NzQyODE4YzI3NmZjZjVmNjY0YWM0KTsKICAgICAgICAKCiAgICAgICAgY2lyY2xlX21hcmtlcl81NzdkMjk4ODQ4ODc0NTdiOTRlZjRiOWYzMDhjZDQwYS5iaW5kUG9wdXAocG9wdXBfNGJkODMyNDQ3OGVmNDczZjgxZDFiNjQ2YzUxMmUyOGEpCiAgICAgICAgOwoKICAgICAgICAKICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzU5OGIzZWQzYTJjZTQ4ZTg4MzliZGI5MTFhNWUzOTZkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDMuNjQ4OTU5NywgLTc5LjQ1NjMyNV0sCiAgICAgICAgICAgICAgICB7ImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLCAiY29sb3IiOiAiIzgwMDBmZiIsICJkYXNoQXJyYXkiOiBudWxsLCAiZGFzaE9mZnNldCI6IG51bGwsICJmaWxsIjogdHJ1ZSwgImZpbGxDb2xvciI6ICIjODAwMGZmIiwgImZpbGxPcGFjaXR5IjogMC43LCAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsICJsaW5lQ2FwIjogInJvdW5kIiwgImxpbmVKb2luIjogInJvdW5kIiwgIm9wYWNpdHkiOiAxLjAsICJyYWRpdXMiOiA1LCAic3Ryb2tlIjogdHJ1ZSwgIndlaWdodCI6IDN9CiAgICAgICAgICAgICkuYWRkVG8obWFwXzA0YjllOThmYjZjODRiMTE4Njg3ZTBhODdmNTNjNzlhKTsKICAgICAgICAKICAgIAogICAgICAgIHZhciBwb3B1cF8wMjIxMDFkZTVmY2M0M2Q4YTIzMGYyMTdjOWUxNGY0OCA9IEwucG9wdXAoeyJtYXhXaWR0aCI6ICIxMDAlIn0pOwoKICAgICAgICAKICAgICAgICAgICAgdmFyIGh0bWxfZDI2ZTQyMzQxMWEyNGQzYTgxY2IxNDNiNmM5NDVhZGEgPSAkKGA8ZGl2IGlkPSJodG1sX2QyNmU0MjM0MTFhMjRkM2E4MWNiMTQzYjZjOTQ1YWRhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5QYXJrZGFsZSxSb25jZXN2YWxsZXMgQ2x1c3RlciAxPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwXzAyMjEwMWRlNWZjYzQzZDhhMjMwZjIxN2M5ZTE0ZjQ4LnNldENvbnRlbnQoaHRtbF9kMjZlNDIzNDExYTI0ZDNhODFjYjE0M2I2Yzk0NWFkYSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNTk4YjNlZDNhMmNlNDhlODgzOWJkYjkxMWE1ZTM5NmQuYmluZFBvcHVwKHBvcHVwXzAyMjEwMWRlNWZjYzQzZDhhMjMwZjIxN2M5ZTE0ZjQ4KQogICAgICAgIDsKCiAgICAgICAgCiAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl83ZWJkYzg2N2I4ZjI0MGFjYjFlMzc2MTJlYTk5MjM1MSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQzLjY1MTU3MDYsIC03OS40ODQ0NDk5XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjZmYwMDAwIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiNmZjAwMDAiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwXzQ5YmExM2U4ZDIyNTRkMWZhYjRmOThmNGRhNWM4YTExID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9hZTU2YTA5ZjI1ZTI0MmQ4YmE4Y2VlN2FlM2Y0ZWZkNSA9ICQoYDxkaXYgaWQ9Imh0bWxfYWU1NmEwOWYyNWUyNDJkOGJhOGNlZTdhZTNmNGVmZDUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlJ1bm55bWVkZSxTd2Fuc2VhIENsdXN0ZXIgMDwvZGl2PmApWzBdOwogICAgICAgICAgICBwb3B1cF80OWJhMTNlOGQyMjU0ZDFmYWI0Zjk4ZjRkYTVjOGExMS5zZXRDb250ZW50KGh0bWxfYWU1NmEwOWYyNWUyNDJkOGJhOGNlZTdhZTNmNGVmZDUpOwogICAgICAgIAoKICAgICAgICBjaXJjbGVfbWFya2VyXzdlYmRjODY3YjhmMjQwYWNiMWUzNzYxMmVhOTkyMzUxLmJpbmRQb3B1cChwb3B1cF80OWJhMTNlOGQyMjU0ZDFmYWI0Zjk4ZjRkYTVjOGExMSkKICAgICAgICA7CgogICAgICAgIAogICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNDAyMGU3YWQyYjc5NDQ1MzhlNzY2OWY3YzExMDAxN2EgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0My42NjI3NDM5LCAtNzkuMzIxNTU4XSwKICAgICAgICAgICAgICAgIHsiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsICJjb2xvciI6ICIjODAwMGZmIiwgImRhc2hBcnJheSI6IG51bGwsICJkYXNoT2Zmc2V0IjogbnVsbCwgImZpbGwiOiB0cnVlLCAiZmlsbENvbG9yIjogIiM4MDAwZmYiLCAiZmlsbE9wYWNpdHkiOiAwLjcsICJmaWxsUnVsZSI6ICJldmVub2RkIiwgImxpbmVDYXAiOiAicm91bmQiLCAibGluZUpvaW4iOiAicm91bmQiLCAib3BhY2l0eSI6IDEuMCwgInJhZGl1cyI6IDUsICJzdHJva2UiOiB0cnVlLCAid2VpZ2h0IjogM30KICAgICAgICAgICAgKS5hZGRUbyhtYXBfMDRiOWU5OGZiNmM4NGIxMTg2ODdlMGE4N2Y1M2M3OWEpOwogICAgICAgIAogICAgCiAgICAgICAgdmFyIHBvcHVwX2ViZjIyMTVjMjVmYzQzMjI5Yzk0MTI3YzJlNjgxNzdhID0gTC5wb3B1cCh7Im1heFdpZHRoIjogIjEwMCUifSk7CgogICAgICAgIAogICAgICAgICAgICB2YXIgaHRtbF9jOTVhODRiZDE4Zjk0NjhjYmRkZDJjY2QyNWE4MjdlZSA9ICQoYDxkaXYgaWQ9Imh0bWxfYzk1YTg0YmQxOGY5NDY4Y2JkZGQyY2NkMjVhODI3ZWUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJ1c2luZXNzIFJlcGx5IE1haWwgUHJvY2Vzc2luZyBDZW50cmUgOTY5IEVhc3Rlcm4gQ2x1c3RlciAxPC9kaXY+YClbMF07CiAgICAgICAgICAgIHBvcHVwX2ViZjIyMTVjMjVmYzQzMjI5Yzk0MTI3YzJlNjgxNzdhLnNldENvbnRlbnQoaHRtbF9jOTVhODRiZDE4Zjk0NjhjYmRkZDJjY2QyNWE4MjdlZSk7CiAgICAgICAgCgogICAgICAgIGNpcmNsZV9tYXJrZXJfNDAyMGU3YWQyYjc5NDQ1MzhlNzY2OWY3YzExMDAxN2EuYmluZFBvcHVwKHBvcHVwX2ViZjIyMTVjMjVmYzQzMjI5Yzk0MTI3YzJlNjgxNzdhKQogICAgICAgIDsKCiAgICAgICAgCiAgICAKPC9zY3JpcHQ+" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



### Explore clusters


```python
toronto_merged.loc[toronto_merged['Cluster Labels'] == 0, toronto_merged.columns[[1] + list(range(5, toronto_merged.shape[1]))]]
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
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>East Toronto</td>
      <td>0</td>
      <td>Trail</td>
      <td>Pub</td>
      <td>Health Food Store</td>
      <td>Other Great Outdoors</td>
      <td>Wine Bar</td>
      <td>Diner</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Central Toronto</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Pub</td>
      <td>Supermarket</td>
      <td>Sports Bar</td>
      <td>Restaurant</td>
      <td>Liquor Store</td>
      <td>American Restaurant</td>
      <td>Sushi Restaurant</td>
      <td>Dance Studio</td>
      <td>Cuban Restaurant</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Downtown Toronto</td>
      <td>0</td>
      <td>Breakfast Spot</td>
      <td>Park</td>
      <td>Historic Site</td>
      <td>Coffee Shop</td>
      <td>Restaurant</td>
      <td>Spa</td>
      <td>Pub</td>
      <td>Bakery</td>
      <td>Gym / Fitness Center</td>
      <td>Dessert Shop</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Downtown Toronto</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Gastropub</td>
      <td>Gym</td>
      <td>Italian Restaurant</td>
      <td>Restaurant</td>
      <td>BBQ Joint</td>
      <td>Japanese Restaurant</td>
      <td>Food Truck</td>
      <td>Creperie</td>
      <td>Cuban Restaurant</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Downtown Toronto</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Sushi Restaurant</td>
      <td>Gastropub</td>
      <td>Park</td>
      <td>Modern European Restaurant</td>
      <td>Spa</td>
      <td>Italian Restaurant</td>
      <td>Ramen Restaurant</td>
      <td>Creperie</td>
      <td>Dance Studio</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Downtown Toronto</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Gastropub</td>
      <td>Pub</td>
      <td>Restaurant</td>
      <td>Beer Bar</td>
      <td>Café</td>
      <td>Gym</td>
      <td>Gym / Fitness Center</td>
      <td>Hotel</td>
      <td>Dessert Shop</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Downtown Toronto</td>
      <td>0</td>
      <td>Café</td>
      <td>Gastropub</td>
      <td>American Restaurant</td>
      <td>Coffee Shop</td>
      <td>Restaurant</td>
      <td>Pub</td>
      <td>Gym / Fitness Center</td>
      <td>Gym</td>
      <td>Museum</td>
      <td>Diner</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Central Toronto</td>
      <td>0</td>
      <td>Café</td>
      <td>Park</td>
      <td>American Restaurant</td>
      <td>Pub</td>
      <td>Burger Joint</td>
      <td>Coffee Shop</td>
      <td>BBQ Joint</td>
      <td>Indian Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Food &amp; Drink Shop</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Downtown Toronto</td>
      <td>0</td>
      <td>Café</td>
      <td>Gastropub</td>
      <td>Gym</td>
      <td>Pizza Place</td>
      <td>Restaurant</td>
      <td>Steakhouse</td>
      <td>Gym / Fitness Center</td>
      <td>Coffee Shop</td>
      <td>American Restaurant</td>
      <td>Food &amp; Drink Shop</td>
    </tr>
    <tr>
      <th>33</th>
      <td>West Toronto</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Gym</td>
      <td>Italian Restaurant</td>
      <td>Bar</td>
      <td>Café</td>
      <td>Pet Store</td>
      <td>Caribbean Restaurant</td>
      <td>Furniture / Home Store</td>
      <td>Breakfast Spot</td>
      <td>Cosmetics Shop</td>
    </tr>
    <tr>
      <th>36</th>
      <td>West Toronto</td>
      <td>0</td>
      <td>Sushi Restaurant</td>
      <td>Coffee Shop</td>
      <td>Italian Restaurant</td>
      <td>Pub</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Burrito Place</td>
      <td>Food</td>
      <td>Tea Room</td>
      <td>Café</td>
      <td>Cosmetics Shop</td>
    </tr>
  </tbody>
</table>
</div>



### Cluster 2


```python
toronto_merged.loc[toronto_merged['Cluster Labels'] == 1, toronto_merged.columns[[1] + list(range(5, toronto_merged.shape[1]))]]
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
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>East Toronto</td>
      <td>1</td>
      <td>Greek Restaurant</td>
      <td>Ice Cream Shop</td>
      <td>Yoga Studio</td>
      <td>Cosmetics Shop</td>
      <td>Pub</td>
      <td>Italian Restaurant</td>
      <td>Brewery</td>
      <td>Dog Run</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Toronto</td>
      <td>1</td>
      <td>Gym</td>
      <td>Sushi Restaurant</td>
      <td>Ice Cream Shop</td>
      <td>Burger Joint</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Liquor Store</td>
      <td>Brewery</td>
      <td>Italian Restaurant</td>
      <td>Pet Store</td>
      <td>Park</td>
    </tr>
    <tr>
      <th>3</th>
      <td>East Toronto</td>
      <td>1</td>
      <td>Gay Bar</td>
      <td>Fish Market</td>
      <td>Cheese Shop</td>
      <td>Sandwich Place</td>
      <td>Seafood Restaurant</td>
      <td>Coffee Shop</td>
      <td>Ice Cream Shop</td>
      <td>Bakery</td>
      <td>Bookstore</td>
      <td>Flea Market</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Central Toronto</td>
      <td>1</td>
      <td>Park</td>
      <td>Food &amp; Drink Shop</td>
      <td>Clothing Store</td>
      <td>Dance Studio</td>
      <td>Hotel</td>
      <td>Sandwich Place</td>
      <td>Breakfast Spot</td>
      <td>Gym</td>
      <td>Concert Hall</td>
      <td>Creperie</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Central Toronto</td>
      <td>1</td>
      <td>Yoga Studio</td>
      <td>Sporting Goods Shop</td>
      <td>Coffee Shop</td>
      <td>Mexican Restaurant</td>
      <td>Restaurant</td>
      <td>Dessert Shop</td>
      <td>Salon / Barbershop</td>
      <td>Diner</td>
      <td>Spa</td>
      <td>Chinese Restaurant</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Central Toronto</td>
      <td>1</td>
      <td>Dessert Shop</td>
      <td>Park</td>
      <td>Sushi Restaurant</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Pizza Place</td>
      <td>Italian Restaurant</td>
      <td>Seafood Restaurant</td>
      <td>Indian Restaurant</td>
      <td>Fish Market</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Café</td>
      <td>General Entertainment</td>
      <td>Bakery</td>
      <td>Diner</td>
      <td>Restaurant</td>
      <td>Jewelry Store</td>
      <td>Japanese Restaurant</td>
      <td>Italian Restaurant</td>
      <td>Indian Restaurant</td>
      <td>Fish Market</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Bookstore</td>
      <td>Bubble Tea Shop</td>
      <td>Theme Restaurant</td>
      <td>Restaurant</td>
      <td>Mexican Restaurant</td>
      <td>Tea Room</td>
      <td>Ramen Restaurant</td>
      <td>Breakfast Spot</td>
      <td>Salon / Barbershop</td>
      <td>Dance Studio</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Café</td>
      <td>Burrito Place</td>
      <td>Plaza</td>
      <td>Clothing Store</td>
      <td>Theater</td>
      <td>Comic Shop</td>
      <td>Tea Room</td>
      <td>Ramen Restaurant</td>
      <td>Pizza Place</td>
      <td>Cuban Restaurant</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Park</td>
      <td>Steakhouse</td>
      <td>Museum</td>
      <td>Concert Hall</td>
      <td>Liquor Store</td>
      <td>Farmers Market</td>
      <td>Cocktail Bar</td>
      <td>French Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Thai Restaurant</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Seafood Restaurant</td>
      <td>Asian Restaurant</td>
      <td>Concert Hall</td>
      <td>Plaza</td>
      <td>Hotel</td>
      <td>Speakeasy</td>
      <td>Steakhouse</td>
      <td>Opera House</td>
      <td>Greek Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Supermarket</td>
      <td>Salad Place</td>
      <td>Hotel</td>
      <td>Sporting Goods Shop</td>
      <td>Plaza</td>
      <td>Lake</td>
      <td>Dessert Shop</td>
      <td>Performing Arts Venue</td>
      <td>Park</td>
      <td>Comic Shop</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Bookstore</td>
      <td>Dessert Shop</td>
      <td>Restaurant</td>
      <td>College Gym</td>
      <td>Beer Bar</td>
      <td>Bar</td>
      <td>Bakery</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>French Restaurant</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Café</td>
      <td>Organic Grocery</td>
      <td>Bar</td>
      <td>Bakery</td>
      <td>Mexican Restaurant</td>
      <td>Arts &amp; Crafts Store</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>Cosmetics Shop</td>
      <td>Creperie</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Airport Lounge</td>
      <td>Boutique</td>
      <td>Bar</td>
      <td>Airport</td>
      <td>Airport Food Court</td>
      <td>Airport Gate</td>
      <td>Airport Terminal</td>
      <td>Coffee Shop</td>
      <td>Harbor / Marina</td>
      <td>Farmers Market</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Park</td>
      <td>Concert Hall</td>
      <td>French Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Fountain</td>
      <td>Thai Restaurant</td>
      <td>Tea Room</td>
      <td>Cocktail Bar</td>
      <td>Museum</td>
      <td>Steakhouse</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Downtown Toronto</td>
      <td>1</td>
      <td>Café</td>
      <td>Grocery Store</td>
      <td>Candy Store</td>
      <td>Restaurant</td>
      <td>Diner</td>
      <td>Italian Restaurant</td>
      <td>Coffee Shop</td>
      <td>Wine Bar</td>
      <td>Dog Run</td>
      <td>Comic Shop</td>
    </tr>
    <tr>
      <th>31</th>
      <td>West Toronto</td>
      <td>1</td>
      <td>Bakery</td>
      <td>Supermarket</td>
      <td>Music Venue</td>
      <td>Middle Eastern Restaurant</td>
      <td>Bar</td>
      <td>Pharmacy</td>
      <td>Gym / Fitness Center</td>
      <td>Brewery</td>
      <td>Café</td>
      <td>Dance Studio</td>
    </tr>
    <tr>
      <th>32</th>
      <td>West Toronto</td>
      <td>1</td>
      <td>Wine Bar</td>
      <td>Pizza Place</td>
      <td>Asian Restaurant</td>
      <td>Bar</td>
      <td>Brewery</td>
      <td>Cuban Restaurant</td>
      <td>Greek Restaurant</td>
      <td>Ice Cream Shop</td>
      <td>Korean Restaurant</td>
      <td>Yoga Studio</td>
    </tr>
    <tr>
      <th>34</th>
      <td>West Toronto</td>
      <td>1</td>
      <td>Park</td>
      <td>Arts &amp; Crafts Store</td>
      <td>Gastropub</td>
      <td>Café</td>
      <td>Italian Restaurant</td>
      <td>Bar</td>
      <td>Speakeasy</td>
      <td>Flea Market</td>
      <td>Bookstore</td>
      <td>Furniture / Home Store</td>
    </tr>
    <tr>
      <th>35</th>
      <td>West Toronto</td>
      <td>1</td>
      <td>Gift Shop</td>
      <td>Italian Restaurant</td>
      <td>Eastern European Restaurant</td>
      <td>Movie Theater</td>
      <td>Cuban Restaurant</td>
      <td>Restaurant</td>
      <td>Dessert Shop</td>
      <td>Dog Run</td>
      <td>Coffee Shop</td>
      <td>Flea Market</td>
    </tr>
    <tr>
      <th>37</th>
      <td>East Toronto</td>
      <td>1</td>
      <td>Garden Center</td>
      <td>Pizza Place</td>
      <td>Restaurant</td>
      <td>Skate Park</td>
      <td>Farmers Market</td>
      <td>Fast Food Restaurant</td>
      <td>Auto Workshop</td>
      <td>Burrito Place</td>
      <td>Comic Shop</td>
      <td>Brewery</td>
    </tr>
  </tbody>
</table>
</div>



### Cluster 3


```python
toronto_merged.loc[toronto_merged['Cluster Labels'] == 2, toronto_merged.columns[[1] + list(range(5, toronto_merged.shape[1]))]]
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
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>Central Toronto</td>
      <td>2</td>
      <td>Park</td>
      <td>Swim School</td>
      <td>Bus Line</td>
      <td>Dog Run</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
      <td>Concert Hall</td>
      <td>Cosmetics Shop</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Downtown Toronto</td>
      <td>2</td>
      <td>Park</td>
      <td>Trail</td>
      <td>Playground</td>
      <td>Dog Run</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
      <td>Concert Hall</td>
      <td>Cosmetics Shop</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Central Toronto</td>
      <td>2</td>
      <td>Park</td>
      <td>Trail</td>
      <td>Sushi Restaurant</td>
      <td>Jewelry Store</td>
      <td>Dog Run</td>
      <td>Cocktail Bar</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
      <td>Concert Hall</td>
    </tr>
  </tbody>
</table>
</div>



### Cluster 4


```python
toronto_merged.loc[toronto_merged['Cluster Labels'] == 3, toronto_merged.columns[[1] + list(range(5, toronto_merged.shape[1]))]]
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
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22</th>
      <td>Central Toronto</td>
      <td>3</td>
      <td>Garden</td>
      <td>Wine Bar</td>
      <td>Eastern European Restaurant</td>
      <td>Coffee Shop</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
      <td>Concert Hall</td>
      <td>Cosmetics Shop</td>
      <td>Creperie</td>
      <td>Cuban Restaurant</td>
    </tr>
  </tbody>
</table>
</div>



### Cluster 5


```python
toronto_merged.loc[toronto_merged['Cluster Labels'] == 4, toronto_merged.columns[[1] + list(range(5, toronto_merged.shape[1]))]]
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
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>Central Toronto</td>
      <td>4</td>
      <td>Gym</td>
      <td>Wine Bar</td>
      <td>Farmers Market</td>
      <td>College Gym</td>
      <td>Comic Shop</td>
      <td>Concert Hall</td>
      <td>Cosmetics Shop</td>
      <td>Creperie</td>
      <td>Cuban Restaurant</td>
      <td>Dance Studio</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
