# Dataset de Noticias Chilenas en Español

Dataset creado para el Trabajo de Titulación de pregrado de Ingeniería Civil en Informática de la Universidad de Valparaíso.

---

## Descripción

El dataset incluye una colección de 300 noticias ocurridas Chile que sucedieron entre los meses de junio de 2019 y enero 2020, todas publicadas en Twitter. Los temas más frecuentes en este dataset está la Copa américa 2019, el paro docente, el eclipse solar, el corte de agua en Osorno, y la crisis social. Cada noticia incluye el id de la publicación, el texto de la publicación, fecha y hora de publicación, la etiqueta de veracidad de 4 estados y el árbol de propagación asociada a ésta. La obtención de los datos incluidos en este dataset fue a través del uso de la API de twitter usando la cuenta gratuita la cual presenta ciertas limitaciones motivo por la cual se omitieron las "citas" en el dataset por lo costoso de obtenerlos todos. Si bien este dataset está pensado para que sea usado en Machine Learning, éste no está dividido en test y train la cual debe hacer este proceso manualmente.

La creacion de este dataset fue en base a la necesidad de usar un conjunto de datos en español ya que en trabajos relacionados en la investigación de detección de noticias falsas, que es un área que está su etapa madura, no existe datasets con noticias en español con etiquetas de veracidad, aunque si bien puede ser creado usando la API de Twitter, puede tardar un tiempo en recolectar datos suficientes para trabajar con ello, sobre todo si se se usa la cuenta gratuita de la API, y a eso también se debe sumar el tiempo necesario para poder etiquetar todas las noticias descargadas. 

## Elementos importantes en el dataset

Este dataset tiene una etiqueta de veracidad de 4 estados basandose en la verificación de hechos en el transcurso del tiempo, las cuales son:

- **Noticia No rumor:** publicacion realizada casi al mismo tiempo de haber ocurrido los eventos descritos en ella, la cual es considerado un hecho. 
- **Noticia Verdadera:** publicación que lleva un tiempo publicado la cual fué corroborada por medios oficiales.
- **Noticia Falsa:** es aquella noticia cuyo contenido haya estado publicada por un tiempo, se ha desmentido por medios oficiales.
- **Noticia No verificada:** es aquella publicación que hasta la fecha no se ha podido verificar los hechos.

Otro elemento presente en este dataset es el **Árbol de propagación** la cual es el conjunto de reacciones que interactúa una noticia, en este caso en un tweet, la cual tiene una forma de árbol ya que la publicación sería la raíz y toda interaccion de ella como comentarios corresponden a las hojas y subárboles. En términos de este dataset, una publicación es decir un tweet **1)** o un hilo de tweets **6)**, corresponden a la raíz del árbol, cuya publicación se puede propagar a traves de retweets **3)**, comentarios **2)**, y citas **4)**, las dos últimas pueden propagarse de la misma forma que una noticia raís la cual en este caso es considerado como un subárbol tal como se muestra los 3 globos ubicados en el nivel central del árbol de la izquierda.

![detalle arbol](./Arbol_Propagacion.png)

## Detalles técnicos del dataset

### Distribucion de noticias seún su estado de veracidad
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
- **fecha de publicación:** fecha y hora en utf 0 de cuando se realizo el retweet.
- **timedelta_time:** tiempo transcurrido en minutos desde cuando se publico la noticia original.

### objeto tweet en Árbol
Estas tablas pertenece al objeto tweet, uno de los dos objetos incluidos en el segundo archivo.

- **tweet_id:** tweet_id del comentario.
- **tweet_id_fuente:** tweet_id a quién se está respondiendo.
- **timedelta_time:** tiempo transcurrido en minutos desde cuando se publico la noticia original.
- **fecha de publicación:** fecha y hora en utf 0 de cuando se publico el comentario
- **tweets:** subárbol asociado a esta publicación (véase objeto retweet en Árbol).
- **retweets:** retweets realizado a esta publicación (Véase objeto tweet en Árbol).

## Acceso al dataset completo
Desafortunadamente, por temas de políticas de privacidad descrita en los términos de uso de la API de Twitter en https://developer.twitter.com/en/developer-terms/policy#4-e, la redistribución del contenido de Twitter al público no está permitido, es por esto que en este repositorio sólo incluirá el archivo `etiquetas.txt` que incluye el listado de las noticias en id acompañado con la etiqueta de veracidad y los archivos `<id_noticia>/<id_noticia>.min` que lista los elementos del árbol usando los ids y el tiempo transcurrido en minutos desde el momento de cuando se publico la noticia.

Si estás interesado en usar el contenido completo de este dataset para ser usado con fines académicos o de investigación, puede contactarse con desarrollador de este dataset que es daniel.toro@alumnos.uv.cl o la profesora encargada de este trabajo que es eliana.providel@uv.cl.

---

*nota: este repositorio no tiene traducción al inglés ya que está pensado a usuarios del habla hispana*

*note: this repositoy no have an english version because this thinked to spanish users.*