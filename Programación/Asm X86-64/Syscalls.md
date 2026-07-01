# Syscalls x86-64 Linux (Reference)

Esta nota contiene la convención de registros y las llamadas al sistema más utilizadas para desarrollo en Assembly x86-64 en Linux.

#  [[Registros]]

---

## Tabla de Syscalls Útiles


| %rax   | Nombre       | rdi (arg1)      | rsi (arg2) | rdx (arg3) | Descripción                 |
| :----- | :----------- | :-------------- | :--------- | :--------- | :-------------------------- |
| **0**  | `sys_read`   | `fd` (0=stdin)  | `*buf`     | `count`    | Lee datos del buffer.       |
| **1**  | `sys_write`  | `fd` (1=stdout) | `*buf`     | `count`    | Escribe datos en el buffer. |
| **2**  | `sys_open`   | `*filename`     | `flags`    | `mode`     | Abre un archivo.            |
| **3**  | `sys_close`  | `fd`            | -          | -          | Cierra el archivo.          |
| **9**  | `sys_mmap`   | `addr`          | `len`      | `prot`     | Mapea memoria.              |
| **12** | `sys_brk`    | `brk`           | -          | -          | Cambia el límite del heap.  |
| **57** | `sys_fork`   | -               | -          | -          | Crea proceso hijo.          |
| **59** | `sys_execve` | `*filename`     | `argv[]`   | `envp[]`   | Ejecuta un programa.        |
| **60** | `sys_exit`   | `error_code`    | -          | -          | Termina el programa.        |

---

## 🛠️ Snippets Rápidos (Sintaxis Intel)

### Escribir en Pantalla
```assembly
mov rax, 1        # sys_write
mov rdi, 1        # stdout
lea rsi, [buffer] # dirección del mensaje
mov rdx, 14       # longitud
syscall
```
### Leer texto de stdin
```assembly
mov rax, 0 # sys_read
mov rdi, 0 # stdin
lea rsi, [input_buffer] # buffer donde se almacena el mensaje
mov rdx, 256 # longitud máxima input
syscall
```
### Terminar proceso
```assembly
mov rax, 60 # sys_exit
mov rdi, rdi # codigo de salida 0 (normal)
syscall 
``` 
