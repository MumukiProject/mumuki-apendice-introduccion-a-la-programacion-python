<ul>
  <li><a title="" href="#listas">Listas</a></li>
  <ul>
    <li><a title="" href="#acceso-indexado">Acceso indexado</a></li>
    <li><a title="" href="#reordenamiento">Reordenamiento</a></li>
  </ul>
  <li><a title="" href="#secuencias">Secuencias (<code>iterable</code>s)</a></li>
  <li><a title="" href="#repeticion-indexada">Repetición indexada</a></li>
  <li><a title="" href="#listas-por-comprension">Listas por comprensión</a></li>
  <ul>
    <li><a title="" href="#filtrados">Filtrados</a></li>
    <li><a title="" href="#mapeos">Mapeos</a></li>
  </ul>

</ul>

<h2>Estructuras de datos</h2>

Las listas y los diccionarios son tipos de datos compuestos que nos serán de gran utilidad a la hora de modelar situaciones más complejas en nuestros programas. 

<h3 id="listas">Listas</h3>

Son agrupaciones que tienen dos características fundamentales:

  * Admiten elementos duplicados: es decir que una lista puede tener varias veces al mismo elemento, pero en posiciones distintas
  * Tienen un orden: esto significa que mantienen el orden en que se hayan agregado los elementos

Por ejemplo: 

```python
ム promedios_de_lluvias_mensuales = [10, 15, 98, 2, 3, 3, 10]
# como admiten duplicados, el 10 y el 3 aparecen varias veces y eso no representa ningún problema...
ム promedios_de_lluvias_mensuales
[10, 15, 98, 2, 3, 3, 10]
# ...y como tienen orden, podemos diferenciarlas de otras con iguales elementos en posiciones distintas:
ム promedios_de_lluvias_mensuales == [3, 98, 10, 15, 2, 3, 10]
False
```

<h4 id="reordenamiento">Reordenamiento</h4>

Las listas pueden ser reordenadas, usando `sorted` y `list.sort`. Estas operaciones reubican los elementos de una lista según su _orden natural_ (es decir, de menor a mayor):  

```python
# sorted es una función
# por lo que devuelve una lista nueva...
ム sorted(promedios_de_lluvias_mensuales)
[2, 3, 3, 10, 10, 15, 98]
# ... dejando la original sin cambios
ム promedios_de_lluvias_mensuales
[10, 15, 98, 2, 3, 3, 10]
# list.sort es un procedimiento...
ム list.sort(promedios_de_lluvias_mensuales)
# ... por lo que no devuelve nada
# pero modifica a la lista original
ム promedios_de_lluvias_mensuales
[2, 3, 3, 10, 10, 15, 98]
```

<h4 id="acceso-indexado">Acceso indexado</h4>

De forma similar a los strings, las listas también soportan
un operador `[]`, que podemos leer como _operador de indexación_, _operador de acceso indexado_ u _operador corchetes_. Y al igual que con los strings, ¡se empieza a contar desde cero! 

```python
ム promedios_de_lluvias_mensuales[0] # el primer elemento
2
ム promedios_de_lluvias_mensuales[3] # el cuarto elemento
10
```

👀 En este punto hay que tener cuidado y mirar con atención, porque estaremos usando los corchetes (`[` y `]`) para tres cosas bastante diferentes: 

  * construir listas _literales_ (es decir, indicando por explícitamente y por extensión todos sus elementos: `["hola", "mundo", "de", "listas"]`;
  * acceder a una lista por índice: `una_lista[42]`;
  * obtener una rebanada o segmento de la lista:  `otra_lista[1:5]`

Más confuso puede ser si combinamos todas estas sintaxis 😖 : 

```python
# el primer elemento de la lista [10, 45, 98]
ム [10, 45, 98][0]
10
# el último elemento de la lista [10, 45, 98]
ム [10, 45, 98][-1]
98
# la sublista entre el segundo y el anteúltimo elemento 
ム [10, 45, 98][1:-1] 
[45]
# el primer elemento de la sublista anterior 
ム [10, 45, 98][1:-1][0]
45
```

¡Pero todo es cuestión de práctica! Sólo recordá que los mismos símbolos pueden significar cosas diferentes según el contexto 😉.

<h3 id="secuencias">Secuencias (<code>iterable</code>s)</h3>

Si queremos saber la cantidad de elementos de una lista, podemos utilizar `len`: 

```python
ム len(promedios_de_lluvias_mensuales)
7
```

¡Pero momento! ¿Otra vez `len`? 🤨 Anteriormente vimos que `len` permite conocer la cantidad caracteres de un string... 

```python
ム len("lluvia")
6
```

...y también para el largo de los rangos (`range`):

```python
ム len(range(0, 10))
10
```

Esto es porque rangos, listas y strings son todas secuencias, también conocidas como `iterable`s en Python, que podemos pensar como una _generalización_ de las cosas que pueden ser recorridas 🤯. En otras palabras, varias de las funciones y operadores que anteriormente vimos no son específicas de un tipo de dato, sino que funcionan con secuencias: 

 * El operador `in`
 * `sum` (excepto por los strings, dado que no podemos sumar sus letras)
 * `len`
 * `sorted`
 * `max` y `min`

Ejemplos: 

```python
ム sum(range(1, 9))
36
ム max("abczd")
"z"
ム "hola" in "hola mundo"
True
ム "funciones" in ["funciones", "procedimientos", "variables", "listas"]
True
ム 12 in range(10, 15)
True
```

<h3 id="repeticion-indexada">Repetición indexada</h3>

Las listas (y en general, todas las _secuencias_) pueden ser _recorridas_, visitando y haciendo algo con cada uno de sus elementos. Para ello contamos con la estructura de control `for...in`, que lleva su generador delante de dos puntos (`:`) y su cuerpo tabulado:

```python
patrimonios_de_la_humanidad = [
  {"declarado": 1979, "nombre": "Parque nacional Tikal", "pais": "Guatemala"},
  {"declarado": 1983, "nombre": "Santuario histórico de Machu Picchu", "pais": "Perú"},
  {"declarado": 1986, "nombre": "Parque nacional do Iguaçu", "pais": "Brasil"},
  {"declarado": 1995, "nombre": "Parque nacional de Rapa Nui", "pais": "Chile"},
  {"declarado": 2003, "nombre": "Quebrada de Humahuaca", "pais": "Argentina"}
 ]

cantidad_patrimonios_declarados_en_este_siglo = 0
for patrimonio in patrimonios_de_la_humanidad:
  if patrimonio["declarado"] >= 2000:
    cantidad_patrimonios_declarados_en_este_siglo += 1
    
```

<h3 id="listas-por-comprension">Listas por compresión</h3>

Las listas por comprensión son expresiones que nos permiten a partir de una o más listas, crear otra nueva mediante la realización de operaciones mapeado y filtrado. En otras palabras, nos permiten implementar recorridos de forma más compacta y declarativa que con `for...in` tradicional.  

<h4 id="filtrados">Filtrados</h4>

Para filtrar una lista es posible usar listas por comprensión en la forma `[...transformacion... for elemento in lista if ...condicion...]`. Por ejemplo, la siguiente expresión.... 

```python
[ persona for persona in personas if persona['tiene_auto'] ]
```

... es equivalente a la siguiente porción de código que emplea repetición indexada: 

```python
personas_con_auto = []
for persona in personas: 
  if persona['tiene_auto']:
    list.append(personas_con_auto, persona)
personas_con_auto  
```

<h4 id="mapeos">Mapeos</h4>

Además de filtrar con usando `if`, también podemos poner una expresión más complejas en `...transformacion...` y así obtener listas nuevas conformadas por los elementos de la original, pero transformados según dicha expresión. Por ejemplo, la siguiente expresión...

```python
[ persona['nombre'] for persona in personas ]
```
... es equivalente a lo siguiente: 

```python
nombres_de_personas = []
for persona in personas: 
  list.append(nombres_de_personas, persona['nombre'])
nombres_de_personas  
```



