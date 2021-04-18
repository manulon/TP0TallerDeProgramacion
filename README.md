# TP0TallerDeProgramacion
# Alumno: Manuel Longo Elia
# Padrón: 102425
## Paso 0: Entorno de trabajo
### Documentar:
**a. Capturas de pantalla de la ejecución del aplicativo (con y sin Valgrind)**
_Sin valgrind:_ \n
./tp \n
Hola mundo

_Con valgrind:_ \n
valgrind ./tp
```
==13807== Memcheck, a memory error detector
==13807== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==13807== Using Valgrind-3.13.0 and LibVEX; rerun with -h for copyright info
==13807== Command: ./tp
==13807== 
Hola mundo
==13807== 
==13807== HEAP SUMMARY:
==13807==     in use at exit: 0 bytes in 0 blocks
==13807==   total heap usage: 1 allocs, 1 frees, 1,024 bytes allocated
==13807== 
==13807== All heap blocks were freed -- no leaks are possible
==13807== 
==13807== For counts of detected and suppressed errors, rerun with: -v
==13807== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

b.
Valgrind es una herramienta que ayuda al programador a controlar la memoria utilizada en su codigo. Lo ayuda, por ejemplo, a ver si su programa pierde memoria.
Actualmente, siempre he utilizado valgrind corriendolo de la siguiente forma valgrind ```./ejecutable```, se que hay mas formas de utilizar la herramienta, de hecho. Si en una terminal se escribe ``` valgrind --help ``` se muestran todas las opciones posibles para la ejecucion de la herramienta.

c.
La funcion ```sizeof()``` sirve para saber cuantos bytes ocupa una variable o una estructura de datos de un tipo de dato determinado.
El valor de salida de sizeof(char) seria 1 byte, y de sizeof(int) seria 4 bytes.

d.
La respuesta es no. Ya que en las estructuras hay padding, es decir que se establece un espacio de "relleno" para que el size del struct sea multiplo de 4.
Adjunto ejemplo:
En el caso del ejemplo, se ve que las variables a, c y d ocupan 4 bytes cada una, y la variable b, por otro lado, ocupa 1 solo byte. Entonces la memoria quedaria asi:
    00   01    02    03 
00[  A |  A  |  A  |  A  ]
04[  B |  /  |  /  |  /  ]
08[  C |  C  |  C  |  C  ]
12[  D |  D  |  D  |  D  ]
( / representa el espacio de relleno del padding ).

e.
STDIN se la conoce como la entrada estandar, su descriptor asociado es el 0. Por lo general estos datos son ingresados mediante el teclado. Por otra parte, STDOUT representa la salida estandar, es el canal por el cual el programa devuelve los datos. Generalmente estos datos se muestran en el monitor y su descriptor asociado es el 1. Finalmente, STDERR representa el error estandar, es la via por la cual se envia un mensaje de error una vez que haya un fallo en la ejecucion. Es representado por el numero 2.
Se puede redireccionar la salida estándar usando en la terminal el caracter >. Si queremos que la salida se agregue al contenido pre-existente y no se reemplace cada vez, se debe usar el símbolo dos veces: >>. Para redireccionar la entrada estándar se usa el caracter <.
El pipe ( | ) le dice a la terminal que se quiere usar la salida del comando a la izquierda como entrada al comando de la derecha.
