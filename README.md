#Rentora: Plataforma web y móvil para la renta de casas en Torreón

> Proyecto académico | Universidad Tecnológica de Torreón (UTT) | Torreón, Coahuila, México

**Estado del repositorio en este documento:** anteproyecto y documentación de diseño en proceso; implementación pendiente de comprobar. Este README es la base oficial pública del proyecto y se completa con evidencia real conforme el equipo avance.

Figma: https://www.figma.com/design/N7y8fdyioaiZ2sBEccnEeP/Rentora?node-id=0-1&t=KrqbS372XJWJE3BA-1
---

## Tabla de contenido

1. [Descripción general](#1-descripción-general)
2. [Planeación del proyecto](#2-planeación-del-proyecto)
3. [Funcionalidades por módulo](#3-funcionalidades-por-módulo)
4. [Requerimientos](#4-requerimientos)
5. [Tecnologías y arquitectura](#5-tecnologías-y-arquitectura)
6. [Diseño e interfaz](#6-diseño-e-interfaz)
7. [Diagramas del sistema](#7-diagramas-del-sistema)
8. [Modelo de datos y diccionario de datos](#8-modelo-de-datos-y-diccionario-de-datos)
9. [Agente de IA](#9-agente-de-ia)
10. [Seguridad](#10-seguridad)
11. [Flujo de trabajo con Git](#11-flujo-de-trabajo-con-git-propuesto)
12. [Estructura del repositorio](#12-estructura-del-repositorio-propuesta)
13. [Ejecución, módulos y pruebas](#13-ejecución-módulos-y-pruebas)
14. [Plan de trabajo](#14-plan-de-trabajo)
15. [Estado de cumplimiento y entregables](#15-estado-de-cumplimiento-y-entregables)
16. [Riesgos principales](#16-riesgos-principales)
17. [Equipo y organización](#17-equipo-y-organización)
18. [Glosario](#18-glosario)
19. [Fuente documental y uso responsable](#19-fuente-documental-y-uso-responsable)

---

## 1. Descripción general

Rentora propone una plataforma **web y móvil (Android)** para facilitar la renta de casas en Torreón. Los arrendadores publican sus inmuebles con fotos, precio, características y ubicación en un mapa; las personas interesadas buscan, filtran, comparan, guardan favoritos y contactan al arrendador.

Para mantener la confiabilidad del contenido, la plataforma incluye:

- Comentarios y calificaciones sobre las publicaciones.
- Un sistema de **reportes y moderación** a cargo de administradores.
- Un **agente de IA** de apoyo (consultas, recomendaciones y apoyo a la moderación) que escala a una persona cuando el caso lo requiere.

La plataforma se ofrece en dos clientes (web y Android) que consumen **una misma API**, de modo que las reglas y la información sean idénticas en ambos.

---

## 2. Planeación del proyecto

### Problemática

Buscar casa en renta suele depender de publicaciones dispersas en redes sociales, letreros y recomendaciones personales, con información incompleta, difícil de comparar y sin forma de verificar la confiabilidad del anuncio o del arrendador. Para el arrendador, además, no existe un canal centralizado donde dar a conocer su inmueble con fotos, ubicación y datos claros. *(Completar con la problemática del anteproyecto; si se citan estadísticas, agregar su fuente verificable.)*

### Objetivo general

Diseñar y desarrollar una plataforma web y móvil que centralice la publicación y búsqueda de casas en renta en Torreón, con ubicación en mapa, comentarios y calificaciones, y herramientas de reporte y moderación que mantengan la confiabilidad del contenido.

### Objetivos específicos

- Gestionar usuarios con dos roles (Usuario y Administrador), con autenticación y verificación de cuenta.
- Permitir a los arrendadores publicar, editar y dar de baja inmuebles con fotos y ubicación en mapa.
- Ofrecer a los interesados búsqueda, filtros, detalle del inmueble, favoritos y contacto con el arrendador.
- Permitir comentarios y calificaciones sobre las publicaciones.
- Permitir reportar contenido y que los administradores lo moderen con trazabilidad.
- Integrar un agente de IA de apoyo con escalamiento a una persona.
- Mantener la misma información y reglas en web y móvil mediante una API común.
- Documentar el sistema (casos de uso, diagramas y modelo de datos) antes de desarrollarlo.

### Alcance

**Incluye:** aplicación web, aplicación Android, API REST, base de datos relacional, panel de administración, mapas, correo de verificación y agente de IA.

### Exclusiones y límites

*(Ajustar según el anteproyecto.)*

- Sin pagos ni contratos de renta dentro de la plataforma.
- Sin versión iOS ni publicación en tiendas de aplicaciones.
- La calidad de la información depende de lo que capturen los arrendadores y de la moderación.
- Un reporte no confirma por sí mismo una falta: toda decisión final de moderación la toma una persona.
- El agente de IA es un apoyo; no sustituye al administrador ni toma decisiones definitivas.

### Roles y actores

| Actor | Funciones principales |
|-------|----------------------|
| **Usuario (interesado)** | Registrarse, iniciar sesión, buscar y filtrar casas, ver detalle, guardar favoritos, contactar, comentar, calificar y reportar |
| **Usuario (arrendador)** | Lo anterior, más publicar, editar, cambiar estado y eliminar sus inmuebles |
| **Administrador** | Gestionar usuarios, moderar publicaciones y comentarios, atender reportes y consultar estadísticas |
| **Agente de IA** | Responder consultas, recomendar casas, apoyar la moderación y escalar a un administrador |

### Metodología

Desarrollo incremental organizado en **tickets** redactados como historias de usuario (*Como / Quiero / Para que*), con criterios de aceptación (*Dado que / Cuando / Entonces*) y definición de terminado (DoD). El seguimiento se hace en **GitHub Projects**.

| Prefijo | Tipo de ticket |
|---------|----------------|
| `FG` | Figma: guía de estilo, wireframes y prototipos |
| `CU` | Casos de uso: diagrama y especificaciones |
| `BD` | Base de datos: MER, modelo relacional y script |
| `DG` | Diagramas: arquitectura, secuencia y clases |

Cada ticket solo se considera terminado cuando cumple su DoD y es aprobado por el líder del área.

---

## 3. Funcionalidades por módulo

### 3.1 Autenticación, cuenta y verificación (CU-03)

- Registro de usuario (nombre, correo, teléfono, contraseña y tipo de usuario).
- Inicio y cierre de sesión con tokens.
- Recuperación y restablecimiento de contraseña por correo.
- Consulta y edición de perfil; cambio de contraseña; eliminación de cuenta.
- Verificación de correo, de teléfono (si aplica) y de identidad del arrendador (si aplica).

### 3.2 Publicaciones (CU-04)

- Crear publicación con título, descripción, precio, tipo de inmueble, recámaras, baños, características, fotos y ubicación en mapa.
- Editar, eliminar o dar de baja una publicación.
- Cambiar estado (disponible / rentada).
- Consultar "Mis publicaciones".

### 3.3 Búsqueda y consulta

- Listado de casas con tarjetas (foto, precio, zona, recámaras y baños).
- Búsqueda por zona, colonia o dirección.
- Filtros por rango de precio, tipo de inmueble, recámaras, baños y características; orden por precio o fecha.
- Vista de lista y vista de mapa con pines.
- Detalle del inmueble con galería, características, ubicación y calificación.
- Favoritos y contacto con el arrendador.

### 3.4 Comentarios y calificaciones (CU-04)

- Agregar, editar y eliminar comentarios propios; respuesta del arrendador.
- Calificar una casa o arrendador (estrellas y reseña opcional); una sola calificación por usuario por casa.
- Consulta de la calificación promedio.

### 3.5 Reportes y moderación (CU-05)

- Reportar publicación, comentario o usuario indicando motivo y descripción.
- Consultar el estado de los reportes enviados.
- Panel del administrador para revisar, filtrar y resolver reportes.
- Aprobar, editar u ocultar contenido; advertir, suspender o bloquear usuarios.
- Notificar al usuario la decisión y registrar cada acción (quién, cuándo, qué y por qué).

### 3.6 Panel de administración

- Gestión de usuarios (consultar, bloquear, eliminar).
- Moderación de publicaciones y comentarios.
- Atención de reportes y consulta de estadísticas generales (opcional).

### 3.7 Agente de IA (CU-05)

Ver la sección [9. Agente de IA](#9-agente-de-ia).

---

## 4. Requerimientos

> Lista **propuesta** a partir de los casos de uso; debe validarse contra el anteproyecto y numerarse de forma definitiva.

### Requerimientos funcionales (RF)

| ID | Requerimiento |
|----|--------------|
| RF-01 | El sistema debe permitir el registro de usuarios con validación de datos |
| RF-02 | El sistema debe permitir iniciar y cerrar sesión mediante tokens |
| RF-03 | El sistema debe permitir recuperar y restablecer la contraseña por correo |
| RF-04 | El sistema debe verificar el correo electrónico de la cuenta |
| RF-05 | El sistema debe permitir consultar y editar el perfil |
| RF-06 | El arrendador debe poder publicar, editar y eliminar inmuebles con fotos y ubicación |
| RF-07 | El arrendador debe poder cambiar el estado de su inmueble (disponible / rentada) |
| RF-08 | El sistema debe permitir buscar y filtrar inmuebles |
| RF-09 | El sistema debe mostrar el listado en lista y en mapa |
| RF-10 | El sistema debe mostrar el detalle del inmueble con su ubicación |
| RF-11 | El usuario debe poder guardar inmuebles en favoritos |
| RF-12 | El usuario debe poder contactar al arrendador |
| RF-13 | El usuario debe poder comentar y calificar (una calificación por casa) |
| RF-14 | El usuario debe poder reportar publicaciones, comentarios y usuarios |
| RF-15 | El administrador debe poder moderar contenido y gestionar usuarios |
| RF-16 | El sistema debe registrar cada acción de moderación |
| RF-17 | El agente de IA debe responder consultas y recomendar casas |
| RF-18 | El agente de IA debe apoyar la detección de contenido inapropiado y escalar a un administrador |

### Requerimientos no funcionales (RNF)

| ID | Requerimiento |
|----|--------------|
| RNF-01 | Interfaz clara y consistente con la guía de estilo (FG-01) |
| RNF-02 | Diseño responsivo en web y adaptación de patrones en móvil |
| RNF-03 | Compatibilidad con navegadores modernos y con Android (versión mínima por definir) |
| RNF-04 | Comunicación por HTTPS y contraseñas almacenadas con hash |
| RNF-05 | Control de acceso por rol en cada endpoint |
| RNF-06 | Validación de datos en cliente y en servidor |
| RNF-07 | Integridad de datos mediante llaves y restricciones en la base de datos |
| RNF-08 | Tiempos de respuesta aceptables en búsqueda y carga de imágenes (meta por definir) |
| RNF-09 | Código modular y documentado, con control de versiones en Git |
| RNF-10 | Accesibilidad básica: contraste, foco visible y texto alternativo |
| RNF-11 | Privacidad de datos personales (aviso de privacidad por definir) |
| RNF-12 | Uso de herramientas gratuitas o de licencia académica cuando sea posible |

---

## 5. Tecnologías y arquitectura

| Capa | Tecnología |
|------|-----------|
| Frontend web | Vue |
| App móvil | Kotlin + Jetpack Compose (Android) |
| Backend / API | Laravel (REST) |
| Base de datos | MySQL 8 |
| Almacenamiento de archivos | R2 (la BD solo guarda las llaves `*_key`) |
| Mapas | Por definir (se documenta en DG-01) |
| Correo | Por definir (se documenta en DG-01) |
| Agente de IA | Por definir (se documenta en DG-01) |
| Diseño | Figma |
| Control de versiones | Git / GitHub |
| Gestión de tareas | GitHub Projects |

### Arquitectura prevista

```
Cliente web (Vue)    ─┐
                      ├─► API REST (Laravel) ─► MySQL
App Android (Kotlin) ─┘          │
                                 ├─► Almacenamiento de imágenes
                                 ├─► Proveedor de correo
                                 ├─► Proveedor de mapas
                                 └─► Proveedor de IA
```

### Capas del backend

| Capa | Responsabilidad |
|------|----------------|
| Controladores / rutas | Reciben las peticiones HTTP y devuelven JSON |
| Servicios (lógica de negocio) | Aplican las reglas definidas en los casos de uso |
| Repositorios / modelos (Eloquent) | Acceso a la base de datos |
| Autenticación y autorización | Tokens y validación de rol (Usuario / Administrador) |

### Patrones de diseño

- **Singleton:** para componentes con una sola instancia (por ejemplo, configuración general o cliente del proveedor de correo).
- **Builder:** para construir objetos con muchos atributos opcionales (por ejemplo, la publicación de una casa).

*(Verificar que coincida con DG-01 y DG-02 terminados.)*

### API REST (propuesta de recursos)

| Recurso | Operaciones principales |
|---------|------------------------|
| `/auth` | registro, login, logout, refresh, recuperar y restablecer contraseña, verificar correo |
| `/usuarios` | perfil, edición, cambio de contraseña, eliminación |
| `/casas` | listar y filtrar, detalle, crear, editar, eliminar, cambiar estado |
| `/casas/{id}/fotos` | agregar, ordenar, eliminar |
| `/favoritos` | listar, agregar, quitar |
| `/casas/{id}/comentarios` | listar, crear, editar, eliminar |
| `/casas/{id}/calificaciones` | crear, editar, promedio |
| `/reportes` | crear, consultar propios; listar y resolver (administrador) |
| `/admin` | usuarios, moderación, estadísticas |
| `/agente` | consulta y recomendación |

*(Los endpoints definitivos se documentarán con la API implementada.)*

---

## 6. Diseño e interfaz

Herramienta: **Figma**. El diseño parte de una guía de estilo (colores, tipografía, iconos y componentes base) y de wireframes de baja fidelidad web y móvil, seguidos de prototipos navegables.

### Principios aplicados

- HTML semántico en web (`header`, `nav`, `main`, `section`, `footer`) y formularios con `label` asociado.
- Accesibilidad como referencia: contraste mínimo 4.5:1, navegación por teclado, foco visible y texto alternativo en imágenes e iconos.
- Diseño responsivo en web y adaptación de patrones en móvil (menú inferior, filtros en hoja inferior, mapa a pantalla completa).
- Estados de carga, error, éxito y "sin resultados" en cada flujo.
- Uso exclusivo de colores, estilos tipográficos e iconos definidos en la guía (sin valores sueltos en las pantallas).

### Paleta de colores

*(Pendiente: completar con los colores definidos en FG-01.)*

| Uso | Color | Hex |
|-----|-------|-----|
| Primario | — | — |
| Secundario | — | — |
| Fondo | — | — |
| Texto | — | — |
| Éxito | — | — |
| Error | — | — |
| Advertencia | — | — |

### Pantallas principales

Inicio de sesión y registro · Recuperar contraseña · Inicio / listado · Búsqueda y filtros · Vista de mapa · Detalle del inmueble · Publicar / editar inmueble · Favoritos · Perfil · Mis publicaciones · Panel de administración · Reportes y moderación.

### Prototipos y wireframes

*(Agregar el enlace de Figma.)*

| Ticket | Contenido |
|--------|-----------|
| FG-01 | Guía de estilo y componentes base (colores, tipografía, iconos) |
| FG-02 | Wireframes de baja fidelidad (web y móvil) |
| FG-03 | Prototipo: registro, login y recuperación de contraseña |
| FG-04 | Prototipo: publicar / editar inmueble con mapa |
| FG-05 | Prototipo: listado, filtros y detalle de inmueble con mapa |

> Los wireframes y prototipos no son evidencia de funcionamiento.

---

## 7. Diagramas del sistema

| Ticket | Entregable | Estado |
|--------|-----------|--------|
| CU-02 | Diagrama de casos de uso (Administrador y Usuario) | En proceso |
| CU-03 | Especificaciones: autenticación, cuenta y verificación | En proceso |
| CU-04 | Especificaciones: publicaciones, comentarios y calificaciones | En proceso |
| CU-05 | Especificaciones: reportes, moderación y agente de IA | En proceso |
| BD-01 | Modelo entidad-relación (MER) | En proceso |
| BD-02 | Modelo relacional, diccionario de datos e índices | En proceso |
| DG-01 | Diagrama de arquitectura cliente-servidor | En proceso |
| DG-02 | Diagramas de secuencia y de clases (login con tokens, verificación, publicación, Singleton y Builder) | En proceso |

*(Agregar aquí las imágenes o enlaces de cada diagrama conforme se terminen. El diagrama CU-02 debe incluir también al Agente de IA como actor y los casos de uso de comentarios y calificaciones.)*

---

## 8. Modelo de datos y diccionario de datos

Base de datos **MySQL 8** (`casas_en_renta`) del sistema web y móvil de renta de inmuebles en Torreón, Coahuila. Está organizada en 5 módulos y 21 tablas.

> **Notas generales**
>
> - Todos los `id` son `BIGINT UNSIGNED` autoincrementales, salvo donde se indica otro tipo.
> - Todas las fechas se guardan en **UTC**. `now` equivale a `CURRENT_TIMESTAMP`.
> - Los archivos viven en **R2** (almacenamiento de objetos) y la base de datos solo guarda su llave (`*_key`).
> - Nada se borra físicamente: se usa borrado lógico con `eliminado_en`.
> - Todas las llaves foráneas son `RESTRICT`.
> - Convención de la columna *Llave*: **PK** llave primaria, **FK→tabla.columna** llave foránea, **UQ** valor único.

### Módulos y tablas

| Módulo | Tablas |
|--------|--------|
| 1. Acceso y cuentas | `roles`, `usuarios`, `tokens_refresco`, `codigos_seguridad`, `solicitudes_verificacion`, `archivos_verificacion` |
| 2. Inmuebles | `tipos_inmueble`, `caracteristicas`, `publicaciones`, `publicacion_caracteristicas`, `multimedia_publicacion`, `favoritos` |
| 3. Interacción | `comentarios`, `calificaciones` |
| 4. Moderación | `motivos_reporte`, `reportes`, `historial_estado_reporte`, `acciones_moderacion` |
| 5. Agente de IA | `hilos_ia`, `mensajes_ia`, `mensajes_ia_publicaciones` |

### Relaciones principales

- Un rol tiene muchos usuarios; un usuario tiene muchos tokens de refresco, códigos de seguridad y solicitudes de verificación.
- Una solicitud de verificación tiene muchos archivos de verificación.
- Un usuario (arrendador) tiene muchas publicaciones; cada publicación tiene un tipo de inmueble, muchas multimedia y muchas características (N:M con `publicacion_caracteristicas`).
- Usuarios y publicaciones se relacionan N:M por `favoritos`; las calificaciones son una por usuario por publicación.
- Un comentario puede responder a otro comentario de la misma publicación (hilo).
- Un reporte apunta a una publicación, un comentario o una cuenta, tiene un motivo y un historial de cambios de estado; las acciones de moderación pueden derivar de un reporte o ser directas.
- Un usuario tiene muchos hilos con el agente de IA; un hilo tiene muchos mensajes, y un mensaje puede referenciar varias publicaciones (N:M).

---

### Módulo 1: Acceso y cuentas

#### `roles`

Catálogo de los roles del sistema (por ejemplo, usuario y administrador).

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | TINYINT | No | PK | — | Identificador del rol. |
| `clave` | VARCHAR(10) | No | UQ | — | Clave corta y única del rol (R-1, R-2). |
| `nombre` | VARCHAR(30) | No | UQ | — | Nombre del rol. |
| `descripcion` | VARCHAR(255) | Sí | — | — | Descripción de los permisos o alcance del rol. |

**Reglas / restricciones:** `clave` y `nombre` son únicos.

#### `usuarios`

Cuentas de todas las personas que usan la plataforma, con su rol, método de registro y estado de la cuenta.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del usuario. |
| `rol_id` | TINYINT | No | FK→roles.id | — | Rol asignado al usuario. |
| `nombre` | VARCHAR(100) | No | — | — | Nombre(s) del usuario. |
| `apellidos` | VARCHAR(150) | No | — | — | Apellidos del usuario. |
| `correo` | VARCHAR(190) | No | UQ | — | Correo electrónico. Es único: rechaza correos ya registrados de forma local o con Google (AUTH-15). |
| `password_hash` | VARCHAR(255) | Sí | — | — | Hash de la contraseña. Es `NULL` si el usuario se registró con Google. |
| `proveedor_auth` | ENUM('local','google') | No | — | `local` | Método con el que se registró la cuenta. |
| `google_id` | VARCHAR(64) | Sí | UQ | — | Identificador de la cuenta de Google, cuando el registro fue con Google. |
| `domicilio` | VARCHAR(255) | Sí | — | — | Domicilio del usuario. |
| `foto_perfil_key` | VARCHAR(255) | Sí | — | — | Llave del archivo de la foto de perfil en R2 (GC-1, GC-14). |
| `estado_cuenta` | ENUM('activa','inactiva','bloqueada') | No | — | `inactiva` | Estado de la cuenta. Pasa a `activa` al verificar el correo (CU-U03). Las cuentas `inactiva` y `bloqueada` no pueden iniciar sesión (AUTH-14). |
| `bloqueada_hasta` | DATETIME | Sí | — | — | Fin de la suspensión temporal (GC-16). Si la cuenta está `bloqueada` y el valor es `NULL`, el bloqueo es indefinido. |
| `verificada` | BOOL | No | — | `0` | Indica si un administrador verificó la cuenta (GC-9). |
| `correo_verificado_en` | DATETIME | Sí | — | — | Fecha y hora en que se verificó el correo. |
| `tos_aceptados_en` | DATETIME | Sí | — | — | Fecha de aceptación de los Términos de Servicio (AUTH-13). |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `actualizado_en` | DATETIME | No | — | `now` | Fecha de la última modificación; se actualiza automáticamente. |

**Reglas / restricciones:** si `proveedor_auth = 'local'`, `password_hash` es obligatorio; si es `'google'`, `google_id` es obligatorio; `bloqueada_hasta` solo puede tener valor si `estado_cuenta = 'bloqueada'`. `correo` y `google_id` son únicos.

#### `tokens_refresco`

Tokens de refresco de sesión de larga duración. Se guarda su hash, nunca el token en claro.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del token. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Usuario dueño de la sesión. |
| `token_hash` | CHAR(64) | No | UQ | — | Hash del token de refresco. |
| `ip` | VARCHAR(45) | Sí | — | — | Dirección IP desde la que se inició la sesión (IPv4 o IPv6). |
| `user_agent` | VARCHAR(255) | Sí | — | — | Navegador o dispositivo desde el que se inició la sesión. |
| `expira_en` | DATETIME | No | — | — | Fecha y hora de expiración del token. |
| `revocado_en` | DATETIME | Sí | — | — | Se llena al cerrar sesión o revocar el token (AUTH-11, SEG-6). |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |

**Reglas / restricciones:** `token_hash` es único; solo se almacena el hash del token.

#### `codigos_seguridad`

Códigos de un solo uso para verificar el correo y recuperar la contraseña.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del código. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Usuario al que pertenece el código. |
| `proposito` | ENUM('verificar_correo','recuperar_password') | No | — | — | Para qué se generó el código. |
| `codigo_hash` | VARCHAR(255) | No | — | — | Hash del código enviado al usuario. |
| `expira_en` | DATETIME | No | — | — | Fecha y hora de expiración del código. |
| `usado_en` | DATETIME | Sí | — | — | Fecha en que se usó el código; `NULL` si aún no se usa. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |

**Reglas / restricciones:** los códigos son de un solo uso; se guarda únicamente su hash.

#### `solicitudes_verificacion`

Solicitudes de los usuarios para que un administrador verifique su cuenta.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador de la solicitud. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Usuario que solicita la verificación. |
| `estado` | ENUM('en_proceso','rechazada','verificada') | No | — | `en_proceso` | Estado de la solicitud. |
| `datos_declarados` | JSON | Sí | — | — | Datos que captura el usuario (campos por definir). |
| `motivo_rechazo` | VARCHAR(500) | Sí | — | — | Motivo por el que se rechazó la solicitud. |
| `revisado_por` | BIGINT UNSIGNED | Sí | FK→usuarios.id | — | Administrador que resolvió la solicitud. |
| `revisado_en` | DATETIME | Sí | — | — | Fecha y hora de la resolución. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `actualizado_en` | DATETIME | No | — | `now` | Fecha de la última modificación; se actualiza automáticamente. |

**Reglas / restricciones:** un usuario solo puede tener una solicitud en estado `en_proceso` a la vez; si `estado = 'rechazada'`, `motivo_rechazo` es obligatorio.

#### `archivos_verificacion`

Documentos privados que el usuario adjunta a una solicitud de verificación.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del archivo. |
| `solicitud_id` | BIGINT UNSIGNED | No | FK→solicitudes_verificacion.id | — | Solicitud a la que pertenece el archivo. |
| `tipo` | ENUM('ine','selfie_con_ine','otro') | No | — | — | Tipo de documento. |
| `storage_key` | VARCHAR(255) | No | — | — | Llave del archivo en el bucket privado de R2. |
| `mime_type` | VARCHAR(100) | No | — | — | Tipo MIME del archivo. |
| `tamano_bytes` | INT | No | — | — | Tamaño del archivo en bytes. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |

**Reglas / restricciones:** los archivos se guardan en un bucket privado; la base de datos solo almacena su llave.

---

### Módulo 2: Inmuebles

#### `tipos_inmueble`

Catálogo de tipos de inmueble (por ejemplo, casa, departamento).

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | SMALLINT | No | PK | — | Identificador del tipo de inmueble. |
| `nombre` | VARCHAR(50) | No | UQ | — | Nombre del tipo de inmueble. |

**Reglas / restricciones:** `nombre` es único.

#### `caracteristicas`

Catálogo de características y restricciones que puede tener un inmueble.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | SMALLINT | No | PK | — | Identificador de la característica. |
| `nombre` | VARCHAR(80) | No | — | — | Nombre de la característica o restricción. |
| `tipo` | ENUM('caracteristica','restriccion') | No | — | `caracteristica` | Indica si es una característica del inmueble o una restricción. |

**Reglas / restricciones:** único por (`nombre`, `tipo`).

#### `publicaciones`

Anuncios de inmuebles en renta publicados por los arrendadores.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador de la publicación. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Propietario o arrendador que publica. |
| `tipo_inmueble_id` | SMALLINT | No | FK→tipos_inmueble.id | — | Tipo de inmueble. |
| `titulo` | VARCHAR(150) | No | — | — | Título del anuncio. |
| `descripcion` | TEXT | No | — | — | Descripción del inmueble. |
| `precio_renta` | DECIMAL(10,2) | No | — | — | Precio de la renta en MXN por mes. |
| `superficie_m2` | DECIMAL(8,2) | Sí | — | — | Superficie del inmueble en metros cuadrados. |
| `recamaras` | TINYINT | No | — | `0` | Número de recámaras. |
| `banos` | TINYINT | No | — | `0` | Número de baños. |
| `direccion` | VARCHAR(255) | Sí | — | — | Dirección del inmueble. |
| `colonia` | VARCHAR(120) | Sí | — | — | Colonia donde se ubica. |
| `codigo_postal` | CHAR(5) | Sí | — | — | Código postal. |
| `latitud` | DECIMAL(10,7) | Sí | — | — | Latitud para el mapa interactivo (PI-9, PI-10). |
| `longitud` | DECIMAL(10,7) | Sí | — | — | Longitud para el mapa interactivo. |
| `estado` | ENUM('disponible','rentado','pausado','oculto') | No | — | `disponible` | Estado de la publicación; lo controla el dueño (PI-11). |
| `oculta_por_moderacion` | BOOL | No | — | `0` | La oculta un administrador (RB-06); el dueño no puede revertirlo. |
| `calificacion_promedio` | DECIMAL(3,2) | No | — | `0.00` | Promedio de estrellas; se actualiza por trigger (CCP-6). |
| `total_calificaciones` | INT | No | — | `0` | Número de calificaciones recibidas; se actualiza por trigger. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `actualizado_en` | DATETIME | No | — | `now` | Fecha de la última modificación; se actualiza automáticamente. |
| `eliminado_en` | DATETIME | Sí | — | — | Borrado lógico (PI-3). |

**Reglas / restricciones:** `precio_renta > 0`; `latitud` y `longitud` van juntas (ambas o ninguna); índice `FULLTEXT` en (`titulo`, `descripcion`).

#### `publicacion_caracteristicas`

Tabla intermedia (N:M) que asigna características a las publicaciones.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `publicacion_id` | BIGINT UNSIGNED | No | PK, FK→publicaciones.id | — | Publicación a la que se asigna la característica. |
| `caracteristica_id` | SMALLINT | No | PK, FK→caracteristicas.id | — | Característica asignada. |

**Reglas / restricciones:** llave primaria compuesta (`publicacion_id`, `caracteristica_id`).

#### `multimedia_publicacion`

Fotos y videos de cada publicación.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del archivo multimedia. |
| `publicacion_id` | BIGINT UNSIGNED | No | FK→publicaciones.id | — | Publicación a la que pertenece. |
| `tipo` | ENUM('foto','video') | No | — | — | Tipo de archivo. |
| `storage_key` | VARCHAR(255) | No | — | — | Llave del archivo en R2 (REN-3). |
| `mime_type` | VARCHAR(100) | No | — | — | Tipo MIME del archivo. |
| `tamano_bytes` | INT | No | — | — | Tamaño del archivo en bytes. |
| `orden` | SMALLINT | No | — | `0` | Posición del archivo en la galería. |
| `es_portada` | BOOL | No | — | `0` | Indica si es la imagen de portada de la publicación. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `eliminado_en` | DATETIME | Sí | — | — | Borrado lógico. |

**Reglas / restricciones:** la base de datos solo guarda la llave del archivo (`storage_key`); el archivo vive en R2.

#### `favoritos`

Tabla intermedia (N:M) con las publicaciones que cada usuario guardó como favoritas.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `usuario_id` | BIGINT UNSIGNED | No | PK, FK→usuarios.id | — | Usuario que guarda el favorito. |
| `publicacion_id` | BIGINT UNSIGNED | No | PK, FK→publicaciones.id | — | Publicación guardada. |
| `creado_en` | DATETIME | No | — | `now` | Fecha en que se guardó como favorita. |

**Reglas / restricciones:** la llave primaria compuesta (`usuario_id`, `publicacion_id`) evita duplicados.

---

### Módulo 3: Interacción

#### `comentarios`

Comentarios públicos con respuestas en forma de hilo. Las preguntas al arrendador y sus respuestas también son comentarios.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del comentario. |
| `publicacion_id` | BIGINT UNSIGNED | No | FK→publicaciones.id | — | Publicación comentada. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Autor del comentario. |
| `comentario_padre_id` | BIGINT UNSIGNED | Sí | FK→comentarios.id | — | Comentario al que responde. `NULL` indica un comentario raíz. |
| `contenido` | TEXT | No | — | — | Texto del comentario. |
| `oculto_por_moderacion` | BOOL | No | — | `0` | Indica si un administrador ocultó el comentario. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `actualizado_en` | DATETIME | No | — | `now` | Fecha de la última modificación; se actualiza automáticamente. |
| `eliminado_en` | DATETIME | Sí | — | — | Borrado lógico. |

**Reglas / restricciones:** autorreferencia con FK compuesta (`comentario_padre_id`, `publicacion_id`), por lo que un comentario solo puede responder a otro de la misma publicación. El hilo se recorre con CTE recursivo.

#### `calificaciones`

Calificaciones en estrellas que los usuarios dan a las publicaciones.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador de la calificación. |
| `publicacion_id` | BIGINT UNSIGNED | No | FK→publicaciones.id | — | Publicación calificada. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Usuario que califica. |
| `estrellas` | TINYINT | No | — | — | Calificación de 1 a 5 estrellas. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `actualizado_en` | DATETIME | No | — | `now` | Fecha de la última modificación; se actualiza automáticamente. |

**Reglas / restricciones:** `estrellas` entre 1 y 5; único por (`publicacion_id`, `usuario_id`): una calificación por usuario y, si ya existe, se actualiza. Un trigger recalcula `calificacion_promedio` y `total_calificaciones` en `publicaciones` al insertar o actualizar.

---

### Módulo 4: Moderación

#### `motivos_reporte`

Catálogo de motivos por los que se puede reportar contenido o cuentas.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | SMALLINT | No | PK | — | Identificador del motivo. |
| `nombre` | VARCHAR(80) | No | UQ | — | Nombre del motivo. |
| `descripcion` | VARCHAR(255) | Sí | — | — | Descripción del motivo. |
| `activo` | BOOL | No | — | `1` | Indica si el motivo está disponible para elegirse. |

**Reglas / restricciones:** `nombre` es único.

#### `reportes`

Reportes de los usuarios sobre publicaciones, comentarios o cuentas.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del reporte. |
| `reportante_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Usuario que envía el reporte. |
| `tipo_objeto` | ENUM('publicacion','comentario','cuenta') | No | — | — | Tipo de objeto reportado. |
| `publicacion_id` | BIGINT UNSIGNED | Sí | FK→publicaciones.id | — | Publicación reportada. |
| `comentario_id` | BIGINT UNSIGNED | Sí | FK→comentarios.id | — | Comentario reportado. |
| `usuario_reportado_id` | BIGINT UNSIGNED | Sí | FK→usuarios.id | — | Cuenta reportada. Solo se llena cuando el objeto es una cuenta; para publicación o comentario, el reportado se obtiene del autor. |
| `motivo_id` | SMALLINT | No | FK→motivos_reporte.id | — | Motivo del reporte. |
| `descripcion` | VARCHAR(1000) | Sí | — | — | Detalle adicional que escribe el reportante. |
| `estado` | ENUM('no_analizado','en_progreso','aceptado','rechazado') | No | — | `no_analizado` | Estado de atención del reporte. |
| `revisado_por` | BIGINT UNSIGNED | Sí | FK→usuarios.id | — | Administrador que revisó el reporte. |
| `resuelto_en` | DATETIME | Sí | — | — | Fecha y hora en que se resolvió. |
| `creado_en` | DATETIME | No | — | `now` | Fecha de creación del registro. |
| `actualizado_en` | DATETIME | No | — | `now` | Fecha de la última modificación; se actualiza automáticamente. |

**Reglas / restricciones:** cada reporte apunta a exactamente **uno** de `publicacion_id`, `comentario_id` o `usuario_reportado_id`, según `tipo_objeto`; un usuario no puede reportar dos veces el mismo objeto (únicos por (`reportante_id`, `publicacion_id`), (`reportante_id`, `comentario_id`) y (`reportante_id`, `usuario_reportado_id`)); no se puede reportar a uno mismo.

#### `historial_estado_reporte`

Bitácora de los cambios de estado de un reporte.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del registro de historial. |
| `reporte_id` | BIGINT UNSIGNED | No | FK→reportes.id | — | Reporte al que pertenece el cambio. |
| `admin_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Administrador que hizo el cambio. |
| `estado_anterior` | ENUM('no_analizado','en_progreso','aceptado','rechazado') | No | — | — | Estado antes del cambio. |
| `estado_nuevo` | ENUM('no_analizado','en_progreso','aceptado','rechazado') | No | — | — | Estado después del cambio. |
| `nota` | VARCHAR(500) | Sí | — | — | Nota del administrador sobre el cambio. |
| `creado_en` | DATETIME | No | — | `now` | Fecha del cambio. |

**Reglas / restricciones:** cada cambio de estado de un reporte queda registrado con el administrador que lo hizo.

#### `acciones_moderacion`

Acciones del administrador, derivadas de un reporte o directas. El agente de IA nunca escribe en esta tabla.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador de la acción. |
| `admin_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Administrador que ejecuta la acción. |
| `reporte_id` | BIGINT UNSIGNED | Sí | FK→reportes.id | — | Reporte que originó la acción; `NULL` si la acción no viene de un reporte. |
| `tipo_objeto` | ENUM('publicacion','comentario','cuenta') | No | — | — | Tipo de objeto sobre el que se actúa. |
| `publicacion_id` | BIGINT UNSIGNED | Sí | FK→publicaciones.id | — | Publicación afectada. |
| `comentario_id` | BIGINT UNSIGNED | Sí | FK→comentarios.id | — | Comentario afectado. |
| `usuario_objetivo_id` | BIGINT UNSIGNED | Sí | FK→usuarios.id | — | Cuenta afectada. |
| `accion` | ENUM('ocultar','restaurar','eliminar','bloquear','suspender','activar','inactivar') | No | — | — | Acción realizada. |
| `motivo` | VARCHAR(500) | Sí | — | — | Justificación de la acción. |
| `vigente_hasta` | DATETIME | Sí | — | — | Fin de la suspensión temporal (cuando `accion = 'suspender'`). |
| `creado_en` | DATETIME | No | — | `now` | Fecha de la acción. |

**Reglas / restricciones:** apunta a exactamente **uno** de `publicacion_id`, `comentario_id` o `usuario_objetivo_id`, según `tipo_objeto`.

---

### Módulo 5: Agente de IA

#### `hilos_ia`

Un hilo por sesión del usuario con el agente. Se crea con el primer mensaje y se cierra al salir de la app o la página.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del hilo. |
| `usuario_id` | BIGINT UNSIGNED | No | FK→usuarios.id | — | Usuario que conversa con el agente. |
| `iniciado_en` | DATETIME | No | — | `now` | Fecha y hora de inicio de la sesión. |
| `finalizado_en` | DATETIME | Sí | — | — | Fecha y hora de cierre de la sesión; `NULL` mientras siga abierta. |

**Reglas / restricciones:** el hilo se crea con el primer mensaje y se cierra al salir de la app o de la página.

#### `mensajes_ia`

Mensajes intercambiados entre el usuario y el agente dentro de un hilo.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `id` | BIGINT UNSIGNED | No | PK | AUTO_INCREMENT | Identificador del mensaje. |
| `hilo_id` | BIGINT UNSIGNED | No | FK→hilos_ia.id | — | Hilo al que pertenece el mensaje. |
| `emisor` | ENUM('usuario','agente') | No | — | — | Quién envió el mensaje. |
| `tipo` | ENUM('texto','recomendacion','resumen_comentarios','guia','sin_resultados','fuera_de_alcance') | No | — | `texto` | Tipo de mensaje o de respuesta del agente. |
| `contenido` | TEXT | No | — | — | Contenido del mensaje. |
| `creado_en` | DATETIME | No | — | `now` | Fecha y hora del mensaje. |

**Reglas / restricciones:** cada mensaje pertenece a un único hilo.

#### `mensajes_ia_publicaciones`

Tabla intermedia (N:M) con las publicaciones que el agente referenció, con enlace, en una respuesta.

| Campo | Tipo | Nulable | Llave | Valor por defecto | Descripción |
|-------|------|---------|-------|-------------------|-------------|
| `mensaje_id` | BIGINT UNSIGNED | No | PK, FK→mensajes_ia.id | — | Mensaje del agente que hace la referencia. |
| `publicacion_id` | BIGINT UNSIGNED | No | PK, FK→publicaciones.id | — | Publicación referenciada. |

**Reglas / restricciones:** llave primaria compuesta (`mensaje_id`, `publicacion_id`).

---

## 9. Agente de IA

El agente de IA es un actor del sistema con alcance acotado.

| Función | Descripción | Nivel de autonomía |
|---------|-------------|--------------------|
| Responder consultas | Dudas sobre la plataforma o búsqueda de casas en lenguaje natural | Responde por sí mismo |
| Recomendar casas | Sugiere inmuebles según las preferencias del usuario | Responde por sí mismo |
| Apoyar la moderación | Detecta contenido inapropiado, spam o publicaciones sospechosas | Solo sugiere; decide un administrador |
| Escalar | Pasa el caso a un administrador cuando no puede resolverlo o es delicado | Obligatorio |

**Reglas:**

- Toda acción del agente queda registrada (quién, cuándo, qué y por qué) y es consultable por el administrador.
- El agente no elimina ni bloquea contenido o usuarios por sí solo.
- Se debe contemplar el falso positivo en la detección automática y la posibilidad de apelar.

*(Ajustar al alcance real definido en el anteproyecto.)*

---

## 10. Seguridad

1. El usuario envía sus credenciales por HTTPS.
2. La API valida contra la base de datos (contraseña con hash).
3. La API genera un token (access y refresh) que incluye el rol.
4. El cliente guarda el token de forma segura y lo envía en cada petición.
5. Un middleware valida el token y los permisos por rol antes de ejecutar cada acción.

**Controles adicionales:**

- Validación de datos en el servidor aunque ya se validen en el cliente.
- Límite de tamaño y tipo de archivo en la carga de fotos.
- Protección contra intentos fallidos repetidos de inicio de sesión.
- Credenciales y claves de terceros solo en variables de entorno (`.env`), nunca en el repositorio.
- Un archivo `.gitignore` que excluya `.env`, dependencias y archivos locales.

---

## 11. Flujo de trabajo con Git (propuesto)

> Propuesta base; debe acordarse con todo el equipo antes de oficializarla.

### Justificación de la herramienta y plataforma de versionamiento

**Git** se eligió como sistema de control de versiones porque el proyecto tiene varias áreas (back, front y móvil) que trabajan en paralelo sobre el mismo código y necesitan ramas baratas, historial completo y fusiones controladas. Al ser distribuido, cada integrante trabaja con una copia local completa y el historial no depende de un único servidor.

**GitHub** se eligió como plataforma porque:

- Integra **Pull Requests** con revisión obligatoria y ramas protegidas, que son la base del flujo de trabajo propuesto.
- Incluye **GitHub Projects**, donde ya se gestionan los tickets (FG, CU, BD, DG), y permite enlazar commits y PR con cada ticket.
- Permite gestionar accesos por persona y rol dentro del repositorio.
- Es de uso gratuito para repositorios académicos y ampliamente usado en la industria, lo que facilita el aprendizaje y la evidencia del trabajo colaborativo.

### Configuración y parámetros del entorno de versiones

| Elemento | Configuración |
|----------|--------------|
| Identidad de Git | `git config user.name` y `git config user.email` con el usuario y correo asociados a GitHub |
| Rama por defecto | `main`, con `dev` como rama de integración |
| Ramas protegidas | `main` y `dev`: PR obligatorio, al menos una aprobación y sin push directo |
| Control de accesos | Colaboradores invitados con el rol mínimo necesario (Write para quien hace commits y PR); administración del repositorio solo para quien la requiera |
| Credenciales | Autenticación por llave SSH o token personal de GitHub; nunca contraseñas ni claves dentro del repositorio |
| Secretos | Variables en `.env` (excluido del repositorio) y `.env.example` sin valores reales |
| Archivos de exclusión | `.gitignore` con `.env`, dependencias (`vendor/`, `node_modules/`), compilados (`build/`, `.gradle/`), archivos de IDE y del sistema |

Ejemplo base de `.gitignore`:

```gitignore
# Secretos y entorno
.env
*.keystore
local.properties

# Dependencias
vendor/
node_modules/

# Compilados
build/
.gradle/
dist/

# IDE y sistema
.idea/
.vscode/
.DS_Store
Thumbs.db
```

### Ramas

```
main  (producción, protegida; solo mediante PR aprobado)
  ↑
dev   (integración, protegida)
  ↑
feature/FG-03-prototipo-login   (ramas de trabajo)
```

### Nomenclatura de ramas

```
tipo/ID-descripcion-corta
```

Ejemplos: `feature/FG-03-prototipo-login`, `docs/CU-03-especificaciones-autenticacion`, `fix/BD-02-indice-favoritos`.

### Formato de commits

```
Título descriptivo | ID-DEL-TICKET

Qué: qué cambios se realizaron.
Cómo: cómo se implementó.
Por qué: motivo del cambio.
```

### Pasos

```bash
git checkout dev && git pull origin dev
git checkout -b feature/FG-03-prototipo-login
# ...cambios...
git add <archivos>
git commit -m "Agregar prototipo de login | FG-03"
git push -u origin feature/FG-03-prototipo-login
# abrir Pull Request hacia dev y pedir revisión
```

### Políticas de colaboración

- Todo cambio entra por Pull Request con al menos una aprobación.
- Prohibido el push directo a `main` y `dev`.
- No aprobar los PR propios.
- No subir archivos `.env`, credenciales ni archivos locales del sistema.
- No usar `git add .` sin revisar qué archivos se agregan.
- Cada tarea debe tener su ticket y la rama debe llevar su ID.

### Estados del ticket en GitHub Projects

`Backlog` → `Por hacer` → `En progreso` → `En revisión` → `Terminado`

---

## 12. Estructura del repositorio (propuesta)

> Ajustar a la estructura real del repositorio.

```
Rentora/
├── backend/          # API Laravel
├── web/              # Cliente web (Vue)
├── android/          # App Android (Kotlin + Jetpack Compose)
├── docs/             # Casos de uso, diagramas, MER y diccionario de datos
├── design/           # Exportaciones y referencias de Figma
├── .gitignore
└── README.md
```

---

## 13. Ejecución, módulos y pruebas

> Todo lo de esta sección está **PENDIENTE de verificar** contra el repositorio real. Los comandos son los habituales del stack y deben comprobarse antes de oficializarlos.

**Requisitos previos:** PHP, Composer, Node.js, MySQL y Android Studio *(versiones por confirmar)*.

### Backend (Laravel)

```bash
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
```

### Frontend web (Vue)

```bash
npm install
npm run dev
```

### App Android (Kotlin + Jetpack Compose)

Abrir el proyecto en Android Studio, sincronizar Gradle y ejecutar en emulador o dispositivo.

### Variables de entorno

| Variable | Descripción |
|----------|-------------|
| `DB_*` | Conexión a MySQL |
| `MAIL_*` | Proveedor de correo |
| `MAPS_API_KEY` | Clave del proveedor de mapas (si aplica) |
| `AI_API_KEY` | Clave del proveedor de IA |

*(Entregar un `.env.example` sin valores reales.)*

### Estado de la verificación

| Elemento | Estado |
|----------|--------|
| Arquitectura implementada, API y BD | PENDIENTE |
| Instalación local y `.env.example` | PENDIENTE |
| Pruebas ejecutadas | NO VERIFICADO |
| Despliegue | NO VERIFICADO |
| Historial de incidencias y aprendizajes | PENDIENTE |

---

## 14. Plan de trabajo

Cronograma aproximado de **mes y medio**, sin considerar días inhábiles, organizado por fases. *(Las fechas exactas están en el cronograma de Excel del equipo.)*

| Fase | Contenido | Tickets |
|------|-----------|---------|
| 1. Diseño | Guía de estilo, wireframes y prototipos en Figma | FG-01 a FG-05 |
| 2. Análisis y diagramas | Casos de uso, arquitectura, secuencia y clases | CU-02 a CU-05, DG-01, DG-02 |
| 3. Base de datos | MER, modelo relacional, diccionario, índices y script | BD-01, BD-02 |
| 4. Backend | API REST, autenticación, módulos y panel de administración | *(por definir)* |
| 5. Frontend web | Pantallas y consumo de la API | *(por definir)* |
| 6. Móvil | App Android y consumo de la API | *(por definir)* |
| 7. Integración y pruebas | Pruebas, correcciones y documentación final | *(por definir)* |

---

## 15. Estado de cumplimiento y entregables

| Elemento | Estado hoy |
|----------|-----------|
| Anteproyecto | Disponible (16-09-2026) |
| Cronograma | Elaborado |
| Guía de estilo, wireframes y prototipos (Figma) | En proceso |
| Casos de uso y diagramas | En proceso |
| Modelo de datos (MER / relacional) | En proceso |
| Backend | No iniciado / no verificado |
| Frontend web | No iniciado / no verificado |
| App Android | No iniciada / no verificada |
| Pruebas automatizadas | No verificadas |
| Despliegue | No verificado |

---

## 16. Riesgos principales

| Riesgo | Mitigación |
|--------|-----------|
| Falta de coordinación entre back, front y móvil | Documentación previa y API común; revisiones por PR |
| Cambios en los requisitos | Tickets con criterios de aceptación y aprobación del líder |
| Inconsistencias entre web y móvil | Una sola API y una guía de estilo compartida |
| Conflictos en Git e integración | Ramas protegidas, ramas por ticket y PR obligatorios |
| Fallas o límites de servicios de terceros (mapas, correo, IA) | Definir proveedores en DG-01 y manejar errores en la API |
| Contenido falso o inapropiado en publicaciones | Reportes, moderación humana y trazabilidad |
| Respuestas incorrectas del agente de IA | Alcance acotado, registro de interacciones y escalamiento a una persona |

---

## 17. Equipo y organización

Proyecto realizado por el equipo de Rentora, Universidad Tecnológica de Torreón. El trabajo se organiza por áreas, cada una con su líder:

| Área | Responsabilidad |
|------|----------------|
| Back y Front | API Laravel, base de datos y cliente web en Vue |
| Móvil | App Android en Kotlin + Jetpack Compose |

---

## 18. Glosario

| Término | Significado |
|---------|------------|
| Arrendador | Persona que publica una casa para rentarla |
| Arrendatario / interesado | Persona que busca casa en renta |
| Wireframe | Boceto de baja fidelidad de una pantalla |
| Prototipo | Maqueta navegable de un flujo, sin funcionamiento real |
| MER | Modelo entidad-relación de la base de datos |
| Caso de uso | Descripción de lo que un actor hace con el sistema |
| DoD | Definición de terminado de un ticket |
| API REST | Interfaz por la que los clientes consumen los datos del backend |
| Token | Credencial temporal que identifica al usuario en cada petición |
| Moderación | Revisión de contenido reportado para aprobarlo, editarlo u ocultarlo |

---

## 19. Fuente documental y uso responsable

Basado en el anteproyecto académico del proyecto de casas en renta. Las fuentes y licencias de mapas, datos e imágenes deben verificarse. Este repositorio es un proyecto académico y no representa una plataforma comercial ni una fuente oficial de información inmobiliaria.

---

*Política de actualización: este README es el documento público oficial; se actualiza solo en hitos con resultados verificables.*
