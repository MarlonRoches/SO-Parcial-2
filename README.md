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
## **ESTRATEGIAS DE DETECCION** 




