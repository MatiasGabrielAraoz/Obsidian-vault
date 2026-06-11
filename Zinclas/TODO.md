


# 2026/06/09
## Trabajar en rama **beta-1-sprint-06-back-01-apiclients**

_Para poder hacer esto necesitan ejecutar el endpoint de setup, pasandole el código “rotarsa“ para que les defina toda la db creándoles todas las tablas mágicas y labels que van a necesitar para esto_
5
### Los métodos _deben estar comentados sobre como debe utilizarse (puede ser arriba del método), para que luego puedan ser consumidos correctamente desde el front._

#### _Los IDs deben ser **hardcodeados**, recuerden que estos metodos ya no son genericos, sino que son dedicados al cliente y seran consumidos por el front, el cual NO debe enterarse de que la db es generica. Pueden obtener todos los IDs ejecutando los siguientes endpoints:_

![[Pasted image 20260611190923.png]]

Implementar los métodos necesarios para administrar la relación entre Moldes y Partes.

La relación se almacena en la Tabla Mágica "Receta de Moldes" mediante los siguientes campos:

- ParteId
    
- MoldeId
    
- MoldeProduce
    

Donde:

- ParteId = Parte producida.
    
- MoldeId = Molde que produce la parte.
    
- MoldeProduce = Cantidad de piezas producidas por ese molde en cada ciclo.
    

## Métodos requeridos

### Crear relación Parte-Molde

Implementar un método que permita registrar de forma sencilla la relación entre una parte y un molde.

Ejemplo:
```C#
CreatePartMoldRelation(  
int moldeId,  
int parteId,  
int cantidadProduccion  
);
```
### Obtener las partes que produce un molde

Implementar un método que reciba un moldeId y devuelva la parte/s asociadas junto con la cantidad producida. (incluir todos los atributos de parte, img abajo)

Ejemplo:
```C#
GetPartsByMold(int moldeId);

Resultado esperado (crear DTO en ZinclasPrisma.RotarSA):

[  
{  
"partId": 25,  
"partName": "Techo",  
"partDescription": "asd",  
"partCategory": "asd",  
"partTypePiece": "asd",  
"partWeight": "asd",  
"partActive": "asd",  
"quantityProduced": 4  
}  
]
```
### Obtener el molde que produce una parte

Implementar un método que reciba un parteId y devuelva el molde/s asociado junto con la cantidad producida. (incluir todos los atributos de molde, img abajo)

Ejemplo:
```C#
GetMoldByPart(int parteId);

Resultado esperado (crear DTO en ZinclasPrisma.RotarSA):  
[

{  
"moldId": 10,  
"moldName": "Molde Casa Grande",  
"moldDescription": "Techo Verde",  
"moldState": "asd",  
"moldUbicationRow": "asd",  
"moldUbicationPosition": "asd",  
"moldAssignedMachine": "asd",  
"moldObservations": "asd",  
"quantityProduced": 4  
}

]
```
Estos métodos serán utilizados:

### Vista de Moldes

Permitir mostrar:

- Qué parte produce el molde.
    
- Cuántas unidades produce.
    

### Vista de Partes

Permitir mostrar:

- Qué molde produce la parte.
    
- Cuántas unidades produce dicho molde.
    

**Importante**: Para que no se haga por ejemplo en el caso de cada molde que se muestre en el front una llamada a la funcion para obtener que partes produce, necesito que implementen un metodo que devuelva todas las relaciones parte molde existentes.

Ej: GetAllPartMoldRelations();

y que devuelva algo asi (crear DTO en ZinclasPrisma.RotarSA):
```Json
[  
{  
"moldId": 10,  
"moldName": "Molde Casa Grande",  
"moldDescription": "Techo Verde",  
"partId": 25,  
"partName": "Techo",  
"partDescription": "Techo Verde",  
"quantityProduced": 4  
}  
]
```
Los métodos específicos son para mostrar detalles.

El método masivo para los listados.

Esta es la informacion que vas a necesitar:

![[Pasted image 20260611190942.png]]

![[Pasted image 20260611190950.png]]
