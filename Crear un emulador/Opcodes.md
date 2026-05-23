Como la memoria de CHIP-8 es un array de uint8_t (8 bits), entonces, para obtener un opcode completo tenes que leer la posición actual del PC y siguiente y unirlas.

# Como está formado un Opcode:

Un opcode de 16 bits se divide en 4 partes de 4 bits llamadas **nibbles**. Normalmente el primer nibble indica el tipo de operación y los otros 3 son datos
### Variables: 

X: Segundo nibble = usa uno de los registros V0 .. VF (primer digito del opcode)

Y: Tercer nibble = tambien usa uno de los registros V0 .. VF (segundo digito del opcode)

N: Cuarto nibble = un numero de 4 bits que sirve como argumento específico dentro de las instrucciones de 2 bytes, indica un valor pequeño como la altura de un sprite en la instrucción de dibujo DXYN, o parametros específicos de subrutinas. (ultimo digito)

NN / KK: El segundo byte completo = un numero de 8 bits que se usa para cargar datos directos, hacer comparaciones o establecer los valores de registros Vx. Actúa como un operando inmediato, no como NNN que indica una dirección en memoria (ultimos 2 digitos hexadecimales)

NNN: Representa una dirección en memoria de 12 bits = utilizada en los operandos de las instrucciones para indicar un destino directo. Sirve para saltar a subrutinas ( 2NNN ), Saltar a una dirección ( 1NNN ), o establecer el registro del indice I ( ANNN ).

### Tabla de Opcodes CHIP-8

| Opcode   | Tipo   | Descripción                                                                                 |
| :------- | :----- | :------------------------------------------------------------------------------------------ |
| **0nnn** | SYS    | Salta a una rutina de lenguaje de máquina en `nnn`. (Ignorado en la mayoría de emuladores). |
| **00E0** | CLS    | Limpia la pantalla.                                                                         |
| **00EE** | RET    | Regresa de una subrutina.                                                                   |
| **1nnn** | JP     | Salto incondicional: `PC = nnn`.                                                            |
| **2nnn** | CALL   | Llama a subrutina: guarda PC en el stack, `PC = nnn`.                                       |
| **3xkk** | SE     | Salta si igual: `if (Vx == kk) PC += 2`.                                                    |
| **4xkk** | SNE    | Salta si no igual: `if (Vx != kk) PC += 2`.                                                 |
| **5xy0** | SE     | Salta si registros iguales: `if (Vx == Vy) PC += 2`.                                        |
| **6xkk** | LD     | Carga constante: `Vx = kk`.                                                                 |
| **7xkk** | ADD    | Suma sin acarreo: `Vx = Vx + kk`.                                                           |
| **8xy0** | LD     | Asignación: `Vx = Vy`.                                                                      |
| **8xy1** | OR     | Bitwise OR: `Vx = Vx \| Vy`.                                                                |
| **8xy2** | AND    | Bitwise AND: `Vx = Vx & Vy`.                                                                |
| **8xy3** | XOR    | Bitwise XOR: `Vx = Vx ^ Vy`.                                                                |
| **8xy4** | ADD    | Suma con acarreo: `Vx = Vx + Vy`, `Vf = 1` si hay overflow.                                 |
| **8xy5** | SUB    | Resta: `Vx = Vx - Vy`, `Vf = 0` si hay borrow.                                              |
| **8xy6** | SHR    | Desplazamiento derecha: `Vf = LSB`, `Vx = Vx >> 1`.                                         |
| **8xy7** | SUBN   | Resta invertida: `Vx = Vy - Vx`, `Vf = 0` si hay borrow.                                    |
| **8xyE** | SHL    | Desplazamiento izquierda: `Vf = MSB`, `Vx = Vx << 1`.                                       |
| **9xy0** | SNE    | Salta si registros diferentes: `if (Vx != Vy) PC += 2`.                                     |
| **Annn** | LD I   | Carga índice: `I = nnn`.                                                                    |
| **Bnnn** | JP V0  | Salto relativo: `PC = nnn + V0`.                                                            |
| **Cxkk** | RND    | Aleatorio: `Vx = random() & kk`.                                                            |
| **Dxyn** | DRW    | Dibuja sprite de `n` bytes en `(Vx, Vy)`. `Vf = 1` si hay colisión.                         |
| **Ex9E** | SKP    | Salta si tecla presionada: `if (key[Vx] == down) PC += 2`.                                  |
| **ExA1** | SKNP   | Salta si tecla NO presionada: `if (key[Vx] == up) PC += 2`.                                 |
| **Fx07** | LDDT   | Carga delay timer: `Vx = delay_timer`.                                                      |
| **Fx0A** | WK     | Espera tecla: detiene ejecución hasta presionar tecla, guarda en `Vx`.                      |
| **Fx15** | SETT   | Setea delay timer: `delay_timer = Vx`.                                                      |
| **Fx18** | SETST  | Setea sound timer: `sound_timer = Vx`.                                                      |
| **Fx1E** | ADD I  | Suma a índice: `I = I + Vx`.                                                                |
| **Fx29** | LD F   | Carga fuente: `I = ubicación_caracter_hex(Vx)`.                                             |
| **Fx33** | LD B   | BCD: guarda centenas, decenas y unidades de `Vx` en `I`, `I+1`, `I+2`.                      |
| **Fx55** | LD [I] | Dump registros: guarda `V0` a `Vx` en memoria desde `I`.                                    |
| **Fx65** | LD V   | Load registros: carga `V0` a `Vx` desde memoria desde `I`.                                  |