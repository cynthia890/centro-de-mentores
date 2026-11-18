# Centro de Mentores · Technovation México 2027

Sitio para los mentores voluntarios de Technovation México, hecho por Mentoralia A.C. (capítulo oficial de Technovation en México). Lo diseña y mantiene Cynn (Cynthia Rodríguez), coordinadora de mentores. Se publica con GitHub Pages desde este repositorio: https://cynthia890.github.io/centro-de-mentores

## Cómo trabajar con Cynn

- Escríbele en español, con calidez y de forma práctica.
- Explica los pasos de git o GitHub en lenguaje sencillo; no da por hecho que sabe programar.
- Antes de un cambio grande de diseño o estructura, propón primero y espera su visto bueno. Los cambios pequeños (una liga, un texto) hazlos directo.
- Después de cada cambio, revisa que la página no se rompa, haz commit con un mensaje claro en español y súbelo (push). Dile qué cambió.
- Ella piensa como diseñadora UX/UI: cuida la estética, la legibilidad y que todo se vea consistente.
- María es la jefa de Cynn en Mentoralia y revisa el sitio. Andy Lozano es quien lleva el diseño de Mentoralia y tiene la guía de identidad visual.

## Cómo está armado

Todo vive en un solo archivo: `index.html` (HTML, CSS y JavaScript juntos; las imágenes del banner y los logos van incrustadas en base64).

- **Todo el contenido editable está en el objeto `CONFIG`**, dentro del `<script>`, entre los comentarios `CONTENIDO DEL CENTRO DE MENTORES` y `FIN DEL CONTENIDO`. Ahí están: `etapaActual`, `contacto`, `avisosHoja`, `avisosEjemplo`, `accesos`, `quizAviso`, `whatsapp`, `recursos`, `etapas`, `clubVirtual`, `casos`, `seguridad`, `canales`, `conTuEquipo` y `preguntas`.
- **Cada recurso se escribe una sola vez** en `CONFIG.recursos` (id, titulo, desc, etapa, tipo, palabras, liga). Las etapas, el Club Virtual, los Tutoriales, los accesos rápidos y el buscador lo toman de ahí por su `id`. Para poner una liga, cambia `liga: "#"` en ese recurso.
- Campos opcionales de un recurso: `tutorial: "plataforma"` o `tutorial: "grabacion"` (sale también en la página de Tutoriales, en esa sección) y `ocultarSinLiga: true` (no se muestra en ningún lado mientras su liga sea `"#"`; hoy lo usa "Cómo aceptar tu vinculación con el equipo en la plataforma").
- **Etapas** (en orden): entrada, vinculacion, aprendizaje, entregas, competencia, celebracion. Para cambiar de etapa se cambia `etapaActual`.
- **Avisos**: se leen de la Google Sheet "Avisos Centro de Mentores" (pestaña Avisos) publicada como CSV. Mientras `avisosHoja` esté vacío, se muestran los `avisosEjemplo`. Columnas: fecha | tipo | titulo | texto | liga | texto_liga | hasta. Tipos: importante, fecha, general.
- **Club Virtual**: es una vista aparte. Solo se ve al entrar con `#club-virtual` al final de la liga o al dar clic en su tarjeta. Sus recursos (etapa `club`) no salen en el buscador general. Las grabaciones de la sesión informativa y de la orientación del Club Virtual solo van aquí, no en Tutoriales.
- **Tutoriales**: también es una vista aparte, con el mismo patrón que el Club Virtual. Se abre con `#tutoriales` (el acceso rápido "Tutoriales de la plataforma" lleva ahí) y tiene dos secciones: "Tutoriales de la plataforma" (`tutorial: "plataforma"`) y "Grabaciones de sesiones" (`tutorial: "grabacion"`). Las tarjetas se ordenan por etapa y muestran su etapa. Cada video sigue apareciendo en su etapa y en el buscador.
- **Classroom de talleres virtuales** (recurso `grab-talleres`): ahí viven las grabaciones de los talleres y los videos de "Inspírate". "Cómo descargar tu certificado" es una guía escrita, no un video.
- **WhatsApp de mentores**: el acceso rápido (y cualquier liga a `#whatsapp`) abre una ventanita: la liga se da al terminar el quiz de evaluación, y si ya lo hicieron y no la tienen, un botón abre un correo a Cynn con asunto y texto ya escritos. Los textos están en `CONFIG.whatsapp`. La liga del grupo nunca va en el sitio.
- **Asesorías de programación** empiezan en marzo; por eso no están en los accesos rápidos (sí en su etapa y en el buscador). "Cuando algo se complica" tampoco está en los accesos rápidos (se quitó a pedido de Cynn), pero su sección sigue en la página.
- **Quiz de evaluación** (acceso rápido): mientras el recurso `quiz` tenga liga `"#"`, el botón abre una ventanita con el anuncio de `CONFIG.quizAviso` (estamos trabajando en él; se necesita al menos 80% para vincularse). En cuanto el quiz tenga liga, el botón lleva directo al quiz.
- En las respuestas de las preguntas frecuentes, `[texto](#seccion)` se vuelve una liga dentro de la página (hoy: "¿Qué hago si una familia no da el permiso de papás?" lleva a #complica). La tarjeta "Familias y permisos" de Cuando algo se complica lleva el campo `primero` ("Primero: habla con tu líder de club.").
- **Buscador**: busca en título, descripción y `palabras`, sin importar acentos. Las palabras clave incluyen sinónimos coloquiales (por ejemplo "permiso papas" encuentra el permiso de papás). Los filtros por etapa y tipo existen pero están ocultos a propósito.
- **Pasos de Entrada (nov 2026, tras la prueba con mentores):** 1 registro como mentor en la plataforma (cierra el 22 de marzo), 2 capacitación global, 3 perfil, 4 background check (etiqueta "Obligatorio", campo `obligatorio: true`), 5 registro a la sesión Zoom, 6 asistir o ver la grabación, 7 quiz. La sesión de profundización (`opcional: true`) no se numera: sale abajo en el bloque "Extra opcional" y no cuenta en la barra. Arriba de los pasos (Entrada y Club Virtual) va: "Ve marcando tú cada paso conforme lo completes. Se guarda en este navegador."
- Las palomitas se guardan en localStorage (claves `cm2027:<etapa>:<posición del paso en CONFIG>`). Si agregas o quitas pasos, las palomitas se recorren; por eso hay migraciones únicas: `cm2027:migr-bg` (background check aparte) y `cm2027:migr-registro` (paso de registro al inicio).
- Un recurso (o un paso) puede llevar `info: [{ t, r }]`: se muestra un botón ⓘ que abre una burbuja con preguntas y respuestas, en la tarjeta del recurso (buscador, etapas, Tutoriales) y en el paso que lo use. Hoy lo usa el recurso `background` (background check), que también alimenta el paso 3 de Entrada. Se presenta como una medida para cuidar la seguridad de las participantes. Del background check aún falta confirmar si en México es con Checkr o con documentos; dudas a volunteers@technovation.org (Megan y Rae).

## Orden de la página

Logos, banner, título y bienvenida, accesos rápidos, Avisos, ¿Dónde estoy en mi temporada?, tarjeta del Club Virtual, Encuentra lo que buscas, Cuando algo se complica, Cómo nos comunicamos, Preguntas frecuentes y Contacto. Aparte, las vistas `#club-virtual` y `#tutoriales`.

## Diseño

- **Colores: solo los de la guía de Andy** ("Nueva identidad Technovation 2026-2027"). Fondo `#EDEDED`, tarjetas y barras en crema `#FAF4EC` (no se usa blanco), texto `#1D1349`, magenta `#EB0089`, amarillo `#FDB71C`, azul `#0076CF`, verde `#42B12A`, naranja `#FF7400`, morado `#8C72DE` (Competencia) y coral `#F28587` (cejas en modo oscuro). Excepciones a propósito, "tonos de apoyo web" pendientes de que Andy los sume a su guía: `#4D4672` texto secundario, `#D6D3DE` líneas, `#9C98AD` pasos completados, `#FCE1F0` fondo de alertas, y los fondos/textos del modo oscuro (`#120C2E`, `#352B66`, `#3A1240`, `#BDB8D3`, `#6C6690`).
- Colores por etapa: Entrada amarillo, Vinculación naranja, Aprendizaje azul, Entregas verde, Competencia morado, Celebración magenta. El magenta también marca seguridad y "Cuando algo se complica".
- Tipografías (guía de Andy): **Rubik** 700 para títulos, **Instrument Sans** para textos y **Castoro cursiva** (clase `.enf`) para una palabra de cada título, del mismo color del título (estilo limpio y uniforme que prefiere Cynn). También van en Castoro cursiva el subtítulo "Technovation México 2027" (magenta) y la frase de cada etapa.
- **Cejas**: etiqueta pequeña en mayúsculas arriba de los títulos de sección (clase `.ceja`), en magenta (coral en modo oscuro). Es el acento propio de Technovation México/Mentoralia.
- Tiene modo oscuro y está pensado para celular. En computadora hay un botón "Modo oscuro / Modo claro" junto al logo de Mentoralia (la elección se guarda en `cm2027:tema`); en celular se sigue el modo del teléfono.
- Las fechas de cada etapa se ven como pastillas con el color de su etapa, también en la etapa actual (junto a "Estás aquí").
- **Identidad visual (comentario de María, nov 2026):** las páginas hechas con IA deben alinearse con la identidad de Mentoralia. En nov 2026 el sitio se alineó a la guía de Andy (colores y tipografías de arriba). Cuando Andy actualice su guía, revisar el sitio contra la versión nueva.
- Tono relajado y cálido ("¡Oh-oh! No encontramos lo que buscas", "tú tranquilo/a"), excepto en seguridad, que se mantiene serio.

## Reglas de contenido

- El programa se llama "Technovation" (sin "Girls"). Las antiguas "embajadoras" ahora se llaman **líderes de club**.
- Se dice "permiso de papás", no "parental consent".
- Lo que tenga que ver con el equipo se ve con su líder de club; si no se resuelve, con Mentoralia. En el Club Virtual, el líder de club es Mentoralia.
- El sitio es público. **Nunca** pongas la liga del WhatsApp de mentores ni ligas de Zoom de sesiones con las niñas. La liga del WhatsApp aparece en el mensaje de confirmación del quiz de Google Forms.
- Directorio de líderes de club: https://hub.mentoralia.org/clubes (corrección de María; antes apuntaba a /club/red-de-clubes).
- Requisitos para ser mentor: mayor de 18 años, de 2 a 4 horas a la semana, capacitación global (6 módulos), perfil y background check en la plataforma, capacitación de Mentoralia (en vivo o grabación) y quiz con mínimo 80%.
- Contacto: cynthia@mentoralia.org (coordinación de mentores) e info@mentoralia.org.

## Pendientes

- Llenar las ligas de los recursos (hoy casi todas están en `"#"`).
- Fechas de etapas (nov 2026): Camino de aprendizaje "Febrero a mayo", Entregas "Hasta el 5 de mayo", Celebración "Mayo (según tu región)"; Entrada, Vinculación y Competencia dicen "Fechas por confirmar". Timeline oficial de referencia: registro de equipos 11 mar, registro de mentores 22 mar, inicio recomendado 10 feb, entrega 5 may, 1ª ronda 11 may–7 jun, semifinalistas 14 jun, 2ª ronda 15–28 jun, anuncio virtual de finalistas y ganadoras regionales 2 jul, World Summit 2027 por confirmar.
- Conectar la hoja de avisos: pegar en `avisosHoja` la liga CSV cuando Cynn la publique.
- Poner la liga del Classroom de talleres virtuales (`grab-talleres`) y de los videos de Tutoriales.
- Idea a futuro: que la lista de recursos también se lea desde la Google Sheet, en una pestaña "Recursos".
- Más adelante, el repositorio podría pasarse a la cuenta de GitHub de Mentoralia.
