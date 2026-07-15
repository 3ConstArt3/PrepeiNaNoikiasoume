___

## Γενική Παρουσίαση

```dataview
TABLE WITHOUT ID
    elink(url, file.name) AS "Code",
    area AS "Area",
    square_meters AS "m²",
    bedrooms AS "Beds",
    energy_class AS "Energy",
    total AS "Total(€)"
FROM "Wellbeing/Renting/Candidates"
FLATTEN round((upfront_costs + monthly_costs) / 10) * 10 AS total
WHERE url != null
SORT file.name ASC
```

___

## Ανά Ενεργειακή Κλάση

```dataview
TABLE WITHOUT ID
    elink(url, file.name) AS "Code",
    area AS "Area",
    energy_class AS "Energy",
    total AS "Total(€)",
    average_sq AS "€/m²",
    square_meters AS "m²",
    bedrooms AS "Beds"
FROM "Wellbeing/Renting/Candidates"
FLATTEN round((upfront_costs + monthly_costs) / 10) * 10 AS total
FLATTEN round(total / square_meters, 2) AS average_sq
WHERE url != null
	AND contains(list("A", "B", "C", "U"), energy_class)
SORT 
    energy_class ASC, 
    total ASC,
    average_sq ASC,
    square_meters DESC
```

___

## Ανά Συνολικό Κόστος

```dataview
TABLE WITHOUT ID
    elink(url, file.name) AS "Code",
    area AS "Area",
    total AS "Total(€)",
    average_sq AS "€/m²",
    square_meters AS "m²",
    energy_class AS "Energy",
    bedrooms AS "Beds"
FROM "Wellbeing/Renting/Candidates"
FLATTEN round((upfront_costs + monthly_costs) / 10) * 10 AS total
FlATTEN round(total / square_meters, 2) AS average_sq
WHERE url != null
	AND contains(list("A", "B", "C", "D"), energy_class)
	AND square_meters >= 55
	AND bedrooms >= 2
SORT 
	total ASC,
	average_sq ASC,
	square_meters ASC, 
	energy_class ASC
```

___

## Ανά Τετραγωνικά Μέτρα

```dataview
TABLE WITHOUT ID
    elink(url, file.name) AS "Code",
    area AS "Area",
    square_meters AS "m²",
    total AS "Total(€)",
    average_sq AS "€/m²",
    energy_class AS "Energy",
    bedrooms AS "Beds"
FROM "Wellbeing/Renting/Candidates"
FLATTEN round((upfront_costs + monthly_costs) / 10) * 10 AS total
FlATTEN round(total / square_meters, 2) AS average_sq
WHERE url != null
	AND contains(list("A", "B", "C", "D", "U"), energy_class)
	AND square_meters >= 50
	AND bedrooms >= 2
SORT 
	square_meters DESC, 
	total DESC,
	average_sq DESC,
	energy_class DESC
```

___
