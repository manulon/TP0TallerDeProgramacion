# TP0TallerDeProgramacion
# Alumno: Manuel Longo Elia
# Padrón: 102425
## Paso 0: Entorno de trabajo
### Documentar:
**a. Capturas de pantalla de la ejecución del aplicativo (con y sin Valgrind)**

![Imagen](https://https://github.com/manulon/imagenesParaTP0/a1.png)

b.
Valgrind es una herramienta que ayuda al programador a controlar la memoria utilizada en su codigo. Lo ayuda, por ejemplo, a ver si su programa pierde memoria.
Actualmente, siempre he utilizado valgrind corriendolo de la siguiente forma valgrind ./<<CURSIVA>>ejecutable, se que hay mas formas de utilizar la herramienta, de hecho. Si en una terminal se escribe <<cursiva>> valgrind --help <<cursiva>> se muestran todas las opciones posibles para la ejecucion de la herramienta.

c.
La funcion sizeof() sirve para saber cuantos bytes ocupa una variable o una estructura de datos de un tipo de dato determinado.
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
