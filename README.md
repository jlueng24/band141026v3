# Cartas del Mundo — versión 4.7

## Subir a GitHub Pages

Descomprime el ZIP y sube **el contenido de esta carpeta** a la raíz del repositorio. `index.html` debe quedar en la raíz, junto a `app.js`, `country-mysteries.js`, `country-card-data.js`, `achievements.js`, `achievements.json` y `countries-local.json`. Conserva toda la carpeta `img`: contiene los logros y el icono `cartas-icon.svg`. GitHub no ejecuta la aplicación si solo subes el archivo ZIP.

Al actualizar un sitio ya publicado, reemplaza los archivos existentes por los de esta versión. El progreso anterior permanece guardado en el navegador del jugador.

La primera pantalla pide el nombre de jugador. «Continuar» lleva a la selección de Banderas, Capitales, Mixto, Supervivencia, Estudio o Misterio del día. Las reglas y el progreso de las partidas anteriores se conservan. El final ahora muestra los aciertos y solo las cartas o logros nuevos; las partidas perfectas tienen un tratamiento propio.

En móvil, tanto la pantalla del jugador como la selección de modo muestran accesos directos a **Álbum** y **Logros**. En pantallas grandes, esos accesos siguen en la navegación lateral.

## Misterio del día: países

Cada fecha local selecciona el mismo país de un conjunto estable de 199 países del catálogo; se excluyen los territorios dependientes. La silueta aparece desde el principio con cuatro opciones fijas de la misma región. Las alternativas se eligen por subregión, proximidad y tamaño cuando los datos lo permiten. El jugador puede abrir hasta tres pistas de texto antes de elegir. Tiene **una sola respuesta**: si acierta, consigue el pin con independencia de las pistas abiertas; si falla, aparece el país correcto y termina el reto. Las pistas abiertas se guardan aunque cierre la ventana. El resultado y el pin quedan asociados al país; un pin puede mostrar su carta aunque la bandera y la capital aún estén pendientes. Los retos ya terminados conservan su resultado y los pines históricos cuyo país se hubiese guardado.

La silueta tiene un SVG independiente, ajustado a su espacio para que no se salga de la tarjeta. Se puede responder directamente al verla, sin abrir pistas.

Los 199 países tienen una ficha propia en `country-mysteries.js`. Se elige una pista difícil y dos de nivel intermedio sin repetir exactamente el mismo dato, de forma estable para cada fecha. Las categorías son río, montaña, monumento, ciudad distinta de la capital nacional, equipo de fútbol, frontera, moneda, idioma, personaje y silueta. Se incluyen 1.591 pistas candidatas en total. Cada pista conserva un enlace de fuente a Wikipedia en la ficha; los datos de monedas, idiomas y fronteras proceden también del catálogo mledoze/countries. Las categorías concretas varían según el país: una isla sin fronteras terrestres, por ejemplo, no recibe esa pista.

Los pines mantienen un marco dorado común. España, Japón e Islandia incorporan ilustraciones específicas; los demás utilizan la silueta individual del país con una combinación de color estable.

## Catálogos

- Europa tiene 45 países en `countries-local.json`, disponible aunque falle la carga mundial.
- El catálogo mundial se obtiene de [mledoze/countries](https://github.com/mledoze/countries), con licencia ODbL 1.0, y se guarda localmente tras una carga correcta. Si esa descarga falla, la aplicación muestra el alcance disponible y permite jugar Europa; no presenta 45 países como si fueran todo el mundo.
- Las banderas se muestran desde FlagCDN. Las imágenes de logros, en cambio, están incluidas en `img/logros`.
- Las cartas comparten un diseño para todos los continentes. El número XX001/999 se calcula por orden alfabético del catálogo disponible dentro de la región; el total incluye también los países sin descubrir. Si se usa el catálogo europeo de respaldo, España es EU016/045. Al regresar el catálogo mundial, su numeración refleja ese catálogo completo.
- Las siluetas se incluyen en `country-card-data.js`, adaptadas de [MapSVG](https://mapsvg.com/maps/world) bajo [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). La silueta de Antártida se derivó del GeoJSON de [mledoze/countries](https://github.com/mledoze/countries) (ODbL 1.0). Las monedas incluidas para uso sin conexión mundial proceden del mismo catálogo mledoze/countries (ODbL 1.0). La fuente y licencia del mapa también aparecen al pie del álbum.

## Verificación técnica

Ejecuta `node tests/smoke.cjs`. Comprueba catálogo y respaldo, modos de juego, Supervivencia, Estudio, silueta y cuatro opciones para los 199 países, tres pistas con fuentes, la respuesta única, logros, álbum y resultado final.

El catálogo mundial se sigue cargando desde la fuente original al jugar; si no hay conexión, las partidas normales ofrecen el respaldo europeo, pero el Misterio del día utiliza las pistas y siluetas locales de los 199 países sin depender de esa descarga.
