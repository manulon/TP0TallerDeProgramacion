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


**b. Captura de pantalla indicando los errores de generación del ejecutable. Explicar cada uno e
indicar si se trata de errores del compilador o del linker.**
