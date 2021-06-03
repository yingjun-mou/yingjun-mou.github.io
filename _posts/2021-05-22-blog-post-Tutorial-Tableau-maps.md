---
title: 'Tableau country maps overlay with more specific locations'
date: 2021-05-22
permalink: /posts/2021/05/Tableau map/
tags:
  - Geo Data
categories:
  - Map
  - Tutorial
---


Tableau country maps overlay with more specific locations
======

[youtube link](https://www.youtube.com/watch?v=KDMGS9eE8ks) 

## 1. Open Tableau, instead of import, directly **Open** the csv file:
- Go to the sheet

## 2. Create generated Lat and Long:
- The inputs are countries, right click country names and choose the **Geographic Roles** to be **Country/Region**
- There will be two new meassure fields created call *Latitude(generated)* and *Longitude(generated)*
- Drag Long to Columns, Lat to Rows

## 3. Create color calculation function:
- Right click meassure tab
- Click **Create calculated field**
- Give it a name such as color calculation, for the function, types:
```
IF MAX([Time]) >= 5 then 'years'
ELSEIF MAX([Time]) == 4 then 'months'
ELSEIF MAX([Time]) == 3 then 'weeks'
ELSEIF MAX([Time]) == 2 then 'days'
ELSEIF MAX([Time]) == 1 then 'passby'
ELSEIF MAX([Time]) == NULL then 'no'
END
```


## 4. Apply the color gradient:
- Drag Color Calculation to *Color*
- Tweak the color, personally, I found the following parameters to be the best
1. Opacity = 40%
2. year = RGB(170,0,0)
3. months = RGB(206,68,68)
4. weeks = RGB(224,136,136)
5. days = RGB(255,134,134)
6. passby = RGB(255,240,240)
7. Null = RGB(159,159,159)
8. Border = RGB(245,245,245)

## 5. Show the country name:
- Drag *Name* to the **Detail** field.

## 6. Show the specific city/attraction name:
- Duplicate Lattitude in the Rows
- For the new map, there will be 4 properties:
1. Country Name - as Detail
2. City - as Detail
3. Lat(of city) - as Detail
4. Long(of city) - as Detail
- Apply **Dual Axis** to merge the two maps


## 7. Put map into a Dashboard:
- Drag Sheet to a new Dashboard
- **Map** -> **Options** -> Uncheck **Allow pan and zoom**
- Hide unnecessary visual elements
- Save to Tableau Public

