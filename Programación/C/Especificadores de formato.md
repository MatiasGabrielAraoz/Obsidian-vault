| Especificador | Tipo de dato |
| ------------- | ------------ |
| `%d` or `%i`  | `int`        |
| `%f` or `%F`  | `float`      |
| `%lf`         | `double`     |
| `%c`          | `char`       |
| `%s`          | `string`     |
# *IMPORTANTE: EXPLICACIÓN DE NIKI:*
* No hablar de cosas que hagan dudar de sus conocimientos hasta fortalecer el vínculo
* Ser gracioso y comprensivo (DIFICIL)
* No mucho más


| Tipo de dato | Tamaño      |     |
| ------------ | ----------- | --- |
| `int`        | 2 o 4 bytes |     |
| `float`      | 4 bytes     |     |
| `double`     | 8 bytes     |     |
| `char`       | 1 byte      |     |

para obtener el tamaño en bytes de una variable o tipo de dato se usa el operador **sizeof**

```
printf("%zu\n", sizeof(myInt));  
printf("%zu\n", sizeof(myFloat));  
printf("%zu\n", sizeof(myDouble));  
printf("%zu\n", sizeof(myChar));
```

se usa %zu para que el compilador espere el operador sizeof q devuelva un valor size_t

otros tipos de datos

unsigned significa que solo almacena valores no negativos (de 0 para arriba)
