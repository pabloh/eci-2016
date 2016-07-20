# Laboratorios 2 & 3

## 3.1

### 1

```
SELECT *
WHERE { ?s ?r ?o }
```

### 2

```
SELECT *
WHERE { ?s foaf:name ?o }
```

### 3

```
SELECT ?o
WHERE { ?s foaf:name ?o }
```

### 4

```
SELECT *
WHERE { <https://raw.githubusercontent.com/pabloh/eci-2016/master/perfil.ttl#yo> foaf:name ?o }
```

### 5

```
SELECT ?s
WHERE { ?s foaf:firstName "José" }
```

### 6

```
SELECT ?n
WHERE {
  ?p a              foaf:Person ;
     foaf:firstName ?n ;
     foaf:age       ?a .
}
ORDER BY DESC(?a)
```

### 7

```
SELECT ?n
WHERE {
  ?p rdf:type       foaf:Person ;
     foaf:firstName ?n ;
     foaf:age       ?a .
}
ORDER BY DESC(?a)
LIMIT 1
OFFSET 4
```

### 8

```
SELECT ?n
WHERE {
  ?p a              foaf:Person ;
     foaf:firstName ?n ;
     foaf:age       ?a1 .
  FILTER(?a1 <= ?a2) .
  {
    SELECT ?a2
    WHERE { <https://raw.githubusercontent.com/pabloh/eci-2016/master/perfil.ttl#yo> foaf:age ?a2 }
  }
}
```

### 9

```
SELECT ?a, ?n
WHERE {
  <https://raw.githubusercontent.com/pabloh/eci-2016/master/perfil.ttl#yo> foaf:knows ?a .
  OPTIONAL { ?a foaf:name ?n }
}
```

### 10

```
SELECT DISTINCT ?p1, ?p2
WHERE {
  ?p1 a foaf:Person .
  ?p2 a foaf:Person .
  FILTER(?p1 != ?p2) .
  {
    ?p1 foaf:interest ?i . ?p2 foaf:interest ?i .
  }
  UNION
  {
    ?p1 foaf:likesMovie ?m . ?p2 foaf:likesMovie ?m .
  } .
}
```

## 3.2

### 13

```
SELECT (COUNT(?p) as ?countp)
WHERE { ?p a foaf:Person . }
```

### 16

```
SELECT AVG(?ni) as ?avg
WHERE {
  ?p a foaf:Person.
  {
    SELECT (COUNT(?i) as ?ni)
    WHERE { ?p foaf:interest ?i }
    GROUP BY (?p)
  }
}
```

## 4
