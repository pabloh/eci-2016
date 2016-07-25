# Tarea

### 1
```sparql
# Tuples of Popes born on the 15th century with their children (if they had)
SELECT ?pope ?son ?birth_year
WHERE
{
  ?pope wdt:P39 wd:Q19546 ;
        wdt:P569 ?birth .
  BIND (YEAR(?birth) AS ?birth_year) .
  OPTIONAL { ?son wdt:P22 ?pope } .
  FILTER(1400 < ?birth_year && ?birth_year <= 1500)
}
ORDER BY(?birth_year)
```

### 2

```sparql
# Popes from Poland and Germany
SELECT ?pope
WHERE
{
  ?pope wdt:P39 wd:Q19546 .
  { ?pope wdt:P27 wd:Q36 }
  UNION
  { ?pope wdt:P27 wd:Q183 }
}
```

### 3

```sparql
# Popes from the last 2 centuries by country
SELECT ?country (COUNT(?country) AS ?ccountry)
WHERE
{
  ?pope wdt:P39 wd:Q19546 ;
        wdt:P569 ?birth .
  BIND (YEAR(?birth) AS ?birth_year).
  FILTER(1800 < ?birth_year) .
  ?pope wdt:P27 ?country .
}
GROUP BY (?country)
ORDER BY DESC(?ccountry)
```

### 4

```sparql
# Descendants of Popes who were also Popes
SELECT ?descendant
WHERE
{
  ?pope wdt:P39 wd:Q19546.
  ?pope (wdt:P40)+ ?descendant .
  ?descendant wdt:P39 wd:Q19546 .
}
```
