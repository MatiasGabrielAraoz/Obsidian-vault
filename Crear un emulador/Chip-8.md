recursos informativos:
#### [Cowgod's Chip-8 Technical Reference](http://devernay.free.fr/hacks/chip8/C8TECH10.HTM)
#### Estudiar **Máscaras de bits**
# Memoria: **4096 bytes (4KB)**
#### de 0x000 a 0x1FF: se reserva para el interprete
#### de 0x050 a 0x0A0: fuentes de los caracteres (los dibujos del 0 al F)
### 0x200 a 0xFFF: se carga el juego (rom), el program counter inicia en 0x200
# Registros:
### de V0 a VF: son 16 registros de 8 bits. Se usan para hacer operaciones
#### VF es una "flag", si la suma supera 255, VF se pone en 1 funcionando como carry
### I (Index Register): 16 bits. se usa para apuntar a direcciones en memoria donde se almacenan los dibujos o datos
### PC (program counter): 16 bits. Guarda la dirección de la siguiente instrucción q se está ejecutando (empieza en 0x200) 
#### el program counter se actualiza después de cada fetch
### SP (Stack Pointer): 8 bits.  apunta a la cima del Stack
# Stack:
### Cuando se llama a una función/subrutina, el procesador tiene q recordar donde volver después. el Stack es un array de 16 valores de 16 bits que guarda las direcciones de retorno, entre otras cosas
# [[Opcodes]] (words) : 
### Cada instrucción en CHIP-8 mide 2 bytes. Cuando el emulador lee la memoria combina 2 bytes para formar un opcode.
# TODO: 
- [ ] implementar teclado
- [ ] implementar ultimos opcodes
- [ ] gestionar graficos
- [ ] hacer pruebas de los opcodes 


