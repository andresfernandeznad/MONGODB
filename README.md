# MONGODB

## 1. Crear una base de datos

```console
MongoDB Enterprise > use administracion
switched to db administracion
```

## 2. Tener una colección

```console
MongoDB Enterprise > db.createCollection('clientes')
{ "ok" : 1 }
```

## 3. Insertar, modificar y borrar documentos en la colección
### 3.1 Insertar

```console
MongoDB Enterprise > db.clientes.insert({nombre: "Juan", profesion: "carpintero", edad: 50})
WriteResult({ "nInserted" : 1 })
```

### 3.2 Modificar

```console
MongoDB Enterprise > p = db.clientes.findOne({nombre: "Juan"})
{
        "_id" : ObjectId("5afb1046674d855a33e52eda"),
        "nombre" : "Juan",
        "profesion" : "carpintero"
        edad: 50
}
MongoDB Enterprise > p.edad = 30
30
MongoDB Enterprise > db.clientes.update({nombre: "Juan"}, p)
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
MongoDB Enterprise > db.clientes.find({nombre: "Juan"})
{ "_id" : ObjectId("5afb1046674d855a33e52eda"), "nombre" : "Juan", "profesion" : "carpintero, "edad" : 30 }

```

### 3.3 Eliminar

```console
MongoDB Enterprise > db.clientes.remove({nombre: "Juan"})
WriteResult({ "nRemoved" : 1 })
```

## 4. Crear un índice sobre un campo de la colección

```console
MongoDB Enterprise > db.clientes.createIndex({nombre: 1})
{
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```

## 5. Realizar consultas en las que utilices mayor que, igual que, menor que.

### 5.1 Encontrar a los clientes con mas de 18 años

```console
MongoDB Enterprise > db.clientes.find({ "edad": {$gt: 18} })
{ "_id" : ObjectId("5afb14be674d855a33e52edc"), "nombre" : "Alejandro", "profesion" : "carpintero", "edad" : 50 }
```

### 5.2 Encontrar a los clientes con menos de 30 años

```console
MongoDB Enterprise > db.clientes.find({ "edad": {$lt: 30}})
{ "_id" : ObjectId("5afb151c674d855a33e52edd"), "nombre" : "Andrés", "profesion" : "Programador", "edad" : 20 }
```

### 5.3 Encontrar a los clientes con 20 años

```console
MongoDB Enterprise > db.clientes.find({ "edad": 20})
{ "_id" : ObjectId("5afb151c674d855a33e52edd"), "nombre" : "Andrés", "profesion" : "Programador", "edad" : 20 }
```

## 6. Realizar una consulta en la que los documentos se muestren ordenados y se limite el número de mostrados

Encuentra a los  4 clientes más mayores y ordénalos.
```console
MongoDB Enterprise > db.clientes.find().sort( {edad: -1} ).limit(4)
{ "_id" : ObjectId("5afb14be674d855a33e52edc"), "nombre" : "Alejandro", "profesion" : "carpintero", "edad" : 50 }
{ "_id" : ObjectId("5afb1641674d855a33e52edf"), "nombre" : "Cliente2", "profesion" : "Programador", "edad" : 33 }
{ "_id" : ObjectId("5afb163a674d855a33e52ede"), "nombre" : "Cliente1", "profesion" : "Programador", "edad" : 23 }
{ "_id" : ObjectId("5afb151c674d855a33e52edd"), "nombre" : "Andrés", "profesion" : "Programador", "edad" : 20 }
```

## 7. Realizar una consulta con agrupamiento y una función para mostrar la media, o suma lo que tu decidas.

Muestra la media de edad para los clientes dependiendo de su profesión.
```console
MongoDB Enterprise > db.clientes.aggregate([{$group: {_id: "$profesion" , "Media de edad": {$avg: "$edad"}}}])
{ "_id" : "Programador", "Media de edad" : 25.333333333333332 }
{ "_id" : "carpintero", "Media de edad" : 50 }
```
