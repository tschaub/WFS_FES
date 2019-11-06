
0. beamMode is ScanSAR Narrow AND swathDirection is ascending AND
   polarization is "HH+VV+HV+VH" and intersects geom(Washington DC)

CQL
```
beamMode='ScanSAR Narrow' AND
swathDirection='ascending' AND 
polarization='HH+VV+HV+VH' AND
intersects(geometry,POLYGON((-77.117938 38.936860,-77.040604 39.995648,-76.910536 38.892912,-77.039359 38.791753,-77.047906 38.841462,-77.034183 38.840655,-77.033142 38.857490)))
```

CQL JSON
```json
[
  "and",
  ["eq", ["property", "beamMode"], "ScanSAR Narrow"],
  ["eq", ["property", "swathDirection"], "ascending"],
  ["eq", ["property", "polarization"], "HH+VV+HV+VH"],
  ["intersects",
    ["property", "footprint"],
    {
      "type": "Polygon",
      "coordinates": [[
        [-77.117938,38.936860],
        [-77.040604,39.995648],
        [-76.910536,38.892912],
        [-77.039359,38.791753],
        [-77.047906,38.841462],
        [-77.034183,38.840655],
        [-77.033142,38.857490]
      ]]
    }
  ]
]
```

1. Floors greater than 5

CQL
```
floors>5
```

CQL JSON
```json
[
  "gt",
  ["property", "floor"],
  5
]
```

2. Taxes less than or equal to 500

CQL
```
taxes <= 500
```

CQL JSON
```json
[
  "lte",
  ["property", "taxes"],
  500
]
```

3. Owner name contains 'Jones'

CQL
```
owner LIKE '% Jones %'
```

CQL JSON
```json
[
  "like",
  ["property", "owner_name"],
  "% Jones %"
]
```

4. Owner name starts with 'Mike'

CQL
```
owner_name LIKE 'Mike%'
```

CQL JSON
```json
[
  "like",
  ["property", "owner_name"],
  "Mike%",
  {"wildCards": "%"}
]
```


5. Owner name does not contain 'Mike'

CQL
```
owner_name NOT LIKE '% Mike %'
```

CQL JSON
```json
[
  "not",
  [
    "like",
    ["property", "owner_name"],
    "% Mike %"
  ]
]
```

6. A swimming pool

CQL
```
swimming_pool=true
```

CQL JSON
```json
[
  "eq",
  ["property", "swimming_pool"],
  true
]
```

7. More than 5 floors and a swimming pool

CQL
```
floors>5 AND swimming_pool=true
```

CQL JSON
```json
[
  "and",
  [
    "gt",
    ["property", "floor"],
    5
  ],
  [
    "eq",
    ["property", "swimming_pool"],
    true
  ]
]
```

8. A swimming pool and (more than five floors or material is like brick)

CQL
```
swimming_pool=true AND (floors>5 OR material LIKE '%brick')
```

CQL JSON
```json
[
  "and",
  [
    "eq",
    ["property", "swimming_pool"],
    true
  ],
  [
    "or",
    [
      "gt",
      ["property", "floor"],
      5
    ],
    [
      "like",
      ["property", "material"],
      "%brick"
    ]
  ]
]
```

9. (More than five floors and material is brick) or swimming pool is true

CQL
```
(floors>5 AND metrial='brick') OR swimming_pool=true
```

CQL JSON
```json
[
  "or",
  [
    "and",
    [
      "gt",
      ["property", "floors"],
      5
    ],
    [
      "eq",
      ["property", "material"],
      "brick"
    ]
  ],
  [
    "eq",
    ["property", "swimming_pool"],
    true
  ]
]
```

10. Not under 5 floors or a swimming pool

CQL
```
NOT (floors<5) OR swimming_pool=true
```

CQL JSON
```json
[
  "or",
  [
    "not",
    [
      "lt",
      ["property", "floors"],
      5
    ]
  ],
  [
    "eq",
    ["property", "swimming_pool"],
    true
  ]
]
```

11. Owner name starts with 'mike' or 'Mike' and is less than 4 floors
 
CQL
```
(owner_name LIKE 'mike%' OR owner_name like 'Mike%') AND floors<4
```

CQL JSON
```json
[
  "and",
  [
    "or",
    [
      "like",
      ["property", "owner_name"],
      "mike%"
    ],
    [
      "like",
      ["property", "owner_name"],
      "Mike%"
    ]
  ],
  [
    "lt",
    ["property", "floors"],
    4
  ]
]
```

12. Built before 2015

CQL
```json
built BEFORE '2015-01-01'
```

CQL JSON
```json
[
  "before",
  ["property", "built"],
  "2015-01-01"
]
```

13. Built after June 5, 2012

CQL
```
built AFTER '2012-06-05'
```

CQL JSON
```json
[
  "after",
  ["property", "built"],
  "2012-06-05"
]
```

14. Updated between 7:30am June 10, 2017 and 10:30am June 11, 2017

CQL
```
updated DURING '2017-06-10T07:30:00' '2017-06-11T10:30:00'
```

CQL JSON
```json
[
  "during",
  ["property", "updated"],
  "2017-06-10T07:30:00",
  "2017-06-11T10:30:00"
]
```

15. Location in the box between -118,33.8 and -117.9,34 in lat/long (geometry 1)

CQL
```
WITHIN(location,ENVELOPE(-118,33.8,-117.9,34)
```

CQL JSON
```json
[
  "within",
  ["property", "location"],
  ["bbox", 33.8, -118, 34, -117.9]
]
```

16. Geometry that intersects with geometry 2 (below)

CQL
```
INTERSECTS(geometry,POLYGON((-10.0 -10.0,10.0 -10.0,10.0 10.0,-10.0 -10.0)))
```

CQL JSON
```json
[
  "intersects",
  ["property", "location"],
  {
    "type": "Polygon",
    "coordinates": [[[-10.0, -10.0], [10.0, -10.0], [10.0, 10.0], [-10.0, -10.0]]]
  }
]
```

17. More than 5 floors and is within geometry 1 (below)

CQL
```
floors>5 AND WITHIN(geometry,ENVELOPE(33.8,-118,34,-117.9))
```

CQL JSON
```json
[
  "and",
  [
    "gt",
    ["property", "floors"],
    5
  ],
  [
    "within",
    ["property", "geometry"],
    ["bbox", 33.8, -118, 34, -117.9]
  ]
]
```