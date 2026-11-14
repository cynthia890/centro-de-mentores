# Centro de Mentores · Technovation México 2027

Sitio para los mentores voluntarios de Technovation México, hecho por Mentoralia A.C. (capítulo oficial de Technovation en México). Lo diseña y mantiene Cynn (Cynthia Rodríguez), coordinadora de mentores. Se publica con GitHub Pages desde este repositorio: https://cynthia890.github.io/centro-de-mentores

## Cómo trabajar con Cynn

- Escríbele en español, con calidez y de forma práctica.
- Explica los pasos de git o GitHub en lenguaje sencillo; no da por hecho que sabe programar.
- Antes de un cambio grande de diseño o estructura, propón primero y espera su visto bueno. Los cambios pequeños (una liga, un texto) hazlos directo.
- Después de cada cambio, revisa que la página no se rompa, haz commit con un mensaje claro en español y súbelo (push). Dile qué cambió.
- Ella piensa como diseñadora UX/UI: cuida la estética, la legibilidad y que todo se vea consistente.

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
- **Buscador**: busca en título, descripción y `palabras`, sin importar acentos. Las palabras clave incluyen sinónimos coloquiales (por ejemplo "permiso papas" encuentra el permiso de papás). Los filtros por etapa y tipo existen pero están ocultos a propósito.
- Las palomitas de los pasos se guardan en localStorage del navegador de cada mentor (claves `cm2027:...`).

## Orden de la página

Logos, banner, título y bienvenida, accesos rápidos, Avisos, ¿Dónde estoy en mi temporada?, tarjeta del Club Virtual, Encuentra lo que buscas, Cuando algo se complica, Cómo nos comunicamos, Preguntas frecuentes y Contacto. Aparte, las vistas `#club-virtual` y `#tutoriales`.

## Diseño

- Paleta TGMX (de Andy, diseño de Mentoralia): fondo `#EDEDED`, texto `#1D1349`, magenta `#EB0089`, amarillo `#FDB71C`, azul `#0076CF`, verde `#42B12A`, naranja `#FF7400`.
- Colores por etapa: Entrada amarillo, Vinculación naranja, Aprendizaje azul, Entregas verde, Competencia morado, Celebración magenta. El magenta también marca seguridad y "Cuando algo se complica".
- Tipografías: Bricolage Grotesque (títulos) y Atkinson Hyperlegible (texto).
- Tiene modo oscuro y está pensado para celular.
- Tono relajado y cálido ("¡Oh-oh! No encontramos lo que buscas", "tú tranquilo/a"), excepto en seguridad, que se mantiene serio.

## Reglas de contenido

- El programa se llama "Technovation" (sin "Girls"). Las antiguas "embajadoras" ahora se llaman **líderes de club**.
- Se dice "permiso de papás", no "parental consent".
- Lo que tenga que ver con el equipo se ve con su líder de club; si no se resuelve, con Mentoralia. En el Club Virtual, el líder de club es Mentoralia.
- El sitio es público. **Nunca** pongas la liga del WhatsApp de mentores ni ligas de Zoom de sesiones con las niñas. La liga del WhatsApp aparece en el mensaje de confirmación del quiz de Google Forms.
- Requisitos para ser mentor: mayor de 18 años, de 2 a 4 horas a la semana, capacitación global (6 módulos), perfil y background check en la plataforma, capacitación de Mentoralia (en vivo o grabación) y quiz con mínimo 80%.
- Contacto: cynthia@mentoralia.org (coordinación de mentores) e info@mentoralia.org.

## Pendientes

- Llenar las ligas de los recursos (hoy casi todas están en `"#"`).
- Fechas de etapas: ya están, tomadas del timeline oficial de la temporada 2027 (registro 11 mar, inicio recomendado 10 feb, entrega 5 may, 1ª ronda 11 may–7 jun, semifinalistas 14 jun, 2ª ronda 15–28 jun, celebración virtual 2 jul, World Summit por confirmar). Son estimadas: el inicio de Entrada y Vinculación, el fin de Aprendizaje y el inicio de Entregas ("abr"). Confirmar con Cynn cuando haya fechas de capacitación.
- Conectar la hoja de avisos: pegar en `avisosHoja` la liga CSV cuando Cynn la publique.
- Poner la liga del Classroom de talleres virtuales (`grab-talleres`) y de los videos de Tutoriales.
- Idea a futuro: que la lista de recursos también se lea desde la Google Sheet, en una pestaña "Recursos".
- Más adelante, el repositorio podría pasarse a la cuenta de GitHub de Mentoralia.
