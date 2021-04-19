# TP0TallerDeProgramacion
# Alumno: Manuel Longo Elia
# Padrón: 102425
## Paso 0: Entorno de trabajo
### Documentar:
**a. Capturas de pantalla de la ejecución del aplicativo (con y sin Valgrind)**

_Sin valgrind:_ 
```
./tp
```
```
Hola mundo
```

_Con valgrind:_
```
valgrind ./tp
```

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

**b. ¿Para qué sirve Valgrind? ¿Cuáles son sus opciones más comunes?**

Valgrind es una herramienta que ayuda al programador a controlar la memoria utilizada en su codigo. Lo ayuda, por ejemplo, a ver si su programa pierde memoria.
Actualmente, siempre he utilizado valgrind corriendolo de la siguiente forma ```valgrind ./ejecutable```, se que hay mas formas de utilizar la herramienta, de hecho. Si en una terminal se escribe ``` valgrind --help ``` se muestran todas las opciones posibles para la ejecucion de la herramienta.

**c. ¿Qué representa sizeof()? ¿Cuál sería el valor de salida de sizeof(char) y sizeof(int)?**

La funcion ```sizeof()``` sirve para saber cuantos bytes ocupa una variable o una estructura de datos de un tipo de dato determinado.

El valor de salida de sizeof(char) seria 1 byte, y de sizeof(int) seria 4 bytes.

**d.¿El sizeof() de una struct de C es igual a la suma del sizeof() de cada uno sus elementos?
Justifique mediante un ejemplo.**

La respuesta es no. Ya que en las estructuras hay padding, es decir que se establece un espacio de "relleno" para que el size del struct sea multiplo de 4.

_Codigo:_
```
#include <stdio.h>

struct ejemplo{
    int a;
    char b;
    float c;
    int d;
};

int main(int argc, char* argv[]){
    struct ejemplo e;
    printf("Los bytes que ocupan el primer elemento del struct es: %ld \n", sizeof(e.a));
    printf("Los bytes que ocupan el segundo elemento del struct es: %ld \n", sizeof(e.b));
    printf("Los bytes que ocupan el tercer elemento del struct es: %ld \n", sizeof(e.c));
    printf("Los bytes que ocupan el cuarto elemento del struct es: %ld \n", sizeof(e.d));
    printf("----------------------------------------------------------------------- \n");
    printf("La suma de todo es: %ld \n", ( sizeof(e.a) + sizeof(e.b) + sizeof(e.c) + sizeof(e.d) ));
    printf("Y el size total del struct es: %ld \n", sizeof(e));
    return 0;
}
```
_Salida:_
```
Los bytes que ocupan el primer elemento del struct es: 4 
Los bytes que ocupan el segundo elemento del struct es: 1 
Los bytes que ocupan el tercer elemento del struct es: 4 
Los bytes que ocupan el cuarto elemento del struct es: 4 
----------------------------------------------------------------------- 
La suma de todo es: 13 
Y el size total del struct es: 16 
```

En el caso del ejemplo, se ve que las variables a, c y d ocupan 4 bytes cada una, y la variable b, por otro lado, ocupa 1 solo byte. Entonces la memoria quedaria asi:
```
    00   01    02    03 
    
00[  A |  A  |  A  |  A  ]

04[  B |  /  |  /  |  /  ]

08[  C |  C  |  C  |  C  ]

12[  D |  D  |  D  |  D  ]
```

( / representa el espacio de relleno del padding ).


**e.Investigar la existencia de los archivos estándar: STDIN, STDOUT, STDERR. Explicar
brevemente su uso y cómo redirigirlos en caso de ser necesario (caracteres > y <) y como
conectar la salida estándar de un proceso a la entrada estándar de otro con un pipe (carácter
| ).**

STDIN se la conoce como la entrada estandar, su descriptor asociado es el 0. Por lo general estos datos son ingresados mediante el teclado. Por otra parte, STDOUT representa la salida estandar, es el canal por el cual el programa devuelve los datos. Generalmente estos datos se muestran en el monitor y su descriptor asociado es el 1. Finalmente, STDERR representa el error estandar, es la via por la cual se envia un mensaje de error una vez que haya un fallo en la ejecucion. Es representado por el numero 2.

Se puede redireccionar la salida estándar usando en la terminal el caracter >. Si queremos que la salida se agregue al contenido pre-existente y no se reemplace cada vez, se debe usar el símbolo dos veces: >>. Para redireccionar la entrada estándar se usa el caracter <.

El pipe ( | ) le dice a la terminal que se quiere usar la salida del comando a la izquierda como entrada al comando de la derecha.


## Paso 1: SERCOM - Errores de generación y normas de programación
### Documentar:
**a. Captura de pantalla mostrando los problemas de estilo detectados. Explicar cada uno.**

Lo que voy a hacer es primero copiar todos los errores de estilo detectados y luego explicarlos cada uno particularmente.

```
/task/student//source_unsafe/paso1_wordscounter.c:27:  Missing space before ( in while(  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:41:  Mismatching spaces inside () in if  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:41:  Should have zero or one spaces inside ( and ) in if  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:47:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]
/task/student//source_unsafe/paso1_wordscounter.c:47:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]
/task/student//source_unsafe/paso1_wordscounter.c:48:  Missing space before ( in if(  [whitespace/parens] [5]
/task/student//source_unsafe/paso1_wordscounter.c:53:  Extra space before last semicolon. If this should be an empty statement, use {} instead.  [whitespace/semicolon] [5]
/task/student//source_unsafe/paso1_main.c:12:  Almost always, snprintf is better than strcpy  [runtime/printf] [4]
/task/student//source_unsafe/paso1_main.c:15:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]
/task/student//source_unsafe/paso1_main.c:15:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]
/task/student//source_unsafe/paso1_wordscounter.h:5:  Lines should be <= 80 characters long  [whitespace/line_length] [2]
Done processing /task/student//source_unsafe/paso1_wordscounter.c
Done processing /task/student//source_unsafe/paso1_main.c
Done processing /task/student//source_unsafe/paso1_wordscounter.h
Total errors found: 11
```
Ahora procedere a explicarlos uno a uno.

1-

```
/task/student//source_unsafe/paso1_wordscounter.c:27:  Missing space before ( in while(  [whitespace/parens] [5]
```
Lo que marca aqui es que se deberia poner un espacio entre la palabra while y la condición para hacer el código más legible. Se debería pasar de: ```while(state != STATE_FINISHED);``` a ```while (state != STATE_FINISHED);```.

2-

```
/task/student//source_unsafe/paso1_wordscounter.c:41:  Mismatching spaces inside () in if  [whitespace/parens] [5]
```
Aqui se indica que hay un mal uso de los espacios en el parentesis del if, Se debería pasar de: ```if (  c == EOF);``` a ```if (c == EOF);```.

3-

```
/task/student//source_unsafe/paso1_wordscounter.c:41:  Should have zero or one spaces inside ( and ) in if  [whitespace/parens] [5]
```
En este caso dice que puede escribirse así ```if (c == EOF)``` o ```if ( c == EOF )``` para que quede prolijo.

4-

```
/task/student//source_unsafe/paso1_wordscounter.c:47:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]
```
Aqui se indica que el condicional deberia escribirse asi:
```
if (c == EOF) {
        next_state = STATE_FINISHED;
    } else if (state == STATE_WAITING_WORD) {
        if (strchr(delim_words, c) == NULL)
            next_state = STATE_IN_WORD;
    } else if (state == STATE_IN_WORD) {
        if(strchr(delim_words, c) != NULL) {
            self->words++;
            next_state = STATE_WAITING_WORD;
        }
    }
```

5-

```
/task/student//source_unsafe/paso1_wordscounter.c:47:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]
```
Es muy similar al anterior, si el if tiene una llave del lado derecho, deberia tenerlo tambien en su lado izquierdo.

6-

```
/task/student//source_unsafe/paso1_wordscounter.c:48:  Missing space before ( in if(  [whitespace/parens] [5]
```
Aqui lo mismo que se menciono arriba, en vez de  ```if(strchr(delim_words, c) != NULL)``` deberia ser ```if (strchr(delim_words, c) != NULL)```

7-

```
/task/student//source_unsafe/paso1_wordscounter.c:53:  Extra space before last semicolon. If this should be an empty statement, use {} instead.  [whitespace/semicolon] [5]
```
Aqui, se corrige el espacio antes del ; del return, dice que deberia ser ```return next_state;```

8-

```
/task/student//source_unsafe/paso1_main.c:12:  Almost always, snprintf is better than strcpy  [runtime/printf] [4]
```
Claramente se ve que aqui recomienda hacer uso de la funcion ```snprintf``` antes que ```strcpy```, igualmente entiendo que esto es a criterio del programador la eleccion de la funcion a utilizar

9-

```
/task/student//source_unsafe/paso1_main.c:15:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]
```
Similar a un error que aparecio antes, dice que antes del else debe precederlo un {

10-

```
/task/student//source_unsafe/paso1_main.c:15:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]
```
Como se menciono anteriormente, las llaves deben estar en ambos lados del else.

11-

```
/task/student//source_unsafe/paso1_wordscounter.h:5:  Lines should be <= 80 characters long  [whitespace/line_length] [2]
```
Claramente dice que la linea es muy larga, que deben tener menos de 80 caracteres. Lo que podria hacerse para solucionar esto es dejar el comentario en dos lineas separadas.

**b. Captura de pantalla indicando los errores de generación del ejecutable. Explicar cada uno e
indicar si se trata de errores del compilador o del linker.**

Los errores que aparecen son: 

```
Compilando el codigo...
cc -Wall -Werror -pedantic -pedantic-errors -O3 -ggdb -DDEBUG -fno-inline -D _POSIX_C_SOURCE=200809L -Dwrapsocks=1 -std=c11 -o paso1_main.o -c paso1_main.c
paso1_main.c: In function 'main':
paso1_main.c:22:9: error: unknown type name 'wordscounter_t'
   22 |         wordscounter_t counter;
      |         ^~~~~~~~~~~~~~
paso1_main.c:23:9: error: implicit declaration of function 'wordscounter_create' [-Wimplicit-function-declaration]
   23 |         wordscounter_create(&counter);
      |         ^~~~~~~~~~~~~~~~~~~
paso1_main.c:24:9: error: implicit declaration of function 'wordscounter_process' [-Wimplicit-function-declaration]
   24 |         wordscounter_process(&counter, input);
      |         ^~~~~~~~~~~~~~~~~~~~
paso1_main.c:25:24: error: implicit declaration of function 'wordscounter_get_words' [-Wimplicit-function-declaration]
   25 |         size_t words = wordscounter_get_words(&counter);
      |                        ^~~~~~~~~~~~~~~~~~~~~~
paso1_main.c:27:9: error: implicit declaration of function 'wordscounter_destroy' [-Wimplicit-function-declaration]
   27 |         wordscounter_destroy(&counter);
      |         ^~~~~~~~~~~~~~~~~~~~
make: *** [/task/student/MakefileTP0:144: paso1_main.o] Error 1

real    0m0.018s
user    0m0.010s
sys     0m0.007s
[Error] Fallo la compilacion del codigo en 'source_unsafe.zip'. Codigo de error 2
```

Todos los errores se deben a los mismo, en el ```paso1_main.c``` no se esta incluyendo ```paso1_wordscounter.h``` lo cual hace que las funciones no esten definidas, ya que se encuentran definidas en ese archivo. La manera de solucionarlo es en el main poner la siguiente linea ```#include <paso1_wordscounter.h>```.


**c. ¿El sistema reportó algún WARNING? ¿Por qué?**

No, el sistema no reporto ningun warning. La linea que marca el warning deberia tener ```warning``` luego de que se marque el archivo y la linea donde ocurrio el problema. En este caso lo que mostro son todos errores, marcados por la palabra ```error```. 

La diferencia entre estos es que si hay un error no es posible la compilacion de los modulos y el programa no podra ejecutarse, sin embargo con un warning el programa puede ser ejecutado, pero no siempre de manera correcta. El warning es mas que nada una advertencia para que el programador.


## Paso 2: SERCOM - Errores de generación 2
### Documentar:
**a. Describa en breves palabras las correcciones realizadas respecto de la versión anterior.**

Basicamente lo que se hizo fue reemplazar 'strcpy' por 'memcpy'. Tambien corrigio todos los errores de estilo que se menciono anteriormente que estaban mal, generando asi que no se marquen errores de ese tipo.

**b. Captura de pantalla indicando la correcta ejecución de verificación de normas de
programación.**

```
Done processing /task/student//source_unsafe/paso2_wordscounter.h
Done processing /task/student//source_unsafe/paso2_main.c
Done processing /task/student//source_unsafe/paso2_wordscounter.c
```

**c. Captura de pantalla indicando los errores de generación del ejecutable. Explicar cada uno e
indicar si se trata de errores del compilador o del linker.**

```
Compilando el codigo...
cc -Wall -Werror -pedantic -pedantic-errors -O3 -ggdb -DDEBUG -fno-inline -D _POSIX_C_SOURCE=200809L -Dwrapsocks=1 -std=c11 -o paso2_wordscounter.o -c paso2_wordscounter.c
In file included from paso2_wordscounter.c:1:
paso2_wordscounter.h:7:5: error: unknown type name 'size_t'
    7 |     size_t words;
      |     ^~~~~~
paso2_wordscounter.h:20:1: error: unknown type name 'size_t'
   20 | size_t wordscounter_get_words(wordscounter_t *self);
      | ^~~~~~
paso2_wordscounter.h:1:1: note: 'size_t' is defined in header '<stddef.h>'; did you forget to '#include <stddef.h>'?
  +++ |+#include <stddef.h>
    1 | #ifndef __WORDSCOUNTER_H__
paso2_wordscounter.h:25:49: error: unknown type name 'FILE'
   25 | void wordscounter_process(wordscounter_t *self, FILE *text_file);
      |                                                 ^~~~
paso2_wordscounter.h:1:1: note: 'FILE' is defined in header '<stdio.h>'; did you forget to '#include <stdio.h>'?
  +++ |+#include <stdio.h>
    1 | #ifndef __WORDSCOUNTER_H__
paso2_wordscounter.c:17:8: error: conflicting types for 'wordscounter_get_words'
   17 | size_t wordscounter_get_words(wordscounter_t *self) {
      |        ^~~~~~~~~~~~~~~~~~~~~~
In file included from paso2_wordscounter.c:1:
paso2_wordscounter.h:20:8: note: previous declaration of 'wordscounter_get_words' was here
   20 | size_t wordscounter_get_words(wordscounter_t *self);
      |        ^~~~~~~~~~~~~~~~~~~~~~
paso2_wordscounter.c: In function 'wordscounter_next_state':
paso2_wordscounter.c:30:25: error: implicit declaration of function 'malloc' [-Wimplicit-function-declaration]
   30 |     char* delim_words = malloc(7 * sizeof(char));
      |                         ^~~~~~
paso2_wordscounter.c:30:25: error: incompatible implicit declaration of built-in function 'malloc' [-Werror]
paso2_wordscounter.c:5:1: note: include '<stdlib.h>' or provide a declaration of 'malloc'
    4 | #include <stdbool.h>
  +++ |+#include <stdlib.h>
    5 |
cc1: all warnings being treated as errors
make: *** [/task/student/MakefileTP0:144: paso2_wordscounter.o] Error 1

real    0m0.021s
user    0m0.006s
sys     0m0.013s
[Error] Fallo la compilacion del codigo en 'source_unsafe.zip'. Codigo de error 2
```

En este caso no voy a hacer como hice antes, de explicar uno a uno. Ya que esta vez todos los errores se basan en lo mismo. La falta de includes, en casi todos los archivos faltan las librerias que incluyen las funciones o tipo de datos que estan faltantes en estos casos. Todos los errores son de compilacion.

## Paso 3: SERCOM - Errores de generación 3
### Documentar:
**a. Describa en breves palabras las correcciones realizadas respecto de la versión anterior.**

Los cambios que se realizaron fueron muy similares todos, se incluyeron librerias que antes no estaban incluidos en los pasos anteriores.

**Captura de pantalla indicando los errores de generación del ejecutable. Explicar cada uno e
indicar si se trata de errores del compilador o del linker.**

Los errores que aparecen son:

```
Compilando el codigo...
cc -Wall -Werror -pedantic -pedantic-errors -O3 -ggdb -DDEBUG -fno-inline -D _POSIX_C_SOURCE=200809L -Dwrapsocks=1 -std=c11 -o paso3_wordscounter.o -c paso3_wordscounter.c
cc -Wall -Werror -pedantic -pedantic-errors -O3 -ggdb -DDEBUG -fno-inline -D _POSIX_C_SOURCE=200809L -Dwrapsocks=1 -std=c11 -o paso3_main.o -c paso3_main.c
cc paso3_wordscounter.o paso3_main.o -o tp -lm -Wl,--wrap=send -Wl,--wrap=recv
/usr/bin/ld: paso3_main.o: in function `main':
/task/student/source_unsafe/paso3_main.c:27: undefined reference to `wordscounter_destroy'
collect2: error: ld returned 1 exit status
make: *** [/task/student/MakefileTP0:135: tp] Error 1

real    0m0.113s
user    0m0.079s
sys     0m0.025s
[Error] Fallo la compilacion del codigo en 'source_unsafe.zip'. Codigo de error 2
```

El unico error que aparece es que no se encuentra el metodo ```wordscounter_destroy``` el cual se encuentra definido en el ```paso3_wordscounter.h``` pero no implementado en el .c de esta libreria. Esto se puede definir como un error de linkeo.


## Paso 4: SERCOM - Memory Leaks y Buffer Overflows
### Documentar:
**a. Describa en breves palabras las correcciones realizadas respecto de la versión anterior.**

Al igual que en el paso anterior, se incluyeron algunos archivos que antes no estaban incluidos y se agrego la funcion ```paso3_wordscounter.h``` que fue la que genero el error antes.

**b. Captura de pantalla del resultado de ejecución con Valgrind de la prueba ‘TDA’. Describir los
errores reportados por Valgrind.**

```
==00:00:00:00.000 60== Memcheck, a memory error detector
==00:00:00:00.000 60== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==00:00:00:00.000 60== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==00:00:00:00.000 60== Command: ./tp input_tda.txt
==00:00:00:00.000 60== Parent PID: 59
==00:00:00:00.000 60==
==00:00:00:00.584 60==
==00:00:00:00.584 60== FILE DESCRIPTORS: 5 open at exit.
==00:00:00:00.584 60== Open file descriptor 4: input_tda.txt
==00:00:00:00.584 60==    at 0x495FEAB: open (open64.c:48)
==00:00:00:00.584 60==    by 0x48E2195: _IO_file_open (fileops.c:189)
==00:00:00:00.584 60==    by 0x48E2459: _IO_file_fopen@@GLIBC_2.2.5 (fileops.c:281)
==00:00:00:00.584 60==    by 0x48D4B0D: __fopen_internal (iofopen.c:75)
==00:00:00:00.584 60==    by 0x48D4B0D: fopen@@GLIBC_2.2.5 (iofopen.c:86)
==00:00:00:00.584 60==    by 0x109177: main (paso4_main.c:14)
==00:00:00:00.584 60==
==00:00:00:00.584 60== Open file descriptor 3: /task/student/cases/tda/__valgrind__
==00:00:00:00.584 60==    <inherited from parent>
==00:00:00:00.584 60==
==00:00:00:00.584 60== Open file descriptor 2: /task/student/cases/tda/__stderr__
==00:00:00:00.584 60==    <inherited from parent>
==00:00:00:00.584 60==
==00:00:00:00.584 60== Open file descriptor 1: /task/student/cases/tda/__stdout__
==00:00:00:00.584 60==    <inherited from parent>
==00:00:00:00.584 60==
==00:00:00:00.584 60== Open file descriptor 0: /task/student/cases/tda/__stdin__
==00:00:00:00.584 60==    <inherited from parent>
==00:00:00:00.584 60==
==00:00:00:00.584 60==
==00:00:00:00.584 60== HEAP SUMMARY:
==00:00:00:00.584 60==     in use at exit: 1,977 bytes in 216 blocks
==00:00:00:00.584 60==   total heap usage: 218 allocs, 2 frees, 10,169 bytes allocated
==00:00:00:00.584 60==
==00:00:00:00.585 60== 472 bytes in 1 blocks are still reachable in loss record 1 of 2
==00:00:00:00.585 60==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==00:00:00:00.585 60==    by 0x48D4AAD: __fopen_internal (iofopen.c:65)
==00:00:00:00.585 60==    by 0x48D4AAD: fopen@@GLIBC_2.2.5 (iofopen.c:86)
==00:00:00:00.585 60==    by 0x109177: main (paso4_main.c:14)
==00:00:00:00.585 60==
==00:00:00:00.585 60== 1,505 bytes in 215 blocks are definitely lost in loss record 2 of 2
==00:00:00:00.585 60==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==00:00:00:00.585 60==    by 0x109301: wordscounter_next_state (paso4_wordscounter.c:35)
==00:00:00:00.585 60==    by 0x1093B5: wordscounter_process (paso4_wordscounter.c:30)
==00:00:00:00.585 60==    by 0x109197: main (paso4_main.c:24)
==00:00:00:00.585 60==
==00:00:00:00.585 60== LEAK SUMMARY:
==00:00:00:00.585 60==    definitely lost: 1,505 bytes in 215 blocks
==00:00:00:00.585 60==    indirectly lost: 0 bytes in 0 blocks
==00:00:00:00.585 60==      possibly lost: 0 bytes in 0 blocks
==00:00:00:00.585 60==    still reachable: 472 bytes in 1 blocks
==00:00:00:00.585 60==         suppressed: 0 bytes in 0 blocks
==00:00:00:00.585 60==
==00:00:00:00.585 60== For lists of detected and suppressed errors, rerun with: -s
==00:00:00:00.585 60== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```

Valgrind reporto que se esta perdiendo memoria, ya que esta no se esta liberando adecuadamente luego de su uso.

**c. Captura de pantalla del resultado de ejecución con Valgrind de la prueba ‘Long Filename’.
Describir los errores reportados por Valgrind**

```
**00:00:00:00.532 48** *** memcpy_chk: buffer overflow detected ***: program terminated
==00:00:00:00.000 48== Memcheck, a memory error detector
==00:00:00:00.000 48== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==00:00:00:00.000 48== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==00:00:00:00.000 48== Command: ./tp input_extremely_long_filename.txt
==00:00:00:00.000 48== Parent PID: 47
==00:00:00:00.000 48==
**00:00:00:00.532 48** *** memcpy_chk: buffer overflow detected ***: program terminated
==00:00:00:00.532 48==    at 0x483E9CC: ??? (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==00:00:00:00.532 48==    by 0x4843C0A: __memcpy_chk (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==00:00:00:00.532 48==    by 0x109168: memcpy (string_fortified.h:34)
==00:00:00:00.532 48==    by 0x109168: main (paso4_main.c:13)
==00:00:00:00.544 48==
==00:00:00:00.544 48== FILE DESCRIPTORS: 4 open at exit.
==00:00:00:00.544 48== Open file descriptor 3: /task/student/cases/nombre_largo/__valgrind__
==00:00:00:00.544 48==    <inherited from parent>
==00:00:00:00.544 48==
==00:00:00:00.544 48== Open file descriptor 2: /task/student/cases/nombre_largo/__stderr__
==00:00:00:00.544 48==    <inherited from parent>
==00:00:00:00.544 48==
==00:00:00:00.544 48== Open file descriptor 1: /task/student/cases/nombre_largo/__stdout__
==00:00:00:00.544 48==    <inherited from parent>
==00:00:00:00.544 48==
==00:00:00:00.544 48== Open file descriptor 0: /task/student/cases/nombre_largo/__stdin__
==00:00:00:00.544 48==    <inherited from parent>
==00:00:00:00.544 48==
==00:00:00:00.544 48==
==00:00:00:00.544 48== HEAP SUMMARY:
==00:00:00:00.544 48==     in use at exit: 0 bytes in 0 blocks
==00:00:00:00.544 48==   total heap usage: 0 allocs, 0 frees, 0 bytes allocated
==00:00:00:00.544 48==
==00:00:00:00.544 48== All heap blocks were freed -- no leaks are possible
==00:00:00:00.544 48==
==00:00:00:00.544 48== For lists of detected and suppressed errors, rerun with: -s
==00:00:00:00.544 48== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

Se detecto un buffer overflow en la funcion ```memcpy_chk```. Esto significa que lo que se esta intentando guardar en el buffer supero el tamaño del mismo.

**d. ¿Podría solucionarse este error utilizando la función strncpy? ¿Qué hubiera ocurrido con la
ejecución de la prueba?**

Valgrind no reportaría ningún error porque no se perdería memoria, ya que strncpy copia hasta n caracteres por lo que no entrarian no estarian ocupando memoria. Pero, dandose el caso de que se supere el buffer la prueba daria error, ya que solo se leerian n caracteres y no los caracteres completos, lo cual diferiria de la salida esperada en la prueba.

**e. Explicar de qué se trata un segmentation fault y un buffer overflow.**

El segmentation fault sucede cuando se accede a memoria a la que no está permitido acceder o cuando se accede a memoria de una forma que no esta permitida. Por ejemplo en un vector de 4 posiciones querer ingresar a la posicion 5.
Por otro lado, el buffer overflow sucede cuando lo que se quiere guardar en el buffer es de mayor tamaño que lo que el buffer tiene reservado para guardar.

## Paso 5: SERCOM - Código de retorno y salida estándar
### Documentar:
**a. Describa en breves palabras las correcciones realizadas respecto de la versión anterior.**

Los cambios fueron tomar el nombre del archivo directo de la terminal y cerrarlo el archivo luego de su uso.
También se creó una cadena de caracteres estática para almacenar los delimitadores de palabras en lugar de pedir memoria.

**b. Describa el motivo por el que fallan las prueba ‘Invalid File’ y ‘Single Word’. ¿Qué información
entrega SERCOM para identificar el error? Realice una captura de pantalla. **

La informacion que tenemos sobre 'Invalid File' es:

```
[=>] Comparando archivo_invalido/__return_code__...
1c1
< 255
---
> 1
```
Esto quiere decir que se esta esperando un 1 y se recibe un 255. 

La informacion que tenemos sobre 'Single word' es:

```
[=>] Comparando una_palabra/__stdout__...
1c1
< 0
---
> 1
```
Esto quiere decir que se esta esperando un 1 y se recibe un 0. 

**c. Captura de pantalla de la ejecución del comando hexdump. ¿Cuál es el último carácter del
archivo input_single_word.txt?**

```
00000000  77 6f 72 64                                       |word|
00000004
```

El ultimo caracter del archivo es el numero hexadecimal 0x64 que convertido a decimal es el numero 100 que en ascii representa la letra 'd'.

**d. Captura de pantalla con el resultado de la ejecución con gdb. Explique brevemente los
comandos utilizados en gdb. ¿Por qué motivo el debugger no se detuvo en el breakpoint de la
línea 45: self->words++;?**

```
gdb ./tp
GNU gdb (Ubuntu 9.2-0ubuntu1~20.04) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from ./tp...
(gdb) info functions
All defined functions:

File paso5_main.c:
9:	int main(int, char **);

File paso5_wordscounter.c:
14:	void wordscounter_create(wordscounter_t *);
18:	void wordscounter_destroy(wordscounter_t *);
22:	size_t wordscounter_get_words(wordscounter_t *);
26:	void wordscounter_process(wordscounter_t *, FILE *);
34:	static char wordscounter_next_state(wordscounter_t *, char, char);

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001090  __cxa_finalize@plt
0x00000000000010a0  fclose@plt
0x00000000000010b0  __stack_chk_fail@plt
0x00000000000010c0  strchr@plt
0x00000000000010d0  __printf_chk@plt
0x00000000000010e0  fopen@plt
0x00000000000010f0  getc@plt
0x00000000000011b0  _start
0x00000000000011e0  deregister_tm_clones
--Type <RET> for more, q to quit, c to continue without paging--c
0x0000000000001210  register_tm_clones
0x0000000000001250  __do_global_dtors_aux
0x0000000000001290  frame_dummy
0x0000000000001380  __libc_csu_init
0x00000000000013f0  __libc_csu_fini
0x00000000000013f8  _fini
(gdb) list wordscounter_next_state
33	
34	static char wordscounter_next_state(wordscounter_t *self, char state, char c) {
35	    const char* delim_words = " ,.;:\n";
36	
37	    char next_state = state;
38	    if (c == EOF) {
39	        next_state = STATE_FINISHED;
40	    } else if (state == STATE_WAITING_WORD) {
41	        if (strchr(delim_words, c) == NULL)
42	            next_state = STATE_IN_WORD;
(gdb) list
43	    } else if (state == STATE_IN_WORD) {
44	        if (strchr(delim_words, c) != NULL) {
45	            self->words++;
46	            next_state = STATE_WAITING_WORD;
47	        }
48	    }
49	    return next_state;
50	}
51	
(gdb) break 45
Punto de interrupción 1 at 0x1300: file paso5_wordscounter.c, line 45.
(gdb) run input_single_word.txt
Starting program: /home/manulon/Escritorio/lqmp/tp input_single_word.txt
0
[Inferior 1 (process 10631) exited normally]

```

El primer comando utilizado es list functions, lo que hace este comando es listar todas las funciones involucradas en los archivos. El segundo comando, list wordscounter_next_state, lo que hace es mostrar algunas lineas de la funcion que esta seguida del 'list', luego list lo que hace es listar las siguientes n lineas. Lo que hace break 45 es marcar un 'breakpoint' que representa el punto donde el programador se quiere parar para comnenzar a debuggear. Y finalmente con run input_single_word.txt corre el archivo de texto que esta escritro a continuacion.
El debugger no se detuvo en el breakpoint porque no se entro nunca a esa parte del codigo, ya que se esta ejecutando la prueba 'una_palabra' entonces no hay delimitadores que separen palabras entonces salta al final de la sentencia.

