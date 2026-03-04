# compilar kernel.c
```i686-elf-gcc -c kernel.c -o kernel.o -std=gnu99 -ffreestanding -O2 -Wall -Wextra```

# compilar boot.s
```i686-elf-as boot.s -o boot.o ```

# Linkear Kernel con Boot
 ```i686-elf-gcc -T linker.ld -o CustomOS -ffreestanding -O2 -nostdlib boot.o kernel.o -lgcc ```

necesita [[Cross-compiler]] y tener descargadas las [[Development tools]]