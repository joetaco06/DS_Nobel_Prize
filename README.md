# DS Nobel Prize JSON format

### Descargar MongoDB Compass aquí:

https://www.mongodb.com/try/download/compass


-------

# EJEMPLO PRÁCTICO:

## ¿Cuántos españoles han ganado el premio nobel?

Código:

db.laureate.find({ bornCountryCode: "ES" }).count();

## ¿Cuántas mujeres han ganado el premio nobel?

Código: 

db.laureate.find({ gender: "female" }).count();

## ¿Cuántos hombres españoles han sido premio nobel?

Código: 

db.laureate.find({ gender: "male", bornCountry: "Spain" }).count();

## ¿Cuántos laureados se llaman María o Jose?

Código: 

db.laureate.find({ $or: { firstname: { $regex: "Maria", $options: "i" } },
    { firstname: { $regex: "Jose", $options: "i" } } ]}).count();


## ¿Cuántas laureados han utilizado “develop” investigación? 

Código: 

db.laureate.find({ "prizes.motivation": { $regex: "develop", $options: "i" } }).count();


## ¿Cuántas laureados hay por país? 

Código:

db.laureate.aggregate([ {   $group: { _id: "$bornCountry",
count: { $sum: 1 } }  }, {  $sort: { count: -1 }  }]);
