# 2026-04-21
Implementar en el proyecto **ZinclasPrisma.ApiClient** los métodos necesarios para consumir los endpoints de autenticación de usuarios.
- [x] Crear AuthApiClient ✅ 2026-04-24
- [x] Usar el metodo **LoginAsync(username, pass)** ✅ 2026-04-25
El método LoginAsync es usado en el cliente.
- [x] Manejar el token JWT recibido ✅ 2026-04-25
- [x] Configurar el envío del token en futuras requests ✅ 2026-04-25
Trabajar en rama **beta1-sprint-01-back-01-auth**

# 2026-04-26
Ya que vamos a tener que hacer un ApiClient para Rotar S.A. y otro para la escuela, lo mejor va a ser definir una interfaz, digamos “ApiClientBase”, y despues hacer “ApiClientRotar” y “ApiClientSchool” para implementar los metodos especificos.

- [x] Renombrar ApiClient a ApiClientBase ✅ 2026-04-28
- [x] Mantener en ApiClientBase solo metodos que sean utiles para ambos (ej: inicio de sesión de usuarios) ✅ 2026-04-28
- [x] Crear los otros dos y hacer que hereden de base. ✅ 2026-04-29
(Implementar metodos especificos para cada uno es otra tarea)  

Trabajar en rama: **beta-1-sprint-02-back-01-endpoints**

# 2026-05-12
Implementar en el SuperadminApiClient los metodos para post y get de las etiquetas PersonLabel, DataLabel y OrderLabel por separado
### Implementar los métodos para post y get de PersonLabel
- [x] post
- [x] get
### Implementar los métodos para post y get de DataLabel
- [x] post
- [x] get
### Implementar los métodos para post y get de OrderLabel
- [x] post
- [x] get

Trabajar en rama: **Beta-1-sprint-03-back-01-endpoints**


# 2026/05/20
Crear un endpoint para crear varios registros a la vez
### URL de endpoint: /api/Generic/create-multiple
## manejar: separate = true
iterar diccionario de DataLabels
##  manejar: separate = false
Crear un solo order y un solo datum y que los generic registries apunten a esa dirección
Para eso tengo que crear el servicio CreateMultipleRegisters que devuelva IActionResult (Ok() & Errors)


## Parametros a ingresar:
- [x] El id del person
- [x] El label de order
- [x] El valor para el order
- [x] Un booleano “separate“
- [x] Un diccionario que la key se inteprete como el DataLabel en el cual guardar y los values como los valores que guardar en las etiquetas correspondientes


Que reciba:

- Una lista con dtos para los data.
- Un dto para el order.
- el separate
- id del person

Todos los registros genericos creados con esta función tienen que tener una instancia independiente de order si separate es true, como si todos hubieran sido creados uno por uno con el endpoint normal de creación, si separate es falso todos los registros genericos creados esta vez deberan indicar a un mismo order.