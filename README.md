
 __Alumno:__ *Jorge Camañez*
 
 __Profesor:__ *Pedro Nieto*

# Ejercicio 2: Nifi+ELK
```
Usando nifi+ELK, debéis presentar una solución que muestre, sobre un mapa, 
la disposición de delitos presentes en esta API:
https://data.cityofnewyork.us/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9
```

#### 1. Creamos una archivo docker con contenedores de Nifi, ElasticSearch y Kibana en los siguientes puertos:

```
    docker-compose up -d
```
	
	| Component | Port |
	| --- | --- | 
	| Kibana | 5601 |
	| Elasticsearch | 9200 |
	| Nifi | 8080 |
	

#### 2. Diseñamos el flowfile en Nifi con los tres conectores siguientes, con el fin de introducir conectar la API con ELK:

  - InvokeHttp: Ingestar los datos vía Api.
  - SplitJSON: Dividir el JSON que ingestamos de la API en diferentes archivos.
  - PutElasticSearchHttp: Enviamos los datos a Elasticsearch con el índice "crime". 

  <img src="images/Flow_nifi.png" size=300px>

#### 3. Desde las tools de Kibana creamos un nuevo índice a partir del que hemos creado con Nifi del tipo geo_point

 <img src="images/ReIndex.png" size=300px>


#### 4. Visualizamos el mapa de incidencias a partir de nuevo índice creado

 <img src="images/Kibana_map.png" size=300px>

#### 5. Creamos un dashborad con el mapa anterior y más gráficos.

Se pueden visualizar las incidencias por ciudad y estado, o los motivos de las incidencias por ejemplo. 

 <img src="images/crime_dashboard.png" size=500px>
