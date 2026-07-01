Los comodines son patrones de busqueda para seleccionar palabras, frases o secuencias de letras. Estos obviamente pueden ser añadidos en varios comandos usando [[Pipes]]

# " * ":
## Este comodín selecciona todos los archivos si está solo, pero tambien se puede usar "(asterisco).txt" para seleccionar todos los archivos q terminen en .txt o usar "archivoX(asterisco)" para seleccionar todos los archivos q empiecen por "archivoX" 

# " ? ":
## Este comodín representa un solo caracter por lo q si ejecutas "ls /dev/sda?" lista todos los archivos q sean iguales a /dev/sda + un caracter.

# " [] ":
## este comodín representa un rango de caracteres o numeros, por ejemplo podemos hacer "ls /dev/sda[1,5]" para mostrar /dev/sda1,/dev/sda2...

# " {} ":
## este comodín representa un conjunto de comodines separados por comas, por ejemplo "ls {sda*,sdb*}". solo funciona si después de la coma no pones un espacio.

# "[!]":
## este comodín es lo contrario a [] ya que lista todo lo q no esté en el rango, por ejemplo "ls /dev/sda[!1,5]" va a mostrar todo excepto los q estén entre 1 y 5

