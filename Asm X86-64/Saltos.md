# Tabla de Saltos (Jumps) x86-64

Las instrucciones de salto condicional (`Jcc`) se basan en el estado de los bits del registro `RFLAGS` después de ejecutar `CMP` o `TEST`.

## 1. Comparaciones con Signo (Signed)
*Se usan para números enteros que pueden ser negativos (ej: -5, 10).*

| Instrucción | Mnemotecnia              | Condición Lógica | Estado de Flags       |
| :---------- | :----------------------- | :--------------- | :-------------------- |
| **`JE`**    | Jump if Equal            | $A = B$          | `ZF = 1`              |
| **`JNE`**   | Jump if Not Equal        | $A \neq B$       | `ZF = 0`              |
| **`JG`**    | Jump if Greater          | $A > B$          | `ZF = 0` y `SF = OF`  |
| **`JGE`**   | Jump if Greater or Equal | $A \geq B$       | `SF = OF`             |
| **`JL`**    | Jump if Less             | $A < B$          | `SF != OF`            |
| **`JLE`**   | Jump if Less or Equal    | $A \leq B$       | `ZF = 1` o `SF != OF` |

---

## 2. Comparaciones sin Signo (Unsigned)
*Ideales para direcciones de memoria, ASCII y contadores positivos.*

| Instrucción | Mnemotecnia            | Condición Lógica | Estado de Flags     |
| :---------- | :--------------------- | :--------------- | :------------------ |
| **`JA`**    | Jump if Above          | $A > B$          | `CF = 0` y `ZF = 0` |
| **`JAE`**   | Jump if Above or Equal | $A \geq B$       | `CF = 0`            |
| **`JB`**    | Jump if Below          | $A < B$          | `CF = 1`            |
| **`JBE`**   | Jump if Below or Equal | $A \leq B$       | `CF = 1` o `ZF = 1` |

---

## 3. Saltos por Banderas Específicas
*Útiles para control de desbordamientos o chequeos rápidos después de un `TEST`.*

| Instrucción | Descripción                       | Flag     |
| :---------- | :-------------------------------- | :------- |
| **`JZ`**    | Jump if Zero (Igual a `JE`)       | `ZF = 1` |
| **`JNZ`**   | Jump if Not Zero (Igual a `JNE`)  | `ZF = 0` |
| **`JS`**    | Jump if Sign (Resultado negativo) |          |
[[Registros]]
[[Syscalls]]