# Registros x86-64 (AMD64)

## Registros de Propósito General (16 × 64 bits)

| Registro (64 bits) | Apodo / Significado       | Uso principal                                                               | ¿es volatil?   |
| :----------------- | :------------------------ | :-------------------------------------------------------------------------- | :------------- |
| **`rax`**          | **A**ccumulator           | Resultado de funciones/operaciones. Operaciones aritméticas (`add`, `mul`). | Volátil        |
| **`rbx`**          | **B**ase                  | Propósito general. Registro base.                                           | **No volátil** |
| **`rcx`**          | **C**ounter               | Contador en bucles (`loop`). 4° argumento en funciones.                     | Volátil        |
| **`rdx`**          | **D**ata                  | Extensión de `rax` para datos grandes (resto de división). 3er argumento.   | Volátil        |
| **`rbp`**          | **B**ase **P**ointer      | Puntero base del marco de pila (stack frame).                               | **No volátil** |
| **`rsp`**          | **S**tack **P**ointer     | Puntero a la **cima de la pila**.                                           | **No volátil** |
| **`rsi`**          | **S**ource **I**ndex      | Fuente para copiar datos (cadenas). 2do argumento.                          | Volátil        |
| **`rdi`**          | **D**estination **I**ndex | Destino para copiar datos. **1er argumento** en funciones.                  | Volátil        |
| **`r8`**           | Registro 8                | Propósito general. 5to argumento.                                           | Volátil        |
| **`r9`**           | Registro 9                | Propósito general. 6to argumento.                                           | Volátil        |
| **`r10`**          | Registro 10               | Propósito general / temporal.                                               | Volátil        |
| **`r11`**          | Registro 11               | Propósito general / temporal.                                               | Volátil        |
| **`r12`**          | Registro 12               | Propósito general.                                                          | **No volátil** |
| **`r13`**          | Registro 13               | Propósito general.                                                          | **No volátil** |
| **`r14`**          | Registro 14               | Propósito general.                                                          | **No volátil** |
| **`r15`**          | Registro 15               | Propósito general.                                                          | **No volátil** |

## Registros Especiales

| Registro           | Nombre              | Función                                                              |
| :----------------- | :------------------ | :------------------------------------------------------------------- |
| **`rip`**          | Instruction Pointer | Apunta a la **próxima instrucción** a ejecutar.                      |
| **`rflags`**       | Flags               | Registro de **estado**. Cada bit indica condición (ZF, SF, CF, etc.) |
| **`xmm0`-`xmm15`** | SIMD                | Registros de 128 bits para operaciones de punto flotante y SIMD.     |

## Acceso a porciones de registros

Un registro de 64 bits se puede dividir en partes más pequeñas:

| Tamaño            | Ejemplo en `rax` | Ejemplo en `r8` |
| :---------------- | :--------------- | :-------------- |
| **64 bits**       | `rax`            | `r8`            |
| **32 bits**       | `eax`            | `r8d`           |
| **16 bits**       | `ax`             | `r8w`           |
| **8 bits (low)**  | `al`             | `r8b`           |
| **8 bits (high)** | `ah`             | (no existe)     |

> **Nota**: Escribir en `eax` pone a cero los 32 bits superiores de `rax`. Escribir en `al` o `ah` solo modifica esa parte, el resto del registro se conserva.

## Convención de llamadas (Sys V AMD64 ABI)

### Parámetros de función (en orden):
1. `rdi`
2. `rsi`
3. `rdx`
4. `rcx`
5. `r8`
6. `r9`
→ El resto van a la pila.

### Valor de retorno:
- Enteros/punteros: `rax`
- Punto flotante: `xmm0`

### Registros volátiles (caller-saved):
`rax`, `rdi`, `rsi`, `rdx`, `rcx`, `r8`-`r11`  
→ Pueden ser modificados por la función llamada.

### Registros no volátiles (callee-saved):
`rbx`, `rbp`, `rsp`, `r12`-`r15`  


### Registros de punteros
- **RIP (Instruction Pointer):** Qué instrucción se está ejecutando.
    
- **RSP (Stack Pointer):** Dónde está el tope de la pila (volátil).
    
- **RBP (Base Pointer):** Referencia fija para acceder a variables locales y parámetros sin importar cuánto se mueva `RSP`.
# [[Syscalls]] en Linux (usando `syscall`)

| Registro  | Uso               |
| :-------- | :---------------- |
| **`rax`** | Número de syscall |
| **`rdi`** | 1er argumento     |
| **`rsi`** | 2do argumento     |
| **`rdx`** | 3er argumento     |
| **`r10`** | 4to argumento     |
| **`r8`**  | 5to argumento     |
| **`r9`**  | 6to argumento     |

> **Resultado**: Se devuelve en `rax`. Si es negativo, es código de error.

## Fuentes
- AMD64 Architecture Programmer's Manual
- System V AMD64 ABI
- Linux syscall conventions
- NASM documentation