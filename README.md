# Complexhibit Repository 🎨

Welcome to the Complexhibit SPARQL endpoint repository! This repository hosts the codebase for the SPARQL endpoint website, where you can query the Complexhibit database.
## Accessing SPARQL Endpoint 🌐

You can access the SPARQL endpoint for querying our database by visiting [Complexhibit SPARQL Endpoint](https://complexhibit.es/sparql).

### Sample Queries 📝

Here are some sample SPARQL queries you can use to explore the database:

#### Stored Galleries 🖼️

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX exo: <https://w3id.org/OntoExhibit/>
PREFIX cidoc: <https://cidoc-crm.org/cidoc-crm/7.1.1/>

SELECT ?gname
WHERE {
  ?g rdf:type exo:Gallery.
  ?g exo:name ?gname
}
```
#### Galleries Exhibiting Artists Born After 1980 🎨👶
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX exo: <https://w3id.org/OntoExhibit/>
PREFIX cidoc: <https://cidoc-crm.org/cidoc-crm/7.1.1/>

SELECT ?gname ?pname ?year
WHERE {
  ?ex rdf:type exo:Exhibition.
  ?ex rdfs:label ?title.
  ?ex exo:hasExhibitionMaking ?exm.
  ?exm exo:hadActivityOrganizer ?org.
  ?org exo:isTheRoleOf ?g.
  ?g rdf:type exo:Gallery.
  ?g exo:name ?gname.
  
  ?exm exo:hadExhibitor ?exhibitor.
  ?exhibitor exo:isTheRoleOf ?person.
  
  ?person rdf:type cidoc:E21_Person.
  ?person exo:wasBorn ?bird.
  ?bird exo:tookPlaceIn ?date.
  ?date rdfs:label ?year.
  ?person exo:name ?pname
  
  FILTER (?year >= '1980')
}
```
#### Women Artists with a Constant Presence in the Exhibition Ecosystem 👩‍🎨💪
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX exo: <https://w3id.org/OntoExhibit/>
PREFIX cidoc: <https://cidoc-crm.org/cidoc-crm/7.1.1/>

SELECT ?pname ?title
WHERE {
  ?ex rdf:type exo:Exhibition.
  ?ex rdfs:label ?title.
  ?ex exo:hasExhibitionMaking ?exm.
  ?exm exo:hadExhibitor ?exhibitor.
  ?exhibitor exo:isTheRoleOf ?person.

  ?person rdf:type cidoc:E21_Person.
  ?person exo:gender 'Femenino'.
  ?person exo:name ?pname
} 
ORDER BY (?pname)

```

## Contact 📧

Feel free to contact us:

- Nuria Rodríguez Ortega 
  - email: <nro@uma.es>
  
- María del Mar Roldán García  
  - email: <mrgarcia@uma.es>  
  - GitHub: [mmroldan](https://github.com/mmroldan)
  
- Martín Jerónimo Salvachúa  
  - email: <martinjs@uma.es>  
  - GitHub: [MartinM10](https://github.com/MartinM10)
  
- María Luisa Díez Platas  
  - email: <marialuisa.diez@unir.net>
