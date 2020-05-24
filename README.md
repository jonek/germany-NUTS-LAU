# Maps of NUTS and LAU subdivisions in Germany

This project's goal is to prepare publicly available Open Data to be easily used in your web based mapping projects.

## Structure of data

* **NUTS:** Nomenclature of territorial units for statistics [Wikipedia](https://en.wikipedia.org/wiki/NUTS_statistical_regions_of_Germany)  
  Consist of three levels:

  * **NUTS 1** countries
  * **NUTS 2** 
    * federal countries (German: Bundesländer [Wikipedia](https://en.wikipedia.org/wiki/States_of_Germany))
    * Regierungsbezirk (German - a subdivision of some of the federal countries [Wikipedia](https://en.wikipedia.org/wiki/Regierungsbezirk))
  * **NUTS 3** districts (German: Kreise [Wikipedia](https://en.wikipedia.org/wiki/Districts_of_Germany))

  These levels are subdivisions of each other.

* **LAU:** Local Administrative Units  
  A subdivision of the **NUTS 3** level. This corresponds to municipalities and communes (German: Gemeinden [Wikipedia](https://en.wikipedia.org/wiki/Municipalities_of_Germany)).


## LAU

**Source:** https://ec.europa.eu/eurostat/web/nuts/local-administrative-units
**File:** `EU-28-LAU-2019-NUTS-2016.xlsx` https://ec.europa.eu/eurostat/documents/345175/501971/EU-28-LAU-2019-NUTS-2016.xlsx

**Converted to:** `germany-LAU-2019.csv` _(manually)_

### LAU - Geo Data

**Source:** https://ec.europa.eu/eurostat/web/gisco/geodata/reference-data/administrative-units-statistical-units/lau  
**File:** `LAU-2018-01M-SH.zip` https://ec.europa.eu/eurostat/cache/GISCO/geodatafiles/LAU-2018-01M-SH.zip

Inspect the shape file:
```
$ ogrinfo -so -al LAU_2018.shp
$ dbview LAU_2018.dbf | head -12
$ dbview -b -d ',' -t LAU_2018.dbf | grep DE_ | head -10
$ mapshaper LAU_2018.shp -calc 'count()' where='GISCO_ID.startsWith("DE")'
[calc] count() where GISCO_ID.startsWith("DE"):  11119
```

**Converted to:** `germany-LAU-2019.topo.json` using command:
```
$ mapshaper LAU_2018.shp -filter 'GISCO_ID.startsWith("DE")' -proj merc -o germany-LAU-2019.topo.json format=topojson
```

## Copyright

For NUTS and LAU data:  
EN: © EuroGeographics for the administrative boundaries

For further info, see: [Copyright notice @ eurostat](https://ec.europa.eu/eurostat/web/gisco/geodata/reference-data/administrative-units-statistical-units)
