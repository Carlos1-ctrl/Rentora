Readme · MD
Casas en Renta

Figma:https://www.figma.com/design/N7y8fdyioaiZ2sBEccnEeP/Sin-t%C3%ADtulo?node-id=1-2&t=35LaV0nk0EDfyfyZ-1

Plataforma web y móvil para publicar y encontrar inmuebles en renta en Torreón, Coahuila, con mecanismos de verificación, reseñas y reportes para reducir el riesgo de fraude.

Estado: anteproyecto (documento fechado el 04-10-2026). Proyecto de la materia Formulación de Proyectos de Tecnología. Docente: Jesús Del Toro Robledo.

Problema

En México, una persona adulta recibe en promedio 86 intentos de estafa al año y las pérdidas por engaños superan los 139 mil millones de pesos (Rodrigo Riquelme, El Economista). En Torreón, quien busca rentar suele recurrir a redes sociales o a recorrer zonas personalmente, con riesgo de fraude y pérdida de tiempo y dinero.

Objetivo

Implementar una solución tecnológica que medie entre quienes buscan rentar un inmueble y quienes lo ofrecen, con mecanismos que mejoren la fiabilidad y reduzcan las estafas.

Objetivos específicos
Búsqueda de inmuebles en Torreón desde web (Chrome, Firefox, Safari y navegadores Chromium) y desde una app Android 8.1 o superior.
Verificación de cuentas.
Comentarios y calificación por estrellas, que influye en la prioridad de cada publicación.
Reporte de cuentas con publicidad engañosa o fraude.
Filtros por ubicación, calificación, precio, restricciones, tamaño, entre otros.
Búsqueda inteligente con IA mediante consultas en lenguaje natural.
Alcance

Incluye: registro de usuarios, publicación de inmuebles, comentarios, reseñas, reportes de cuentas fraudulentas, filtros y búsqueda con IA (que complementa los filtros, no los sustituye).

No incluye:

Venta de inmuebles.
Pasarela de pagos.
Otras ciudades o estados.
Notificaciones (en esta primera versión).
Garantizar la fiabilidad de las publicaciones, inspecciones físicas ni validación legal de la propiedad.
Actuar como intermediario legal ante fraudes.
Cumplimiento total de la NOM-247-SE-2021.
MVP

Registro e inicio de sesión, publicación y consulta de inmuebles, búsqueda con filtros básicos, detalle del inmueble, comunicación entre usuarios y mecanismos básicos de verificación, comentarios, calificaciones y reportes.

Roles
Rol	Descripción
Administrador	Acceso, consulta, creación, modificación y eliminación de recursos administrativos. Revisa verificaciones y reportes.
Usuario	Publica inmuebles en renta, consulta propiedades, solicita información, comenta, califica y responde solicitudes sobre sus publicaciones.
Requerimientos funcionales (67)
Módulo	Prefijo	Cantidad
Autenticación y autorización	RF-AUTH	15
Gestión de cuenta de usuario	RF-GC	13
Publicación de inmuebles	RF-PI	10
Comentarios y calificaciones	RF-CCP	6
Reportes de publicaciones, comentarios y cuentas	RF-RPCC	14
Integración de la inteligencia artificial	RF-IA	9
Aspectos destacados
Sesión: registro manual o con Google; token de corta duración (≈15 min) en cabeceras y token de larga duración en cookie cifrada httpOnly, almacenado cifrado y revocable.
Verificación de cuenta: datos, archivos y selfie sosteniendo la INE; un administrador compara y acepta o rechaza con motivo.
Publicaciones: fotos y videos, mapa interactivo, estados (disponible, rentada o pausada) y favoritos.
Reportes: sobre publicaciones, comentarios y cuentas; sin duplicados; el administrador puede ocultar contenido o bloquear cuentas.
Agente de IA: consulta y recomienda inmuebles en lenguaje natural, resume comentarios, enlaza cada publicación, mantiene el contexto de la conversación, rechaza temas ajenos al sistema y no revela información privada.
Requerimientos no funcionales
Categoría	Resumen
Fiabilidad	Disponibilidad de 99.4% mensual, respaldos periódicos y recuperación de datos.
Portabilidad	Compatibilidad con navegadores y Android 8.1+, diseño responsivo, misma API para web y móvil, fechas en UTC y montos en pesos mexicanos.
Rendimiento	Respuesta en máximo 3 s, paginación, archivos multimedia en R2 y soporte para 100 usuarios simultáneos.
Privacidad	Protección de datos personales y de los documentos de verificación; sin contraseñas ni tokens en logs.
Seguridad	HTTPS, contraseñas de 8+ caracteres, validación de archivos, secretos en variables de entorno, límite de intentos fallidos y cookies httpOnly.
Tecnologías
Componente	Tecnología
App móvil	Android con Kotlin y Jetpack Compose
Frontend web	Vue
Backend	Laravel
Base de datos	MySQL
Archivos multimedia	R2
Metodología

Se usa Scrum, con sprints cortos, porque los requerimientos pueden ajustarse durante el desarrollo.

Riesgos principales
Riesgo	Valor	Nivel	Mitigación
Falta de comunicación del equipo	25	Crítico	Juntas diarias
Falta de análisis de requerimientos	20	Crítico	Validarlos antes de desarrollar
Falta de liderazgo	15	Alto	Designar un responsable
Falta de tiempo	12	Alto	Cronograma por actividad
Falta de responsabilidad	12	Alto	Responsables y fechas de entrega
Falta de promoción del producto	12	Alto	Estrategias de difusión

El anteproyecto completo incluye 11 riesgos.

Limitaciones
Desarrollo en menos de cuatro meses y curva de aprendizaje de las tecnologías.
Sin presupuesto fijo para infraestructura; el costo del proveedor de IA es un factor a analizar.
La verificación de cuentas no garantiza identidad ni honestidad de los usuarios.
La búsqueda con IA y la verificación pueden depender de proveedores externos.
La calidad de los resultados depende de la información que publiquen los usuarios.
Equipo
Integrante	Rol
Carlos Santiago Hernández Zapata	Líder de Frontend y Backend
Alejandro Machado Puentes	Desarrollador Frontend
Mateo Martínez Espino	Desarrollador Frontend
Christian Adrian Macias Saucedo	Desarrollador Backend
Ximena Guadalupe Hernández Hernández	Desarrolladora Backend
