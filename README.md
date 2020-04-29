# Dataset de Noticias Chilenas en Español

Dataset creado para el Trabajo de Titulación de pregrado de Ingeniería Civil en Informática de la Universidad de Valparaíso.

---

## Descripción

El dataset incluye un fragmento de 40 noticias ocurridas en Chile de un total de 300, que sucedieron entre los meses de junio de 2019 y enero 2020, todas publicadas en Twitter. Los temas más frecuentes en este dataset está la Copa américa 2019, el paro docente, el eclipse solar, el corte de agua en Osorno, y la crisis social. Cada noticia incluye el id de la publicación, el texto de la publicación, fecha y hora de publicación, la etiqueta de veracidad de 4 estados y el árbol de propagación asociada a ésta. La obtención de los datos incluidos en este dataset fue a través del uso de la API de Twitter usando la cuenta gratuita la cual presenta ciertas limitaciones motivo por la cual se omitieron las "citas" en el dataset por lo costoso de obtenerlos todos. Si bien este dataset está pensado para que sea usado en Machine Learning, éste no está dividido en test y train la cual debe hacer este proceso manualmente.

La creación de este dataset fue en base a la necesidad de usar un conjunto de datos en español ya que en trabajos relacionados en la investigación de detección de noticias falsas, que es un área que está su etapa madura, no existe datasets con noticias en español con etiquetas de veracidad, aunque si bien puede ser creado usando la API de Twitter, puede tardar un tiempo en recolectar datos suficientes para trabajar con ello, sobre todo si se se usa la cuenta gratuita de la API, y a eso también se debe sumar el tiempo necesario para poder etiquetar todas las noticias descargadas. 

## Elementos importantes en el dataset

Este dataset tiene una etiqueta de veracidad de 4 estados basándose en la verificación de hechos en el transcurso del tiempo, las cuales son:

- **Noticia No rumor:** publicación realizada casi al mismo tiempo de haber ocurrido los eventos descritos en ella, la cual es considerado un hecho. 
- **Noticia Verdadera:** publicación que lleva un tiempo publicado la cual fue corroborada por medios oficiales.
- **Noticia Falsa:** es aquella noticia cuyo contenido haya estado publicada por un tiempo, se ha desmentido por medios oficiales.
- **Noticia No verificada:** es aquella publicación que hasta la fecha no se ha podido verificar los hechos.

Otro elemento presente en este dataset es el **Árbol de propagación** la cual es el conjunto de reacciones que interactúa con una noticia, en este caso en un tweet, la cual tiene una forma de árbol ya que la publicación sería la raíz y toda interacción de ella como comentarios corresponden a las hojas y subárboles. En términos de este dataset, una publicación es decir un tweet **1)** o un hilo de tweets **6)**, corresponden a la raíz del árbol, cuya publicación se puede propagar a través de retweets **3)**, comentarios **2)**, y citas **4)**, las dos últimas pueden propagarse de la misma forma que una noticia raíz la cual en este caso es considerado como un subárbol tal como se muestra los 3 globos ubicados en el nivel central del árbol de la izquierda.

![detalle arbol](./Arbol_Propagacion.png)

## Detalles técnicos del dataset

### Distribución de noticias según su estado de veracidad
<ul>
	<li><b>noticias falsas:</b> 53</li>
	<li><b>noticias verdaderas:</b>		87</li>
	<li><b>noticias no rumor:</b>		111</li>
	<li><b>noticias no verificadas:</b>	49</li>
</ul>
<ul>
    <li><b>noticias totales:</b> 300</li>
</ul>


## Descripción de contenido del dataset
El dataset tiene 2 tipos de archivo, el primero incluye el listado de las noticias publicadas en Twitter con su respectiva etiqueta y el segundo archivo incluye el árbol de propagación asociada a esta publicación.

### lista de noticias
Contenido incluido en el primer archivo cuyas tablas son las siguientes:

- **tweet_id:** id del evento en Twitter.
- **texto:** texto de la noticia.
- **fecha de publicación:** Fecha y hora en utc 0 de cuando se publicó la noticia.
- **etiqueta:** Etiqueta de veracidad `Verdadero`, `Falso`, `No Verificado`, `No Rumor`.
- **web de publicación:** web que hace referencia a la publicación hecha en Twitter.
- **Observación:** Observación sobre la publicación.


### objeto retweet en Árbol
Estas tablas pertenece al objeto retweet, uno de los dos objetos incluidos en el segundo archivo.

- **id_usuario:** id del usuario quien hizo el retweet.
- **fecha de publicación:** fecha y hora en utc 0 de cuando se realizo el retweet.
- **timedelta_time:** tiempo transcurrido en minutos desde cuando se publico la noticia original.

### objeto tweet en Árbol
Estas tablas pertenece al objeto tweet, uno de los dos objetos incluidos en el segundo archivo.

- **tweet_id:** tweet_id del comentario.
- **tweet_id_fuente:** tweet_id a quién se está respondiendo.
- **timedelta_time:** tiempo transcurrido en minutos desde cuando se publico la noticia original.
- **fecha de publicación:** fecha y hora en utc 0 de cuando se publico el comentario
- **tweets:** subárbol asociado a esta publicación (véase objeto retweet en Árbol).
- **retweets:** retweets realizado a esta publicación (Véase objeto tweet en Árbol).

## Contenido del dataset en el repositorio

Por [políticas de privacidad de la API de Twitter](https://developer.twitter.com/en/developer-terms/policy#4-e), la distribución del contenido de Twitter fuera de su servicio no está permitido exceptuando los ids, por lo cual en este repositorio se publicará sólo los ids en 2 tipos de archivos en donde el archivo `dataset/etiquetas.txt` incluirá el listado de las noticias acompañada con la etiqueta de veracidad y los archivos `dataset/<id_noticia>/<id_noticia>.min` listará los elementos del árbol.

Extracto del archivo [`dataset/etiquetas.txt`](./dataset/etiquetas.txt) que lista las noticias en ids con su etiqueta de veracidad asociada.
```javascript

No rumor:1149169121915023360
No rumor:1149895300812804096
No rumor:1150110141523492865
No verificado:1150188608768360449
Verdadero:1152564330346536964
Verdadero:1172179932421808130
No verificado:1173691271006826496
No rumor:1174324420481036289
No verificado:1174854243532050432
No rumor:1182419214356930560

```

Extracto del archivo `dataset/<id_noticia>/<id_noticia>.min` que lista las acciones que han ocurrido en una noticia, en este caso, a la noticia de id: [1188132627498307584](./dataset/1188132627498307584/1188132627498307584.min) en donde a la izquierda indica el tipo de acción, seguido del evento en cuestión incluyendo el id del usuario quien ha realizado la acción, el id de dicha de acción y el tiempo transcurrido desde la publicación de la noticia en minutos, y luego a la derecha, aparece el evento a la cual se está interactuando que pude ser la noticia origina o bien un comentario.
```php

retweet: ['3222122855','1188257116844445696','494.68']->['910572234166751235','1188153648720830464','83.53']
reply: ['2190186869','1188155562502119427','91.13']->['910572234166751235','1188153648720830464','83.53']
reply: ['3681725475','1188151882444873728','76.52']->['910572234166751235','1188132627498307584','0.0']
reply: ['120153485','1188157779627954176','99.95']->['910572234166751235','1188132627498307584','0.0']
retweet: ['910572234166751235','1188159231255601152','105.72']->['120153485','1188157779627954176','99.95']
retweet: ['1851909912','1188160428532215809','110.47']->['120153485','1188157779627954176','99.95']
retweet: ['1471726465','1188162996775870464','120.68']->['120153485','1188157779627954176','99.95']
retweet: ['1152997665715752965','1188177729188843521','179.22']->['120153485','1188157779627954176','99.95']
retweet: ['3222122855','1188256512654876675','492.28']->['120153485','1188157779627954176','99.95']
reply: ['304042341','1188158156163158017','101.43']->['910572234166751235','1188132627498307584','0.0']
reply: ['885314323446472706','1188159894639259648','108.35']->['910572234166751235','1188132627498307584','0.0']
retweet: ['3222122855','1188256680640942080','492.95']->['885314323446472706','1188159894639259648','108.35']
reply: ['317854608','1188163298967113728','121.88']->['885314323446472706','1188159894639259648','108.35']
reply: ['1099355116765876225','1188163302699995138','121.90']->['910572234166751235','1188132627498307584','0.0']
reply: ['1187497687387725825','1188169650238038017','147.12']->['910572234166751235','1188132627498307584','0.0']
```

## Acceso al dataset completo

Cualquier interesado en acceder al dataset personalizado creado en este trabajo para ser usado con fines académicos o de investigación, puede contactarse con desarrollador de este dataset que es daniel.toro@alumnos.uv.cl o la profesora encargada de este trabajo que es eliana.providel@uv.cl. También puede acceder al contenido usando la API a costa de más tiempo y la probabilidad de eventos eliminados incluyendo una noticia entera.

---

*nota: este repositorio no tiene traducción al inglés ya que está pensado a usuarios del habla hispana*

*note: this repositoy no have an english version because this thinked to spanish users.*


