# es un comando para buscar patrones de texto dentro de uno o varios archivos o la salida de otros comandos (usando [[Pipes]]) e imprimiendo en stdout las lineas que cumplen con el filtro

## grep {OPTION}... -f PATTERN_FILE ... {FILE} ...

### si no se especifica un archivo se hace una busqueda recursiva que busca en el directorio de trabajo, las busquedas no recursivas leen el stdin 
## -e (--regexp=PATTERNS)
### define el patrón a buscar

## -f (--file=FILE)
### obtiene patrones del archivo, uno por linea. si el archivo esta vacío o nada coincide con el patrón no se muestra nada

## -d (--directories=ACTION)
### si la entrada es un directorio usa ACTION para procesarlo. por defecto lee los directorios como si fueran archivos normales si ACTION es "skip" se saltea el directorio, si es "recurse" lee todos los archivos adentro del directorio, funcionando igual que la opción -r 

## -r (--recurive)
### lee todos los archivos en cada directorio de forma recursiva, seguido de los vinculos simbólicos solo si no están en la linea de comandos, si no se especifica un archivo grep busca en el directorio en el q estás. esto es equivalente a -d "recurse"

## -v (--invert-match)
### invierte el sentido y selecciona todas las lineas excluyendo las q cumplan con el patrón

## -c (--count)
### suprime la salida normal y escribe la cantidad de lineas q coinciden.

## -m (--max-count=NUMBER)
### deja de leer el archivo despues de X cantidad de coincidencias.