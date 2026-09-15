# AccessRide Colombia

Prototipo de aplicación web de transporte accesible para personas con discapacidad en Colombia. Conecta usuarios con conductores y vehículos adaptados (rampa, elevador, espacio para silla de ruedas, apoyo visual/auditivo, opción Pet Friendly), con rutas calculadas sobre calles reales y un botón de emergencia con contacto de confianza.

> **Proyecto de grado / prototipo académico.** No procesa pagos reales ni reemplaza servicios de transporte certificados.

## Demo

Publicado con GitHub Pages

## Funcionalidades

**Cuentas y perfil**
- Registro de usuarios con correo y contraseña, con foto de perfil opcional (o avatar generado automáticamente).
- Inicio de sesión persistente: la sesión se mantiene activa al recargar la página o volver más tarde.
- Modo de prueba: crea una cuenta temporal con datos de ejemplo sin necesidad de registrarte.
- Perfil editable con tipo de necesidad, ayudas requeridas, mascota y contacto de emergencia.

**Ubicación y mapa**
- Detección de ubicación por GPS del navegador, con validación de que el punto esté dentro del territorio colombiano.
- Mapa interactivo con la ubicación del usuario y conductores cercanos generados alrededor de ese punto.
- Búsqueda de direcciones con autocompletado, o selección del destino tocando directamente el mapa.

**Solicitud de viaje**
- Cálculo de ruta por calles reales entre el punto de recogida y el destino, con tarifa estimada según distancia.
- Recomendación de conductor según compatibilidad: se prioriza a quien mejor cubre las necesidades declaradas en el perfil (rampa/elevador, espacio, apoyo visual o auditivo, ayuda al abordar, mascota), junto con cercanía y calificación.
- Aviso claro cuando el cálculo de ruta usa una estimación en línea recta por no haber conexión con el servicio de rutas.

**Seguimiento del viaje**
- Simulación del conductor en dos tramos: primero la ruta hacia el punto de recogida, luego la ruta hacia el destino, con el vehículo desplazándose sobre el trazado real.
- La línea de ruta se va acortando a medida que el conductor avanza, para dar sensación de progreso.
- Indicadores de tiempo restante, distancia restante y tarifa, con barra de progreso del viaje.
- Botón de emergencia (SOS) y acceso directo para llamar al contacto de confianza.

**Historial y accesibilidad**
- Historial de viajes realizados, guardado en la cuenta del usuario.
- Modo oscuro y modo de alto contraste, ajustables en cualquier momento y guardados como preferencia del usuario.
- Interfaz pensada para lectores de pantalla: anuncios en vivo, foco visible por teclado y áreas táctiles amplias.

## Tecnologías propias

- HTML, CSS y JavaScript sin frameworks (vanilla JS), en un único archivo.
- Tipografías [Manrope](https://fonts.google.com/specimen/Manrope) y [Atkinson Hyperlegible](https://fonts.google.com/specimen/Atkinson+Hyperlegible) vía Google Fonts, esta última diseñada por el Braille Institute para mejorar la legibilidad.

## Créditos y servicios de terceros

Este proyecto no sería posible sin las siguientes herramientas, librerías y servicios gratuitos/de código abierto:

| Servicio | Uso en el proyecto | Enlace |
|---|---|---|
| **Firebase (Authentication y Cloud Firestore)** | Registro e inicio de sesión de usuarios, y almacenamiento del perfil, historial de viajes y alertas de emergencia. | [firebase.google.com](https://firebase.google.com/) |
| **Leaflet** | Librería de mapas interactivos usada en la pantalla principal y en el seguimiento del viaje. | [leafletjs.com](https://leafletjs.com/) |
| **OpenStreetMap** | Mapas base (teselas) mostrados en la aplicación. © colaboradores de OpenStreetMap, datos bajo licencia [ODbL](https://www.openstreetmap.org/copyright). | [openstreetmap.org](https://www.openstreetmap.org/) |
| **Nominatim (OpenStreetMap)** | Geocodificación: convierte direcciones escritas en coordenadas y viceversa, y alimenta el autocompletado de direcciones. | [nominatim.org](https://nominatim.org/) |
| **OSRM (Open Source Routing Machine)** | Cálculo de rutas reales por calles entre dos puntos, usando el servidor de demostración público del proyecto. | [project-osrm.org](https://project-osrm.org/) |
| **Blobatar** | Generación de avatares automáticos para usuarios y conductores que no tienen foto de perfil propia. | [blobatar.dev](https://blobatar.dev/) |
| **Google Fonts** | Alojamiento de las tipografías Manrope y Atkinson Hyperlegible. | [fonts.google.com](https://fonts.google.com/) |
| **cdnjs (Cloudflare)** | Distribución (CDN) de la librería Leaflet. | [cdnjs.com](https://cdnjs.com/) |

Todos los nombres, marcas y logotipos mencionados pertenecen a sus respectivos titulares y se usan únicamente con fines de atribución técnica, no de afiliación o patrocinio.

Los conductores, vehículos y viajes que aparecen en la aplicación son **datos simulados** generados por el propio código, no información real de ninguna persona ni empresa.

## Aviso sobre el uso de inteligencia artificial

Parte del código de este proyecto (incluyendo la integración con Firebase, ajustes de lógica y este mismo README) fue generado o asistido con herramientas de inteligencia artificial (Claude, de Anthropic), bajo supervisión y revisión del autor del proyecto. El diseño de la interfaz, la lógica de negocio y las decisiones de producto fueron dirigidas por el autor; la IA se usó como herramienta de apoyo para la escritura y depuración de código, no como autora independiente del proyecto.

Se recomienda revisar y probar el código antes de usarlo en un entorno de producción real, especialmente en lo referente a seguridad (reglas de Firestore), manejo de datos personales y sensibles (información de salud/discapacidad), y cumplimiento normativo aplicable a aplicaciones de transporte y datos de usuarios en Colombia.

## Configuración y despliegue

1. Clona este repositorio.
2. Si vas a usar tu propio proyecto de Firebase, reemplaza el objeto `firebaseConfig` dentro de `index.html` con tus propias credenciales.
3. En la consola de Firebase, activa **Authentication → Sign-in method → Correo electrónico/contraseña**.
4. En **Authentication → Settings → Authorized domains**, agrega el dominio donde publicarás la app (por ejemplo `tuusuario.github.io`).
5. Configura las reglas de seguridad de **Firestore** para que cada usuario solo pueda leer y escribir sus propios datos.
6. Publica el archivo `index.html` con GitHub Pages (Settings → Pages → selecciona la rama y carpeta correspondientes).

## Limitaciones conocidas

- No procesa pagos reales; las tarifas son solo estimaciones.
- Los conductores y sus ubicaciones son generados aleatoriamente alrededor del usuario, no son conductores reales.
- El botón de emergencia es una simulación: no contacta a líneas de emergencia reales.
- Depende de servicios públicos gratuitos (Nominatim, OSRM) que pueden tener límites de uso; si no responden, la app recurre a una estimación en línea recta.
