# Arquitectura TOY-8

Nombre y apellido: Leonardo Gutierrez

## Instrucciones

- Forkear este repo
- Completar nombre y apellido
- Responder editando este mismo archivo
- Pushear a GitHub y pasarme el link de su fork (el repo tiene que ser público)


Tienen un emulador de la computadora y el circuito para el Logisim en el [blog](https://la35.net/orga/emulador.html). Usenlos sabiamente para responder.

**Tip:** si editan en el Atom tienen un _preview_ de Markdown tocando `Ctrl + Shift + M` mientras editan este archivo.
## Ejercicios

1. Considerar el siguiente programa de TOY-8 en lenguaje máquina. Traducir a hexadecimal en la tercer columna y a ensamblador en la cuarta como se muestra en la primera línea. ¿Cuál es el valor de 0xE cuando el programa se detiene? ¿Qué es lo que hace este programa si 0xE es el resultado del mismo?

```
0x1:  10101011    #  AB  #  lw B
0x2:  11101010    #  EA  #  bze A
0x3:  00101101    #  2D  #  add D
0x4:  11001011    #  CB  #  sw B
0x5:  10101110    #  AE  #  lw E 
0x6:  00101100    #  2C  #  add C
0x7:  11001110    #  CE  #  sw E
0x8:  10100000    #  A0  #  lw 0
0x9:  11100001    #  E1  #  bze 1 
0xA:  00000000    #  00  #  halt
0xB:  00000011    #  03  #  dato
0xC:  00000110    #  06  #  dato
0xD:  11111111    #  FF  #  dato
0xE:  00000000    #  00  #  halt              El valor del programa
```

2. Consideren el siguiente _hexdump_ de la memoria de TOY-8. O sea un volcado de la memoria en hexadecimal. ¿Cuántos programas distintos pueden encontrar? Indicar cuáles bytes interpretan como instrucciones y cuáles como datos.

```
0x0   00 A5 26 C7
0x4   00 08 05 00
0x8   A7 6D 2E C7
0xc   00 FF 01 00
```

```  
Hay 2 programas distintos

0x0   00000000(instruccion)  10100101(instruccion)  00100110(instruccion)  11000111(instruccion)
0x4   00000000(instruccion)  00001000(dato)         00000101(dato)  00000000(instruccion) 
0x8   10100111(instruccion)  01101101(instruccion)  00101110(instruccion)  11000111(instruccion)
0xc   00000000(instruccion)  11111111(instruccion)  00000001(dato)  00000000(instruccion)
```
3. Para el primer programa del ejercicio anterior. ¿Qué líneas de control se activan para cada instrucción? ¿Cuál es el valor del bus de datos y de instrucciones en cada instrucción? Completen la siguiente tabla, agreguen las filas que sean necesarias.

|Instrucción|Reloj|Control       |Data bus|Address Bus|
|-----------|-----|--------------|--------|-----------|
|A5         |0    |IR en         |A5      |1          |
|A5         |1    |R en, addr mux|08      |5          |
|26         |0    |              |        |           |

4. El siguiente programa suma los números que encuentra en la entrada hasta que aparece un cero, y luego envía el resultado a la salida. Traducirlo a ensamblador y a C siguiendo el ejemplo de las primeras dos líneas.

```
0x1:  A0  #  lw 0  #  
0x2:  CE  #  sw E  #  int sum = 0;
0x3:  AF  #  lw F  #  tag1:
0x4:  E9  #  bze 9 #  if (sum == 0) { goto tag2 }
0x5:  2E  #  add E #  sum += 14;
0x6:  CE  #  sw E  #  int E = sum;
0x7:  A0  #  lw 0  #  sum = 0;
0x8:  E3  #  bze 3 #  if (sum == 0) { goto tag1 } 
0x9:  AE  #  lw 0  #  tag2: sum = 0
0xA:  CF  #  sw F  #  int F = sum;
0xB:  00  #  halt  #  return 0;
```

5. Una mejora que le podríamos hacer a esta computadora es duplicar la cantidad de memoria, pasar de 16 bytes a 32 bytes. ¿Cómo lo harían manteniendo la longitud de las instrucciones en 8 bits? ¿Qué partes de la CPU habría que modificar y cómo?
