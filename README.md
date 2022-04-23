# Interbloqueo
## Que es?
Es cuando un sistema multiprogramacion se queda colgado esperando por in evento que no va a pasar.
## **Condiciones**
* **Control Exlusivo**: Estos procesos reclaman un proceso en especifico solamente para ellos.
* **Recursos Mantenidos**: Estos procesos mantienen los recursos que se le asignan pero siguen esperando adicionales que no se les otorgara.
* **Apropiacion**: Pasa por los recursos asginados no se pueden soltar hasta que se terminen de utilizar.
* **Espera Circular**: Es cuando 2 o mas elementos deben consumir recursos de su sucesor, por lo que se quedan esperando y nunca los reciben.

## **Interbloqueo entre usuarios**
Pueden poroducirse en procesos donde los procesos **propios de usuarios** nunca lleguen a su fin.
## **Consideraciones**
* Los procesos **reclaman control exclusivo de los recursos que piden**.
* Los procesos **mantienen los recursos que ya les han sido asignados** mientras esperan por recursos adicionales.
* Los **recursos no pueden ser extraídos de los procesos que los tienen** hasta su completa utilización.
* Existe una **cadena circular** de procesos en la cual **cada uno de ellos mantiene a uno o mas recursos que son requeridos por el siguiente**proceso de la cadena. **(condición de espera circular)**.


## **DEADLOCK** 
*1.* Dos procesos desean imprimir grandes archivos en cinta. 

*2.* El proceso “a” solicita la impresora, que se le concede. 

*3.* El proceso “b” solicita la unidad de cinta, que se le concede. 

*4.* El proceso “a” solicita la unidad de cinta, pero se deniega la solicitud hasta que “b” la libera. 

*5.* El proceso “b” solicita la impresora y se produce el bloqueo (deadlock). 

## **Interbloqueo de Trafico**
Similar a el trafico de autos, este puede detenerse totalmente, por lo que se necesita intervencion externa para reestablecer todo el sistema.

## **Interbloqueo de Recurso Simple**
1. Tiene su origen en la **contención normal de los recursos dedicados o reutilizables en serie**.
2. Pueden ser **utilizados por un solo usuario** a la vez. 
3. **Cada proceso está esperando por el otro** para liberar uno de los recursos. 
4. **El recurso retenido no será liberado** hasta que el otro proceso usuario libere su recurso. 
5. **Este último proceso usuario no liberará su recurso** retenido hasta que el primer proceso usuario libere su recurso retenido. 
6. Se produce una espera **circular**.

## **Interbloqueo Spool:**
Varios programas generan lineas spool, por lo que **pueden interbloquearse si el buffer se llena antes de completar las tareas.** 
### **Reduccion:**
Se pueden reducir **asignando espacio en disco mayor del necesario con asignacion dinamica**, limitando a los spoolers de entrada, para que no lean mas trabajos cuando el buffer se este saturando.
### **Sistema Spool**
Se refiere al proceso mediante el cual la computadora introduce trabajos en un buffer, de manera que un dispositivo pueda acceder a ellos cuando esté listo. Es útil en **caso de dispositivos que acceden a los datos a distintas velocidades.** El buffer proporciona **un lugar de espera donde los datos pueden estar hasta que el dispositivo (generalmente más lento) los procesa.** Esto **permite que la CPU pueda trabajar en otras tareas** mientras que espera que el dispositivo más lento acabe de procesar el trabajo.

## **Postergacion Indefinida**
### **Que es?**
Cuando los recursos son planificados en función de **prioridades**, un proceso dado puede esperar indefinidamente, **mientras sigan llegando procesos de prioridades mayores.**

### **Evitar:**
Se puede evitar al **permitir que un proceso aumente de prioridad mientras espera**, a esto se le dice envejecimiento.  

```diff
+ -------------------------------------------------------------------------------
```

# **ESTUDIO DEL INTERBLOQUEO**
Hay cuatro aspectos importantes en la investigación del interbloqueo:
* Prevención
* Evitación
* Detección
* Recuperación

## **PREVENCION del Interbloqueo**
**Condicionar un sistema para que elimine toda posibilidad** de que este se produzca.
### **NEGACIONES**
### Negación de la condición de **“Espera por”** 
* Pedir los recursos al inicio, todo o nada 
* *Problema*: desperdicio de recursos *->* Postergación Indefinida.

### Negación de la condición de **“No apropiatividad”** 
* **Soltar recursos después de una 2da petición, y pedirlos junto con los que no se tiene,** todos de una vez 
* *Problema:* Postergación Indefinida.

### Negación de la condición de **“Espera Circular”**:
* Procesos con numeración de orden de ejecución


## **EVITACION del Interbloqueo**
La meta es **imponer condiciones menos estrictas** que en la prevención, **para intentar lograr una mejor utilización de los recursos**. 

**Permite la aparición del interbloqueo**, pero siempre que aparece la posibilidad, entonces **se esquiva**.

## **DETECCION del Interbloqueo**
1. **Determinar** si ha ocurrido un interbloqueo. 
2. **Encontrar** los procesos y recursos implicados en el bloqueo. 
3. Ya teniendo esas variables detectadas, podemos **eliminarlo del sistema**. 

## **RECUPERACION del Interbloqueo**
Consiste en despejar interbloqueos de un sistema, de manera que pueda seguir operando libre de ellos, y qque **los procesos estancados lleguen a su terminación, liberando sus recursos.**
```diff
+ ---------------------------------------------------------------------------
```
## **HAVENDER**:
```
"Si falta una de las 4 condiciones necesarias no se produce el interbloqueo."
```
### **Las estrategias son:**
* **Cada proceso deberá pedir todos sus recursos** requeridos de una sola vez y no podrá proceder hasta que se le hayan sido asignados.

* **Si un proceso quiere mas recursos**, **debe liberar los que tiene** y de ser necesario, entonces puede pedir **pedir los asignados y los adicionales**
*** Se impondrá la ordenación lineal** de los tipos de recursos en todos los procesos, es decir, si a un proceso le han sido asignados recursos de un tipo dado, **solo podrá pedir aquellos recursos de los tipos que siguen en el ordenamiento.**

```diff
+ ---------------------------------------------------------------------------
```
## **Evitación o Predicción del Interbloqueo**
Una forma de resolver el problema del interbloqueo, que se diferencia sutilmente de la prevención, es la predicción del interbloqueo. 

En la **prevención de interbloqueo**, se obligaba a las solicitudes de recursos a **impedir que sucediera , por lo menos, alguna de las cuatro condiciones** de interbloqueo.

*** ------- De las 4 evitar por lo menos 1 ----- ***

Impidiendo una de las tres condiciones necesarias:
* exclusión mutua
* retención y espera
* no apropiación

O directamente, **impidiendo la aparición de un circulo viciosos de espera.** siendo ineficiente de los recursos y una ejecución ineficiente de los procesos. 
```diff
+ ---------------------------------------------------------------------------
```
## **PREDICCION DE INTERBLOQUEO**
### Requirimientos
* En esta **se pueden dar las 3 condiciones**, pero el SO toma **desiciones para asegurar que nunca se generae un interbloqueo.**
* Esta **permite mas concurrencia**.
* Se decide dinámicamente **si la petición actual** de asignación de un recurso **podría llevar potencialmente a un interbloqueo**. 
* **Necesita conocer las peticiones futuras** de recursos.

### Enfoques
* **No iniciar el proceso** si puede llevar a interbloqueo.
* **No otorgar recusos al proceso** si puede llevar a interbloqueo.
```diff
+ ---------------------------------------------------------------------------
```
## **ESTRATEGIAS DE PREVENCION VS DETECCION**
* ***Prevencion***: Resuelven **limitando acceso y restringiendo** acceso sobre procesos.
* ***Deteccion***:** Otorgaran los recursos** y el **SO (con algoritmos) detectara las condiciones** para circulos viciosos.

## **ESTRATEGIAS DE DETECCION** 
* Para determinar si hay un interbloqueo,** se verificaran los estados** de los recursos.
* **Al solicitar o devolver** recursos , se actualiza el estado y **se hace una verificación detectar ciclos**. 
* Este método **está basado** en suponer que un **interbloqueo no se presente** y que** los recursos del sistema que han sido asignados**, se liberarán en el momento que otro proceso lo requiera.
```diff
+ ---------------------------------------------------------------------------
```
## **RECUPERACION**
### MANUAL
* **Informar al operador**que ha ocurrido un interbloqueo y que este ocupe manualmente.
### SO (Automatica)
1. **Abortar uno o más procesos** hasta romper la espera circular
2. **Apropiar algunos recursos** de uno o más de los procesos bloqueados.

* Actualmente, la recuperación se realiza **eliminando un proceso y quitándole sus recursos**. 
* El proceso eliminado **se pierde, pero ahora es posible terminar**.
* Se pueden **ir eliminando procesos** bloqueados, para que los demas tengan los recursos para terminar
```diff
+ ---------------------------------------------------------------------------
```
## **ABORTAR**
Tenemos dos métodos, en ambos, **el sistema recupera todos los recursos asignados** a los procesos terminados. 
### **1. Abortar TODOS los procesos interbloqueados**
* **Romperá el ciclo**, pero con un **costo muy elevado**
* **Habrá que descartar los resultados** de estos cálculos parciales.

### **2. Eliminar 1 a 1**
* El orden en que se seleccionan los procesos para abortarlos debe basarse en algún **criterio de costo mínimo**.
 * Por cada **iteracion** se debe **acudir al algoritmo**. 
* **Tarda** en mucho tiempo 
* Si éste se encuentra **actualizando un archivo, puede que se corrompa**.
* Abortar los procesos con el **menor costo posible**

### Prioridades
* ***Prioridad:*** 
Se elimina el proceso de **menor prioridad**. 
* ***Tiempo de procesador:*** Abortara el **proceso que haya utilizado menos tiempo** el procesador, ya que se pierde menos trabajo y facil de recuperar. 
* ***Tipos de recursos:*** **Recursos son muy necesarios y escasos** será preferible **liberarlos cuanto antes**. 
* ***Cantidad de Recursos:*** Eliminar los que **mas recursos** usen.
* ***Suspensión / reanudación:*** Trabajo **facil de recuperar**. 
```diff
+ ---------------------------------------------------------------------------
```
## **APROPIACION**
**Quitar** recursos y **asignar a otros** hasta romper el ciclo.

Si se utiliza la apropiación de recursos para tratar los interbloqueos, hay que considerar tres aspectos: 
* Selección de la víctima: A quien le quitaremos. 
* Retroceso: Cuanto vamos a perder.
* Bloqueo indefinido: Cuanto nos vamos a tardar.

## Detección y Recuperación
Estrategia que se utiliza en **grandes computadoras**, especialmente **sistemas por lote** en los que la **eliminación y su reinicio** suele aceptarse.
```diff
+ ---------------------------------------------------------------------------
```
## **ESTRATEGIAS INTEGRADAS** 
**Puede ser mas eficiente usar diferente estrategias** en diferentes situaciones, una de ellas sugiere lo siguiente: 

* Agrupar los recursos clases diferentes.
* Ordenación lineal para la prevención de circulo viciosos de espera e impedir el interbloqueo entre clases de recursos.
* Dentro de cada clase emplear el algoritmo mas apropiado.

### Ejemplo:
- ***Espacio intercambiable***: bloques de memoria en almacenamiento secundario para el intercambio de procesos.
- ***Recursos de procesos:*** dispositivos asignables, como unidades de cintas y archivos.
- ***Memoria principal:*** asignable a los procesos en paginas o segmentos.
- ***Recursos internos:*** como canales de E / S.
```diff
+ ---------------------------------------------------------------------------
```
## **ALG. BANQUERO**
## Interbloqueo:
Se solicitan mas recursos de los disponibles.
## Estado seguro:
Se pueden ejecutar sin interbloqueos.
## Analogia
Los **clientes solicitan dinero** pero tiene que haber dinero para dar y **no quedarse sin dinero fisico**.  
### Requerimientos
* **Numero fijo de recursos asignables**.
* **Usuarios Constantes**.
* El banquero debe **satisfacer todas las solicitudes**.
* Los clientes **garantizan los pagos**
* Los usuarios deben **indicar sus necesidades máximas** por adelantado.
```diff
- ---------------------------------------------------------------------------
```
