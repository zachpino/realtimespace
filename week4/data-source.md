### Sourcing Data
-----

With a census API key, we can pull down data to embed in our census tract vectors.

```curl 'http://api.census.gov/data/2015/acs5?get=B01003_001E&for=tract:*&in=state:17&key=e0f41b3ce147e2d2ca2d7ee4085fbefd43c142a5' -o il_2015_tract_key.json```
