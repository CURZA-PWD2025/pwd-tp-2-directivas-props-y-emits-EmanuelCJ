## Comentarios

Emanuel, como estas? te comento que tenes algunos errores que corregir:
- la idea de tener un componente ``Card``es para que la logica de mostrar una pelicula recaida en el, vos estas utilizando como con ``CardList`` y renderizas de un contenedero ``div`` con la informacion y no estaria funcionando como se espera.
- el boton que cambia al hacer click esta mutando en todos las peliculas, esto pasa por lo mismo que te comente mas arriba, si tenes separada la logica de la lista del item podes tener encapsulado el comportamiento de cada boton
- Según como lo pensaste el emit no tendria sentido, ya que todo lo estas manejando en un componente y los emits son para comunicar componentes hijos con padres.
- todo lo que tenga que ver con data, interfaces, resources van en carpetas por fuera de la carpetad de componentes, si bien no es algo estricto te ayuda a la hora de organizar tus archivos de manera ordenada.
- te falto crear la interface para tipar el objeto Film/Pelicula
Fijate de corregir y reenviarlo asi te queda como debe ser.
