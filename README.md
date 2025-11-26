# PLAN DE PRUEBAS DE SOFTWARE
## Sistema de Gestión de Asistencia por Código QR - UPeU

**Versión:** 1.0  
**Fecha:** 2025-01-15  
**Elaborado por:** Equipo de QA

---

## INDICE GENERAL

1. REQUISITOS DEL SISTEMA
2. CASOS DE PRUEBA POR SUITE
3. TABLA MATRIZ DE CASOS

---

## 1. REQUISITOS DEL SISTEMA

### 1.1 Requisitos Funcionales (RF)

| ID | Descripción |
|----|-------------|
| RF-01 | El sistema debe permitir login con usuario y contraseña mediante endpoint POST /users/login |
| RF-02 | El sistema debe validar credenciales antes de permitir acceso al sistema |
| RF-03 | El sistema debe generar token JWT válido al autenticarse exitosamente |
| RF-04 | El sistema debe permitir registro de nuevos usuarios mediante endpoint POST /users/register |
| RF-05 | El sistema debe validar que username, correo y documento sean únicos en el registro |
| RF-06 | El sistema debe implementar control de acceso basado en roles (SUPERADMIN, ADMIN, LIDER, INTEGRANTE) |
| RF-07 | El sistema debe generar menú dinámico según rol del usuario mediante endpoint POST /accesos/menu |
| RF-08 | El sistema debe permitir gestión completa de matrículas (crear, leer, actualizar, eliminar) |
| RF-09 | El sistema debe permitir importación masiva de matrículas desde archivo Excel mediante POST /matriculas/importar |
| RF-10 | El sistema debe validar período académico obligatorio en importación de matrículas |
| RF-11 | El sistema debe permitir exportación de matrículas a Excel mediante GET /matriculas/exportar |
| RF-12 | El sistema debe permitir descarga de plantilla Excel para importación mediante GET /matriculas/descargar-plantilla |
| RF-13 | El sistema debe permitir filtrar matrículas por sede, facultad, programa, período y tipo de persona |
| RF-14 | El sistema debe permitir gestión CRUD de sedes académicas |
| RF-15 | El sistema debe permitir gestión CRUD de facultades |
| RF-16 | El sistema debe permitir gestión CRUD de programas de estudio |
| RF-17 | El sistema debe permitir gestión CRUD de períodos académicos |
| RF-18 | El sistema debe permitir obtener período activo mediante GET /periodos/activo |
| RF-19 | El sistema debe permitir gestión CRUD de eventos generales |
| RF-20 | El sistema debe permitir filtrar eventos generales por período y programa |
| RF-21 | El sistema debe permitir obtener eventos activos en una fecha mediante GET /eventos-generales/activos |
| RF-22 | El sistema debe permitir gestión CRUD de sesiones específicas (eventos específicos) |
| RF-23 | El sistema debe permitir crear sesiones recurrentes mediante POST /eventos-especificos/recurrencia |
| RF-24 | El sistema debe permitir filtrar sesiones por fecha mediante GET /eventos-especificos/fecha |
| RF-25 | El sistema debe permitir filtrar sesiones por rango de fechas mediante GET /eventos-especificos/rango |
| RF-26 | El sistema debe permitir gestión CRUD de grupos generales |
| RF-27 | El sistema debe permitir filtrar grupos generales por evento mediante GET /grupos-generales/evento/{id} |
| RF-28 | El sistema debe permitir gestión CRUD de grupos pequeños |
| RF-29 | El sistema debe permitir asignar líder a grupo pequeño |
| RF-30 | El sistema debe validar que líder no esté asignado a otro grupo del mismo evento |
| RF-31 | El sistema debe permitir obtener grupos pequeños de un líder mediante GET /grupos-pequenos/lider/{id} |
| RF-32 | El sistema debe permitir obtener participantes disponibles para un evento mediante GET /grupos-pequenos/disponibles/{id} |
| RF-33 | El sistema debe validar capacidad máxima al agregar participantes a grupo pequeño |
| RF-34 | El sistema debe permitir agregar participante a grupo pequeño mediante POST /grupo-participantes |
| RF-35 | El sistema debe permitir remover participante de grupo mediante PUT /grupo-participantes/remover/{id} |
| RF-36 | El sistema debe permitir obtener participantes de un grupo mediante GET /grupo-participantes/grupo/{id} |
| RF-37 | El sistema debe permitir generar código QR para sesión mediante GET /asistencias/generar-qr/{eventoId}/lider/{liderId} |
| RF-38 | El sistema debe validar que solo el líder del grupo pueda generar QR para sus sesiones |
| RF-39 | El sistema debe permitir registrar asistencia mediante escaneo QR mediante POST /asistencias/registrar-qr |
| RF-40 | El sistema debe validar que el registro por QR solo se permita el día de la sesión |
| RF-41 | El sistema debe validar ventana de tiempo para registro QR (30 min antes hasta 2 horas después) |
| RF-42 | El sistema debe prevenir registros duplicados de asistencia para la misma sesión y persona |
| RF-43 | El sistema debe validar que la persona pertenezca al evento antes de registrar asistencia |
| RF-44 | El sistema debe permitir obtener lista de participantes para llamado mediante GET /asistencias/lista-llamado/{eventoId}/lider/{liderId} |
| RF-45 | El sistema debe permitir marcar asistencia manualmente por líder mediante POST /asistencias/marcar-manual |
| RF-46 | El sistema debe permitir marcar asistencia con estados: PRESENTE, TARDE, AUSENTE, JUSTIFICADO |
| RF-47 | El sistema debe validar que líder solo pueda marcar asistencias de participantes de sus grupos |
| RF-48 | El sistema debe permitir consultar asistencias por sesión mediante GET /asistencias/sesion/{eventoEspecificoId} |
| RF-49 | El sistema debe permitir consultar asistencias por persona mediante GET /asistencias/persona/{personaId} |
| RF-50 | El sistema debe permitir generar reporte de asistencia por evento mediante GET /asistencias/reporte/{eventoGeneralId} |
| RF-51 | El sistema debe calcular porcentaje de asistencia por participante en reportes |
| RF-52 | El sistema debe permitir obtener usuarios por rol mediante GET /users/rol/{rolNombre} |
| RF-53 | El sistema debe permitir obtener líderes disponibles mediante GET /users/lideres-disponibles |
| RF-54 | El sistema debe permitir buscar persona por código de estudiante mediante GET /personas/codigo/{codigo} |
| RF-55 | El sistema debe mostrar dashboard administrativo con estadísticas (total personas, eventos activos, asistencias hoy, total matrículas) |
| RF-56 | El sistema debe mostrar dashboard de líder con estadísticas (mis grupos, participantes, asistencias registradas, porcentaje promedio) |
| RF-57 | El sistema debe mostrar dashboard de integrante con estadísticas básicas |
| RF-58 | El sistema debe redirigir automáticamente al dashboard según rol del usuario autenticado |

### 1.2 Requisitos No Funcionales (RNF)

| ID | Descripción |
|----|-------------|
| RNF-01 | El sistema debe responder a peticiones HTTP en menos de 2 segundos para operaciones CRUD básicas |
| RNF-02 | El sistema debe soportar al menos 100 usuarios concurrentes |
| RNF-03 | El sistema debe mantener disponibilidad del 99% durante horario académico |
| RNF-04 | El sistema debe utilizar autenticación JWT con tokens que expiran en 5 horas |
| RNF-05 | El sistema debe validar tokens JWT en cada petición a endpoints protegidos |
| RNF-06 | El sistema debe encriptar contraseñas usando BCrypt antes de almacenarlas |
| RNF-07 | El sistema debe permitir comunicación CORS desde cualquier origen (*) |
| RNF-08 | El sistema debe validar formato de archivos Excel (.xlsx, .xls) en importaciones |
| RNF-09 | El sistema debe generar códigos QR en formato base64 para visualización en frontend |
| RNF-10 | El sistema debe mantener integridad referencial en base de datos (foreign keys) |
| RNF-11 | El sistema debe validar unicidad de username, documento y código de estudiante |
| RNF-12 | El sistema debe manejar errores y retornar mensajes descriptivos en formato JSON |
| RNF-13 | El sistema debe ser compatible con navegadores modernos (Chrome, Firefox, Edge, Safari últimas 2 versiones) |
| RNF-14 | El sistema debe funcionar correctamente en dispositivos móviles para escaneo de QR |
| RNF-15 | El sistema debe mantener logs de operaciones críticas (creación, actualización, eliminación) |

---

## 2. CASOS DE PRUEBA POR SUITE

### 2.1 AUTENTICACIÓN

TC-AUT-001 – Login exitoso con credenciales válidas  
TC-AUT-002 – Login con credenciales inválidas  
TC-AUT-003 – Login con usuario inexistente  
TC-AUT-004 – Login con contraseña incorrecta  
TC-AUT-005 – Validación de campos vacíos en login  
TC-AUT-006 – Persistencia de token JWT en localStorage  
TC-AUT-007 – Validación de token JWT expirado  
TC-AUT-008 – Logout elimina token y datos de sesión  
TC-AUT-009 – Redirección automática según rol después de login  
TC-AUT-010 – Registro exitoso de nuevo usuario  
TC-AUT-011 – Registro con username duplicado  
TC-AUT-012 – Registro con correo duplicado  
TC-AUT-013 – Registro con documento duplicado  
TC-AUT-014 – Validación de formato de email en registro  
TC-AUT-015 – Validación de contraseñas que no coinciden en registro  
TC-AUT-016 – Redirección a login después de registro exitoso  
TC-AUT-017 – Acceso denegado a rutas protegidas sin token  
TC-AUT-018 – Acceso denegado con token inválido  
TC-AUT-019 – Renovación de sesión con token válido  
TC-AUT-020 – Limpieza de sesión al acceder a página de login

### 2.2 GESTIÓN DE USUARIOS, ROLES Y PERMISOS

TC-USU-001 – Obtener usuarios por rol ADMIN  
TC-USU-002 – Obtener usuarios por rol LIDER  
TC-USU-003 – Obtener usuarios por rol INTEGRANTE  
TC-USU-004 – Obtener líderes disponibles sin grupo asignado  
TC-USU-005 – Obtener líderes disponibles excluyendo grupo específico  
TC-USU-006 – Obtener menú dinámico para usuario ADMIN  
TC-USU-007 – Obtener menú dinámico para usuario LIDER  
TC-USU-008 – Obtener menú dinámico para usuario INTEGRANTE  
TC-USU-009 – Obtener menú dinámico para usuario SUPERADMIN  
TC-USU-010 – Validar que menú solo muestre accesos permitidos por rol  
TC-USU-011 – Validar que rutas restringidas no sean accesibles por roles no autorizados  
TC-USU-012 – Redirección automática cuando usuario sin permisos intenta acceder a ruta protegida

### 2.3 GESTIÓN DE MATRÍCULAS

TC-MAT-001 – Listar todas las matrículas  
TC-MAT-002 – Obtener matrícula por ID  
TC-MAT-003 – Buscar matrículas por código de estudiante  
TC-MAT-004 – Filtrar matrículas por sede  
TC-MAT-005 – Filtrar matrículas por facultad  
TC-MAT-006 – Filtrar matrículas por programa  
TC-MAT-007 – Filtrar matrículas por período  
TC-MAT-008 – Filtrar matrículas por tipo de persona (ESTUDIANTE/INVITADO)  
TC-MAT-009 – Filtrar matrículas con múltiples criterios combinados  
TC-MAT-010 – Crear nueva matrícula  
TC-MAT-011 – Actualizar matrícula existente  
TC-MAT-012 – Eliminar matrícula  
TC-MAT-013 – Importar matrículas desde Excel con formato válido  
TC-MAT-014 – Importar matrículas con período obligatorio  
TC-MAT-015 – Validar error al importar archivo no Excel  
TC-MAT-016 – Validar error al importar archivo Excel vacío  
TC-MAT-017 – Importar matrículas con filtros aplicados (sede, facultad, programa)  
TC-MAT-018 – Exportar matrículas a Excel sin filtros  
TC-MAT-019 – Exportar matrículas a Excel con filtros aplicados  
TC-MAT-020 – Descargar plantilla Excel para importación  
TC-MAT-021 – Validar formato de archivo Excel descargado  
TC-MAT-022 – Procesar reporte de importación (total, exitosos, fallidos, errores)

### 2.4 GESTIÓN DE ESTRUCTURA ACADÉMICA

#### 2.4.1 Sedes

TC-SED-001 – Listar todas las sedes  
TC-SED-002 – Obtener sede por ID  
TC-SED-003 – Crear nueva sede  
TC-SED-004 – Actualizar sede existente  
TC-SED-005 – Eliminar sede  
TC-SED-006 – Validar unicidad de nombre de sede

#### 2.4.2 Facultades

TC-FAC-001 – Listar todas las facultades  
TC-FAC-002 – Obtener facultad por ID  
TC-FAC-003 – Crear nueva facultad  
TC-FAC-004 – Actualizar facultad existente  
TC-FAC-005 – Eliminar facultad  
TC-FAC-006 – Validar unicidad de nombre de facultad

#### 2.4.3 Programas de Estudio

TC-PRO-001 – Listar todos los programas  
TC-PRO-002 – Obtener programa por ID  
TC-PRO-003 – Crear nuevo programa  
TC-PRO-004 – Actualizar programa existente  
TC-PRO-005 – Eliminar programa  
TC-PRO-006 – Validar unicidad de nombre de programa  
TC-PRO-007 – Validar relación programa-facultad

#### 2.4.4 Períodos Académicos

TC-PER-001 – Listar todos los períodos  
TC-PER-002 – Obtener período por ID  
TC-PER-003 – Obtener período activo  
TC-PER-004 – Filtrar períodos por estado (ACTIVO, INACTIVO, FINALIZADO)  
TC-PER-005 – Crear nuevo período  
TC-PER-006 – Actualizar período existente  
TC-PER-007 – Eliminar período  
TC-PER-008 – Validar unicidad de nombre de período  
TC-PER-009 – Validar que fecha fin sea posterior a fecha inicio

### 2.5 GESTIÓN DE EVENTOS GENERALES

TC-EVG-001 – Listar todos los eventos generales  
TC-EVG-002 – Obtener evento general por ID  
TC-EVG-003 – Filtrar eventos por programa  
TC-EVG-004 – Filtrar eventos por período y programa  
TC-EVG-005 – Filtrar eventos solo por período  
TC-EVG-006 – Obtener eventos activos en una fecha específica  
TC-EVG-007 – Crear nuevo evento general  
TC-EVG-008 – Validar que fecha fin sea posterior a fecha inicio  
TC-EVG-009 – Validar relación evento-período  
TC-EVG-010 – Validar relación evento-programa  
TC-EVG-011 – Actualizar evento general existente  
TC-EVG-012 – Eliminar evento general  
TC-EVG-013 – Validar estado por defecto ACTIVO al crear evento

### 2.6 GESTIÓN DE SESIONES (EVENTOS ESPECÍFICOS)

TC-SES-001 – Listar todas las sesiones  
TC-SES-002 – Obtener sesión por ID  
TC-SES-003 – Filtrar sesiones por evento general  
TC-SES-004 – Filtrar sesiones por fecha específica  
TC-SES-005 – Filtrar sesiones por rango de fechas  
TC-SES-006 – Crear sesión individual  
TC-SES-007 – Validar que hora fin sea posterior a hora inicio  
TC-SES-008 – Validar tolerancia mínima por defecto (10 minutos)  
TC-SES-009 – Crear sesiones recurrentes con días de semana específicos  
TC-SES-010 – Crear recurrencia con rango de fechas válido  
TC-SES-011 – Validar que sesiones recurrentes se creen en días correctos  
TC-SES-012 – Actualizar sesión existente  
TC-SES-013 – Eliminar sesión  
TC-SES-014 – Validar relación sesión-evento general  
TC-SES-015 – Validar estado por defecto PROGRAMADO al crear sesión

### 2.7 GESTIÓN DE GRUPOS GENERALES

TC-GRG-001 – Listar todos los grupos generales  
TC-GRG-002 – Obtener grupo general por ID  
TC-GRG-003 – Filtrar grupos generales por evento  
TC-GRG-004 – Crear nuevo grupo general  
TC-GRG-005 – Validar relación grupo general-evento general  
TC-GRG-006 – Actualizar grupo general existente  
TC-GRG-007 – Eliminar grupo general

### 2.8 GESTIÓN DE GRUPOS PEQUEÑOS

TC-GRP-001 – Listar todos los grupos pequeños  
TC-GRP-002 – Obtener grupo pequeño por ID  
TC-GRP-003 – Filtrar grupos pequeños por grupo general  
TC-GRP-004 – Filtrar grupos pequeños por líder  
TC-GRP-005 – Obtener participantes disponibles para evento  
TC-GRP-006 – Crear nuevo grupo pequeño  
TC-GRP-007 – Asignar líder a grupo pequeño  
TC-GRP-008 – Validar que líder no esté asignado a otro grupo del mismo evento  
TC-GRP-009 – Validar capacidad máxima por defecto (20 participantes)  
TC-GRP-010 – Actualizar grupo pequeño existente  
TC-GRP-011 – Eliminar grupo pequeño  
TC-GRP-012 – Validar relación grupo pequeño-grupo general

### 2.9 GESTIÓN DE PARTICIPANTES EN GRUPOS

TC-PAR-001 – Listar todos los participantes  
TC-PAR-002 – Obtener participante por ID  
TC-PAR-003 – Filtrar participantes por grupo pequeño  
TC-PAR-004 – Filtrar participantes por persona  
TC-PAR-005 – Agregar participante a grupo pequeño  
TC-PAR-006 – Validar que participante no esté duplicado en el mismo grupo  
TC-PAR-007 – Validar capacidad máxima al agregar participante  
TC-PAR-008 – Validar que participante no esté en otro grupo del mismo evento  
TC-PAR-009 – Remover participante de grupo (marcar como INACTIVO)  
TC-PAR-010 – Eliminar participante de grupo  
TC-PAR-011 – Validar estado por defecto ACTIVO al agregar participante

### 2.10 REGISTRO DE ASISTENCIAS CON QR

TC-QR-001 – Generar código QR para sesión válida  
TC-QR-002 – Validar que solo líder del grupo pueda generar QR  
TC-QR-003 – Validar que QR contenga datos correctos de sesión  
TC-QR-004 – Validar formato de imagen QR en base64  
TC-QR-005 – Escanear QR válido y registrar asistencia  
TC-QR-006 – Validar registro solo el día de la sesión  
TC-QR-007 – Validar ventana de tiempo (30 min antes - 2 horas después)  
TC-QR-008 – Validar que persona pertenezca al evento antes de registrar  
TC-QR-009 – Prevenir registro duplicado de asistencia  
TC-QR-010 – Validar error al escanear QR fuera de horario permitido  
TC-QR-011 – Validar error al escanear QR de día incorrecto  
TC-QR-012 – Validar error al escanear QR de evento al que no pertenece  
TC-QR-013 – Registrar asistencia con coordenadas GPS opcionales  
TC-QR-014 – Determinar estado PRESENTE o TARDE según tolerancia

### 2.11 GESTIÓN DE ASISTENCIAS

TC-ASI-001 – Listar todas las asistencias  
TC-ASI-002 – Obtener asistencia por ID  
TC-ASI-003 – Filtrar asistencias por sesión (evento específico)  
TC-ASI-004 – Filtrar asistencias por persona  
TC-ASI-005 – Obtener lista de participantes para llamado (con estado de asistencia)  
TC-ASI-006 – Validar que líder solo vea participantes de sus grupos  
TC-ASI-007 – Marcar asistencia manual como PRESENTE  
TC-ASI-008 – Marcar asistencia manual como TARDE  
TC-ASI-009 – Marcar asistencia manual como AUSENTE  
TC-ASI-010 – Marcar asistencia manual como JUSTIFICADO con motivo  
TC-ASI-011 – Validar que líder solo pueda marcar asistencias de sus grupos  
TC-ASI-012 – Actualizar asistencia existente  
TC-ASI-013 – Eliminar asistencia  
TC-ASI-014 – Consultar historial personal de asistencias

### 2.12 REPORTES Y CONSULTAS

TC-REP-001 – Generar reporte de asistencia por evento general  
TC-REP-002 – Validar cálculo de total de sesiones en reporte  
TC-REP-003 – Validar cálculo de asistencias PRESENTE en reporte  
TC-REP-004 – Validar cálculo de asistencias TARDE en reporte  
TC-REP-005 – Validar cálculo de asistencias AUSENTE en reporte  
TC-REP-006 – Validar cálculo de asistencias JUSTIFICADO en reporte  
TC-REP-007 – Validar cálculo de porcentaje de asistencia por participante  
TC-REP-008 – Validar que reporte incluya todos los participantes del evento  
TC-REP-009 – Consultar dashboard administrativo con estadísticas  
TC-REP-010 – Consultar dashboard de líder con estadísticas  
TC-REP-011 – Consultar dashboard de integrante

### 2.13 SEGURIDAD

TC-SEG-001 – Validar autenticación JWT en endpoints protegidos  
TC-SEG-002 – Validar rechazo de peticiones sin token  
TC-SEG-003 – Validar rechazo de peticiones con token inválido  
TC-SEG-004 – Validar rechazo de peticiones con token expirado  
TC-SEG-005 – Validar encriptación de contraseñas con BCrypt  
TC-SEG-006 – Validar que contraseñas no se almacenen en texto plano  
TC-SEG-007 – Validar control de acceso por roles en endpoints  
TC-SEG-008 – Validar que ADMIN no pueda acceder a funcionalidades de SUPERADMIN  
TC-SEG-009 – Validar que LIDER solo acceda a sus grupos  
TC-SEG-010 – Validar que INTEGRANTE solo vea sus propias asistencias  
TC-SEG-011 – Validar headers CORS en respuestas  
TC-SEG-012 – Validar protección contra inyección SQL en consultas

### 2.14 BASE DE DATOS

TC-BD-001 – Validar integridad referencial al eliminar sede con matrículas  
TC-BD-002 – Validar integridad referencial al eliminar facultad con programas  
TC-BD-003 – Validar integridad referencial al eliminar programa con eventos  
TC-BD-004 – Validar integridad referencial al eliminar período con eventos  
TC-BD-005 – Validar integridad referencial al eliminar evento con sesiones  
TC-BD-006 – Validar integridad referencial al eliminar grupo general con grupos pequeños  
TC-BD-007 – Validar integridad referencial al eliminar grupo pequeño con participantes  
TC-BD-008 – Validar constraint UNIQUE en username de usuario  
TC-BD-009 – Validar constraint UNIQUE en documento de persona  
TC-BD-010 – Validar constraint UNIQUE en código de estudiante  
TC-BD-011 – Validar constraint UNIQUE en nombre de sede  
TC-BD-012 – Validar constraint UNIQUE en nombre de facultad  
TC-BD-013 – Validar constraint UNIQUE en nombre de programa  
TC-BD-014 – Validar constraint UNIQUE en nombre de período  
TC-BD-015 – Validar constraint UNIQUE en asistencia (evento específico + persona)  
TC-BD-016 – Validar constraint UNIQUE en grupo participante (grupo pequeño + persona)  
TC-BD-017 – Validar transacciones atómicas en creación de eventos con sesiones  
TC-BD-018 – Validar rollback en caso de error en transacciones

### 2.15 ERRORES Y EXCEPCIONES

TC-ERR-001 – Manejo de error 400 Bad Request en validaciones  
TC-ERR-002 – Manejo de error 401 Unauthorized en autenticación  
TC-ERR-003 – Manejo de error 404 Not Found en recursos inexistentes  
TC-ERR-004 – Manejo de error 500 Internal Server Error  
TC-ERR-005 – Mensajes de error descriptivos en formato JSON  
TC-ERR-006 – Validación de campos requeridos con mensajes claros  
TC-ERR-007 – Manejo de excepciones de constraint violation  
TC-ERR-008 – Manejo de excepciones de ModelNotFoundException  
TC-ERR-009 – Manejo de excepciones de RuntimeException  
TC-ERR-010 – Validación de formato de archivo en importación Excel  
TC-ERR-011 – Manejo de errores de conexión a base de datos  
TC-ERR-012 – Manejo de errores de timeout en peticiones

### 2.16 RENDIMIENTO Y STRESS

TC-PER-001 – Tiempo de respuesta de login menor a 1 segundo  
TC-PER-002 – Tiempo de respuesta de listado de matrículas menor a 2 segundos  
TC-PER-003 – Tiempo de respuesta de generación de QR menor a 500ms  
TC-PER-004 – Tiempo de respuesta de registro de asistencia menor a 1 segundo  
TC-PER-005 – Sistema soporta 50 usuarios concurrentes en login  
TC-PER-006 – Sistema soporta 100 usuarios concurrentes consultando asistencias  
TC-PER-007 – Importación de Excel con 1000 registros completa en menos de 30 segundos  
TC-PER-008 – Generación de reporte con 500 participantes completa en menos de 5 segundos  
TC-PER-009 – Consulta de dashboard completa en menos de 2 segundos  
TC-PER-010 – Sistema mantiene rendimiento bajo carga de 100 usuarios simultáneos

### 2.17 COMPATIBILIDAD

TC-COM-001 – Funcionalidad completa en Chrome (últimas 2 versiones)  
TC-COM-002 – Funcionalidad completa en Firefox (últimas 2 versiones)  
TC-COM-003 – Funcionalidad completa en Edge (últimas 2 versiones)  
TC-COM-004 – Funcionalidad completa en Safari (últimas 2 versiones)  
TC-COM-005 – Escaneo de QR funcional en dispositivos Android  
TC-COM-006 – Escaneo de QR funcional en dispositivos iOS  
TC-COM-007 – Interfaz responsive en tablets  
TC-COM-008 – Interfaz responsive en móviles  
TC-COM-009 – Visualización correcta de tablas en diferentes resoluciones  
TC-COM-010 – Funcionalidad de importación Excel en diferentes navegadores

---

## 3. TABLA DE CASOS DE PRUEBA

| Suite | ID | Título | Precondiciones | Pasos | Resultado Esperado | Prioridad | Tipo | Requisitos | Responsable |
|-------|----|--------|----------------|-------|-------------------|-----------|------|------------|-------------|
| Autenticación | TC-AUT-001 | Login exitoso con credenciales válidas | Usuario registrado y activo en BD. API accesible por HTTPS. | 1. Abrir aplicación en navegador<br>2. Acceder a ruta /login<br>3. Ingresar username válido<br>4. Ingresar password válido<br>5. Click en botón "Ingresar" | Se autentica exitosamente, se genera token JWT, se almacena en localStorage, se redirige al dashboard según rol del usuario. | P1 | Funcional/API | RF-01, RF-02, RF-03 | Tester |
| Autenticación | TC-AUT-002 | Login con credenciales inválidas | Usuario existe en BD. | 1. Abrir /login<br>2. Ingresar username válido<br>3. Ingresar password incorrecto<br>4. Click en "Ingresar" | Se muestra mensaje de error "Credenciales inválidas", no se genera token, usuario permanece en página de login. | P1 | Funcional/API | RF-02 | Tester |
| Autenticación | TC-AUT-003 | Login con usuario inexistente | Usuario NO existe en BD. | 1. Abrir /login<br>2. Ingresar username inexistente<br>3. Ingresar cualquier password<br>4. Click en "Ingresar" | Se muestra mensaje de error, no se genera token, usuario permanece en página de login. | P1 | Funcional/API | RF-02 | Tester |
| Autenticación | TC-AUT-004 | Login con contraseña incorrecta | Usuario existe en BD con password conocida. | 1. Abrir /login<br>2. Ingresar username válido<br>3. Ingresar password incorrecta<br>4. Click en "Ingresar" | Se muestra mensaje de error, no se genera token. | P1 | Funcional/API | RF-02 | Tester |
| Autenticación | TC-AUT-005 | Validación de campos vacíos en login | Ninguna. | 1. Abrir /login<br>2. Dejar campos username y password vacíos<br>3. Click en "Ingresar" | Se muestra mensaje de validación "Por favor completa todos los campos", formulario no se envía. | P2 | Funcional/UI | RF-02 | Tester |
| Autenticación | TC-AUT-006 | Persistencia de token JWT en localStorage | Login exitoso realizado. | 1. Realizar login exitoso<br>2. Abrir DevTools del navegador<br>3. Verificar localStorage | Token JWT está almacenado en localStorage con clave "token", datos de usuario almacenados con clave "user". | P1 | Funcional | RF-03 | Tester |
| Autenticación | TC-AUT-007 | Validación de token JWT expirado | Token JWT expirado almacenado en localStorage. | 1. Tener token expirado en localStorage<br>2. Intentar acceder a ruta protegida<br>3. Realizar petición a API protegida | Token es detectado como expirado, se elimina de localStorage, se redirige a /login, petición API retorna 401 Unauthorized. | P1 | Funcional/Seguridad | RF-03, RNF-04 | Tester |
| Autenticación | TC-AUT-008 | Logout elimina token y datos de sesión | Usuario autenticado con token válido. | 1. Usuario autenticado en sistema<br>2. Click en botón "Cerrar Sesión" o llamar a authService.logout() | Token eliminado de localStorage, datos de usuario eliminados, redirección a /login. | P1 | Funcional | RF-08 | Tester |
| Autenticación | TC-AUT-009 | Redirección automática según rol después de login | Usuario autenticado con rol específico. | 1. Login exitoso como ADMIN<br>2. Login exitoso como LIDER<br>3. Login exitoso como INTEGRANTE<br>4. Login exitoso como SUPERADMIN | ADMIN redirige a /dashboard/admin, LIDER redirige a /dashboard/lider, INTEGRANTE redirige a /dashboard/integrante, SUPERADMIN redirige a /superadmin. | P1 | Funcional | RF-58 | Tester |
| Autenticación | TC-AUT-010 | Registro exitoso de nuevo usuario | No existe usuario con mismo username/correo/documento. | 1. Acceder a /register<br>2. Completar formulario: username, nombreCompleto, correo, documento, password, confirmPassword<br>3. Click en "Registrarse" | Usuario creado en BD, persona creada asociada, mensaje de éxito, redirección a /login. | P1 | Funcional/API | RF-04 | Tester |
| Autenticación | TC-AUT-011 | Registro con username duplicado | Usuario con mismo username ya existe en BD. | 1. Acceder a /register<br>2. Ingresar username existente<br>3. Completar resto del formulario<br>4. Click en "Registrarse" | Se muestra mensaje de error "El nombre de usuario ya está en uso", usuario no se crea. | P1 | Funcional/API | RF-05 | Tester |
| Autenticación | TC-AUT-012 | Registro con correo duplicado | Usuario con mismo correo ya existe en BD. | 1. Acceder a /register<br>2. Ingresar correo existente<br>3. Completar resto del formulario<br>4. Click en "Registrarse" | Se muestra mensaje de error "El correo electrónico ya está registrado", usuario no se crea. | P1 | Funcional/API | RF-05 | Tester |
| Autenticación | TC-AUT-013 | Registro con documento duplicado | Persona con mismo documento ya existe en BD. | 1. Acceder a /register<br>2. Ingresar documento existente<br>3. Completar resto del formulario<br>4. Click en "Registrarse" | Se muestra mensaje de error "El número de documento ya está registrado", usuario no se crea. | P1 | Funcional/API | RF-05 | Tester |
| Autenticación | TC-AUT-014 | Validación de formato de email en registro | Ninguna. | 1. Acceder a /register<br>2. Ingresar email con formato inválido (ej: "email_invalido")<br>3. Completar resto del formulario<br>4. Click en "Registrarse" | Se muestra mensaje de error "Debe ser un correo válido", formulario no se envía o backend rechaza con 400. | P2 | Funcional/Validación | RF-05 | Tester |
| Autenticación | TC-AUT-015 | Validación de contraseñas que no coinciden en registro | Ninguna. | 1. Acceder a /register<br>2. Ingresar password<br>3. Ingresar confirmPassword diferente<br>4. Click en "Registrarse" | Se muestra mensaje de error "Las contraseñas no coinciden", formulario no se envía. | P2 | Funcional/UI | RF-05 | Tester |
| Autenticación | TC-AUT-016 | Redirección a login después de registro exitoso | Registro exitoso completado. | 1. Completar registro exitoso<br>2. Verificar redirección | Usuario es redirigido automáticamente a /login, no se genera token automáticamente. | P2 | Funcional | RF-04 | Tester |
| Autenticación | TC-AUT-017 | Acceso denegado a rutas protegidas sin token | Usuario no autenticado. | 1. Sin token en localStorage<br>2. Intentar acceder a /dashboard/admin o cualquier ruta protegida | Se redirige automáticamente a /login, no se muestra contenido protegido. | P1 | Seguridad | RF-06, RNF-05 | Tester |
| Autenticación | TC-AUT-018 | Acceso denegado con token inválido | Token con formato incorrecto o corrupto. | 1. Almacenar token inválido en localStorage<br>2. Intentar acceder a ruta protegida<br>3. Realizar petición a API | Se redirige a /login, petición API retorna 401 Unauthorized, token se elimina de localStorage. | P1 | Seguridad | RF-06, RNF-05 | Tester |
| Autenticación | TC-AUT-019 | Renovación de sesión con token válido | Usuario autenticado con token válido no expirado. | 1. Usuario autenticado<br>2. Realizar petición a API protegida con token válido | Petición se procesa exitosamente, no se requiere nuevo login, token sigue siendo válido. | P2 | Funcional | RF-03, RNF-04 | Tester |
| Autenticación | TC-AUT-020 | Limpieza de sesión al acceder a página de login | Usuario puede estar autenticado o no. | 1. Acceder a ruta /login<br>2. Verificar localStorage | Si había token o datos de usuario, se limpian automáticamente al cargar página de login. | P2 | Funcional | RF-08 | Tester |
| Gestión de Usuarios | TC-USU-001 | Obtener usuarios por rol ADMIN | Usuario ADMIN autenticado. Existen usuarios con rol ADMIN en BD. | 1. Login como ADMIN<br>2. Realizar GET /users/rol/ADMIN con token válido | Se retorna lista de usuarios con rol ADMIN, respuesta 200 OK, formato JSON correcto. | P2 | API | RF-52 | Tester |
| Gestión de Usuarios | TC-USU-002 | Obtener usuarios por rol LIDER | Usuario ADMIN autenticado. Existen usuarios con rol LIDER en BD. | 1. Login como ADMIN<br>2. Realizar GET /users/rol/LIDER con token válido | Se retorna lista de usuarios con rol LIDER, respuesta 200 OK. | P2 | API | RF-52 | Tester |
| Gestión de Usuarios | TC-USU-003 | Obtener usuarios por rol INTEGRANTE | Usuario ADMIN autenticado. Existen usuarios con rol INTEGRANTE en BD. | 1. Login como ADMIN<br>2. Realizar GET /users/rol/INTEGRANTE con token válido | Se retorna lista de usuarios con rol INTEGRANTE, respuesta 200 OK. | P2 | API | RF-52 | Tester |
| Gestión de Usuarios | TC-USU-004 | Obtener líderes disponibles sin grupo asignado | Usuario ADMIN autenticado. Existen líderes sin grupo asignado. | 1. Login como ADMIN<br>2. Realizar GET /users/lideres-disponibles sin parámetros | Se retorna lista de líderes (PersonaDTO) que no tienen grupo pequeño asignado, respuesta 200 OK. | P2 | API | RF-53 | Tester |
| Gestión de Usuarios | TC-USU-005 | Obtener líderes disponibles excluyendo grupo específico | Usuario ADMIN autenticado. Existe grupo pequeño con ID conocido. | 1. Login como ADMIN<br>2. Realizar GET /users/lideres-disponibles?excludeGrupoId=1 | Se retorna lista de líderes excluyendo el líder del grupo especificado, respuesta 200 OK. | P2 | API | RF-53 | Tester |
| Gestión de Usuarios | TC-USU-006 | Obtener menú dinámico para usuario ADMIN | Usuario ADMIN autenticado. | 1. Login como ADMIN<br>2. Realizar POST /accesos/menu con username en body<br>3. Verificar respuesta | Se retorna lista de MenuGroup con accesos de ADMIN (Matrículas, Importar Excel, Sedes, Facultades, Programas, Eventos, Grupos, Reportes, Dashboard Admin), respuesta 200 OK. | P1 | API/Funcional | RF-07 | Tester |
| Gestión de Usuarios | TC-USU-007 | Obtener menú dinámico para usuario LIDER | Usuario LIDER autenticado. | 1. Login como LIDER<br>2. Realizar POST /accesos/menu con username en body | Se retorna lista de MenuGroup con accesos de LIDER (Dashboard Líder, Mis Grupos, Registrar Asistencia, Ver Asistencias, Mis Asistencias), respuesta 200 OK. | P1 | API/Funcional | RF-07 | Tester |
| Gestión de Usuarios | TC-USU-008 | Obtener menú dinámico para usuario INTEGRANTE | Usuario INTEGRANTE autenticado. | 1. Login como INTEGRANTE<br>2. Realizar POST /accesos/menu con username en body | Se retorna lista de MenuGroup con accesos de INTEGRANTE (Dashboard Integrante, Mis Asistencias, Escanear QR), respuesta 200 OK. | P1 | API/Funcional | RF-07 | Tester |
| Gestión de Usuarios | TC-USU-009 | Obtener menú dinámico para usuario SUPERADMIN | Usuario SUPERADMIN autenticado. | 1. Login como SUPERADMIN<br>2. Realizar POST /accesos/menu con username en body | Se retorna lista de MenuGroup con TODOS los accesos del sistema, respuesta 200 OK. | P1 | API/Funcional | RF-07 | Tester |
| Gestión de Usuarios | TC-USU-010 | Validar que menú solo muestre accesos permitidos por rol | Usuarios de diferentes roles autenticados. | 1. Login como ADMIN y obtener menú<br>2. Login como LIDER y obtener menú<br>3. Comparar accesos | Cada rol ve solo los accesos asignados a su rol, no se muestran accesos de otros roles. | P1 | Funcional/Seguridad | RF-06, RF-07 | Tester |
| Gestión de Usuarios | TC-USU-011 | Validar que rutas restringidas no sean accesibles por roles no autorizados | Usuario INTEGRANTE autenticado. | 1. Login como INTEGRANTE<br>2. Intentar acceder manualmente a /matriculas (solo ADMIN)<br>3. Intentar acceder a /asistencias/registrar (solo LIDER) | Se redirige o se muestra mensaje de acceso denegado, funcionalidad no es accesible, menú no muestra opciones restringidas. | P1 | Seguridad | RF-06 | Tester |
| Gestión de Usuarios | TC-USU-012 | Redirección automática cuando usuario sin permisos intenta acceder a ruta protegida | Usuario autenticado sin permisos para ruta específica. | 1. Login como INTEGRANTE<br>2. Modificar URL manualmente a /matriculas<br>3. Verificar comportamiento | Sistema detecta falta de permisos, redirige a dashboard del usuario o muestra error 403, no se muestra contenido restringido. | P1 | Seguridad | RF-06 | Tester |
| Gestión de Matrículas | TC-MAT-001 | Listar todas las matrículas | Usuario ADMIN autenticado. Existen matrículas en BD. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Verificar lista | Se muestra tabla con todas las matrículas, columnas: código, nombre, programa, período, estado, respuesta 200 OK. | P1 | Funcional/API | RF-08 | Tester |
| Gestión de Matrículas | TC-MAT-002 | Obtener matrícula por ID | Usuario ADMIN autenticado. Matrícula con ID conocido existe. | 1. Login como ADMIN<br>2. Realizar GET /matriculas/{id} con token | Se retorna matrícula completa con todos los datos, respuesta 200 OK, formato MatriculaDTO correcto. | P2 | API | RF-08 | Tester |
| Gestión de Matrículas | TC-MAT-003 | Buscar matrículas por código de estudiante | Usuario ADMIN autenticado. Matrícula con código conocido existe. | 1. Login como ADMIN<br>2. Realizar GET /matriculas/estudiante/{codigo} | Se retorna lista de matrículas del estudiante, respuesta 200 OK. | P2 | API | RF-08 | Tester |
| Gestión de Matrículas | TC-MAT-004 | Filtrar matrículas por sede | Usuario ADMIN autenticado. Existen matrículas de diferentes sedes. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar filtro "Sede"<br>4. Aplicar filtro | Solo se muestran matrículas de la sede seleccionada, respuesta 200 OK. | P2 | Funcional/API | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-005 | Filtrar matrículas por facultad | Usuario ADMIN autenticado. Existen matrículas de diferentes facultades. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar filtro "Facultad"<br>4. Aplicar filtro | Solo se muestran matrículas de la facultad seleccionada, respuesta 200 OK. | P2 | Funcional/API | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-006 | Filtrar matrículas por programa | Usuario ADMIN autenticado. Existen matrículas de diferentes programas. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar filtro "Programa"<br>4. Aplicar filtro | Solo se muestran matrículas del programa seleccionado, respuesta 200 OK. | P2 | Funcional/API | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-007 | Filtrar matrículas por período | Usuario ADMIN autenticado. Existen matrículas de diferentes períodos. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar filtro "Período"<br>4. Aplicar filtro | Solo se muestran matrículas del período seleccionado, respuesta 200 OK. | P1 | Funcional/API | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-008 | Filtrar matrículas por tipo de persona | Usuario ADMIN autenticado. Existen matrículas de tipo ESTUDIANTE e INVITADO. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar filtro "Tipo Persona: ESTUDIANTE"<br>4. Aplicar filtro | Solo se muestran matrículas de tipo ESTUDIANTE, respuesta 200 OK. | P2 | Funcional/API | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-009 | Filtrar matrículas con múltiples criterios combinados | Usuario ADMIN autenticado. Existen matrículas con diferentes combinaciones. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar múltiples filtros: Sede, Facultad, Programa, Período<br>4. Aplicar filtros | Solo se muestran matrículas que cumplen TODOS los criterios seleccionados, respuesta 200 OK. | P2 | Funcional/API | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-010 | Crear nueva matrícula | Usuario ADMIN autenticado. Persona, Sede, Facultad, Programa, Período existen en BD. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Click en "Nueva Matrícula"<br>4. Completar formulario con datos válidos<br>5. Click en "Guardar" | Matrícula creada en BD, mensaje de éxito, matrícula visible en lista, respuesta 201 Created. | P1 | Funcional/API | RF-08 | Tester |
| Gestión de Matrículas | TC-MAT-011 | Actualizar matrícula existente | Usuario ADMIN autenticado. Matrícula existe en BD. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar matrícula<br>4. Click en "Editar"<br>5. Modificar datos<br>6. Click en "Guardar" | Matrícula actualizada en BD, cambios reflejados en lista, respuesta 200 OK. | P1 | Funcional/API | RF-08 | Tester |
| Gestión de Matrículas | TC-MAT-012 | Eliminar matrícula | Usuario ADMIN autenticado. Matrícula existe en BD. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Seleccionar matrícula<br>4. Click en "Eliminar"<br>5. Confirmar eliminación | Matrícula eliminada de BD, desaparece de lista, respuesta 200 OK con CustomResponse. | P2 | Funcional/API | RF-08 | Tester |
| Gestión de Matrículas | TC-MAT-013 | Importar matrículas desde Excel con formato válido | Usuario ADMIN autenticado. Archivo Excel válido con formato correcto. Período existe en BD. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Seleccionar período<br>4. Seleccionar archivo Excel válido<br>5. Aplicar filtros opcionales<br>6. Click en "Importar" | Procesamiento exitoso, reporte muestra: total registros, exitosos, fallidos, errores detallados, matrículas creadas en BD, respuesta 200 OK. | P1 | Funcional/API | RF-09, RF-10 | Tester |
| Gestión de Matrículas | TC-MAT-014 | Importar matrículas con período obligatorio | Usuario ADMIN autenticado. Archivo Excel válido. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Seleccionar archivo Excel<br>4. NO seleccionar período<br>5. Click en "Importar" | Se muestra mensaje de error "Debe seleccionar un periodo para la importación", importación no se ejecuta, respuesta 400 Bad Request. | P1 | Funcional/Validación | RF-10 | Tester |
| Gestión de Matrículas | TC-MAT-015 | Validar error al importar archivo no Excel | Usuario ADMIN autenticado. Archivo .txt o .pdf disponible. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Seleccionar archivo .txt o .pdf<br>4. Click en "Importar" | Se muestra mensaje de error "El archivo debe ser un Excel (.xlsx o .xls)", importación no se ejecuta, respuesta 400 Bad Request. | P1 | Funcional/Validación | RNF-08 | Tester |
| Gestión de Matrículas | TC-MAT-016 | Validar error al importar archivo Excel vacío | Usuario ADMIN autenticado. Archivo Excel vacío disponible. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Seleccionar archivo Excel vacío<br>4. Click en "Importar" | Se muestra mensaje de error "El archivo está vacío", importación no se ejecuta, respuesta 400 Bad Request. | P2 | Funcional/Validación | RF-09 | Tester |
| Gestión de Matrículas | TC-MAT-017 | Importar matrículas con filtros aplicados | Usuario ADMIN autenticado. Archivo Excel válido. Filtros: sede, facultad, programa. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Seleccionar período<br>4. Seleccionar filtros: sede, facultad, programa<br>5. Seleccionar archivo Excel<br>6. Click en "Importar" | Solo se procesan y crean matrículas que cumplen los filtros, reporte indica filtros aplicados, respuesta 200 OK. | P2 | Funcional/API | RF-09, RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-018 | Exportar matrículas a Excel sin filtros | Usuario ADMIN autenticado. Existen matrículas en BD. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Click en "Exportar a Excel" sin aplicar filtros | Se descarga archivo Excel con todas las matrículas, formato válido, nombre de archivo con timestamp, respuesta 200 OK con Content-Type application/vnd.openxmlformats-officedocument.spreadsheetml.sheet. | P2 | Funcional/API | RF-11 | Tester |
| Gestión de Matrículas | TC-MAT-019 | Exportar matrículas a Excel con filtros aplicados | Usuario ADMIN autenticado. Filtros aplicados en interfaz. | 1. Login como ADMIN<br>2. Acceder a /matriculas<br>3. Aplicar filtros: sede, facultad, programa, período<br>4. Click en "Exportar a Excel" | Se descarga archivo Excel solo con matrículas que cumplen los filtros, formato válido, respuesta 200 OK. | P2 | Funcional/API | RF-11, RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-020 | Descargar plantilla Excel para importación | Usuario ADMIN autenticado. | 1. Login como ADMIN<br>2. Acceder a /matriculas/importar<br>3. Click en "Descargar Plantilla" | Se descarga archivo "Plantilla_Importacion_Matriculas.xlsx", plantilla contiene columnas correctas según MatriculaExcelDTO, formato válido, respuesta 200 OK. | P2 | Funcional/API | RF-12 | Tester |
| Gestión de Matrículas | TC-MAT-021 | Validar formato de archivo Excel descargado | Archivo Excel descargado disponible. | 1. Descargar plantilla o exportación<br>2. Abrir archivo en Excel o herramienta compatible<br>3. Verificar estructura | Archivo se abre correctamente, contiene datos en formato tabular, columnas correctas, sin errores de formato. | P2 | Funcional | RF-11, RF-12 | Tester |
| Gestión de Matrículas | TC-MAT-022 | Procesar reporte de importación | Importación de Excel ejecutada. | 1. Ejecutar importación<br>2. Verificar reporte mostrado | Reporte muestra: totalRegistros, exitosos, fallidos, lista de errores detallados, lista de warnings, formato ImportResultDTO correcto. | P1 | Funcional | RF-09 | Tester |
| Gestión Estructura Académica - Sedes | TC-SED-001 | Listar todas las sedes | Usuario ADMIN autenticado. Existen sedes en BD. | 1. Login como ADMIN<br>2. Acceder a /sedes<br>3. Verificar lista | Se muestra tabla con todas las sedes, columnas: ID, nombre, descripción, respuesta 200 OK. | P2 | Funcional/API | RF-14 | Tester |
| Gestión Estructura Académica - Sedes | TC-SED-002 | Obtener sede por ID | Usuario ADMIN autenticado. Sede con ID conocido existe. | 1. Login como ADMIN<br>2. Realizar GET /sedes/{id} con token | Se retorna sede completa, respuesta 200 OK, formato SedeDTO correcto. | P2 | API | RF-14 | Tester |
| Gestión Estructura Académica - Sedes | TC-SED-003 | Crear nueva sede | Usuario ADMIN autenticado. Nombre de sede único. | 1. Login como ADMIN<br>2. Acceder a /sedes<br>3. Click en "Nueva Sede"<br>4. Ingresar nombre y descripción<br>5. Click en "Guardar" | Sede creada en BD, mensaje de éxito, sede visible en lista, respuesta 201 Created. | P1 | Funcional/API | RF-14 | Tester |
| Gestión Estructura Académica - Sedes | TC-SED-004 | Actualizar sede existente | Usuario ADMIN autenticado. Sede existe en BD. | 1. Login como ADMIN<br>2. Acceder a /sedes<br>3. Seleccionar sede<br>4. Click en "Editar"<br>5. Modificar datos<br>6. Click en "Guardar" | Sede actualizada en BD, cambios reflejados, respuesta 200 OK. | P1 | Funcional/API | RF-14 | Tester |
| Gestión Estructura Académica - Sedes | TC-SED-005 | Eliminar sede | Usuario ADMIN autenticado. Sede existe en BD sin matrículas asociadas. | 1. Login como ADMIN<br>2. Acceder a /sedes<br>3. Seleccionar sede<br>4. Click en "Eliminar"<br>5. Confirmar | Sede eliminada de BD, desaparece de lista, respuesta 200 OK. | P2 | Funcional/API | RF-14 | Tester |
| Gestión Estructura Académica - Sedes | TC-SED-006 | Validar unicidad de nombre de sede | Usuario ADMIN autenticado. Sede con nombre "Filial Juliaca" ya existe. | 1. Login como ADMIN<br>2. Intentar crear sede con nombre duplicado | Se muestra error de constraint violation, sede no se crea, respuesta 400 Bad Request. | P1 | Base de Datos | RNF-11 | Tester |
| Gestión Estructura Académica - Facultades | TC-FAC-001 | Listar todas las facultades | Usuario ADMIN autenticado. Existen facultades en BD. | 1. Login como ADMIN<br>2. Acceder a /facultades<br>3. Verificar lista | Se muestra tabla con todas las facultades, respuesta 200 OK. | P2 | Funcional/API | RF-15 | Tester |
| Gestión Estructura Académica - Facultades | TC-FAC-002 | Obtener facultad por ID | Usuario ADMIN autenticado. Facultad con ID conocido existe. | 1. Login como ADMIN<br>2. Realizar GET /facultades/{id} | Se retorna facultad completa, respuesta 200 OK. | P2 | API | RF-15 | Tester |
| Gestión Estructura Académica - Facultades | TC-FAC-003 | Crear nueva facultad | Usuario ADMIN autenticado. Nombre de facultad único. | 1. Login como ADMIN<br>2. Acceder a /facultades<br>3. Click en "Nueva Facultad"<br>4. Ingresar nombre y descripción<br>5. Click en "Guardar" | Facultad creada en BD, mensaje de éxito, respuesta 201 Created. | P1 | Funcional/API | RF-15 | Tester |
| Gestión Estructura Académica - Facultades | TC-FAC-004 | Actualizar facultad existente | Usuario ADMIN autenticado. Facultad existe en BD. | 1. Login como ADMIN<br>2. Acceder a /facultades<br>3. Seleccionar facultad<br>4. Editar y guardar | Facultad actualizada, cambios reflejados, respuesta 200 OK. | P1 | Funcional/API | RF-15 | Tester |
| Gestión Estructura Académica - Facultades | TC-FAC-005 | Eliminar facultad | Usuario ADMIN autenticado. Facultad existe sin programas asociados. | 1. Login como ADMIN<br>2. Acceder a /facultades<br>3. Eliminar facultad | Facultad eliminada, respuesta 200 OK. | P2 | Funcional/API | RF-15 | Tester |
| Gestión Estructura Académica - Facultades | TC-FAC-006 | Validar unicidad de nombre de facultad | Usuario ADMIN autenticado. Facultad con nombre ya existe. | 1. Login como ADMIN<br>2. Intentar crear facultad con nombre duplicado | Error de constraint violation, facultad no se crea, respuesta 400 Bad Request. | P1 | Base de Datos | RNF-11 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-001 | Listar todos los programas | Usuario ADMIN autenticado. Existen programas en BD. | 1. Login como ADMIN<br>2. Acceder a /programas<br>3. Verificar lista | Se muestra tabla con todos los programas, respuesta 200 OK. | P2 | Funcional/API | RF-16 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-002 | Obtener programa por ID | Usuario ADMIN autenticado. Programa con ID conocido existe. | 1. Login como ADMIN<br>2. Realizar GET /programas/{id} | Se retorna programa completo con facultad asociada, respuesta 200 OK. | P2 | API | RF-16 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-003 | Crear nuevo programa | Usuario ADMIN autenticado. Facultad existe en BD. Nombre único. | 1. Login como ADMIN<br>2. Acceder a /programas<br>3. Click en "Nuevo Programa"<br>4. Seleccionar facultad<br>5. Ingresar nombre y descripción<br>6. Guardar | Programa creado en BD asociado a facultad, mensaje de éxito, respuesta 201 Created. | P1 | Funcional/API | RF-16 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-004 | Actualizar programa existente | Usuario ADMIN autenticado. Programa existe en BD. | 1. Login como ADMIN<br>2. Acceder a /programas<br>3. Editar programa y guardar | Programa actualizado, cambios reflejados, respuesta 200 OK. | P1 | Funcional/API | RF-16 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-005 | Eliminar programa | Usuario ADMIN autenticado. Programa existe sin eventos asociados. | 1. Login como ADMIN<br>2. Acceder a /programas<br>3. Eliminar programa | Programa eliminado, respuesta 200 OK. | P2 | Funcional/API | RF-16 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-006 | Validar unicidad de nombre de programa | Usuario ADMIN autenticado. Programa con nombre ya existe. | 1. Login como ADMIN<br>2. Intentar crear programa con nombre duplicado | Error de constraint violation, programa no se crea, respuesta 400 Bad Request. | P1 | Base de Datos | RNF-11 | Tester |
| Gestión Estructura Académica - Programas | TC-PRO-007 | Validar relación programa-facultad | Usuario ADMIN autenticado. Facultad existe en BD. | 1. Login como ADMIN<br>2. Crear programa asociado a facultad<br>3. Verificar relación | Programa se crea correctamente asociado a facultad, relación se mantiene en BD, respuesta 201 Created. | P1 | Base de Datos | RF-16 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-001 | Listar todos los períodos | Usuario ADMIN autenticado. Existen períodos en BD. | 1. Login como ADMIN<br>2. Realizar GET /periodos | Se retorna lista de todos los períodos, respuesta 200 OK. | P2 | API | RF-17 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-002 | Obtener período por ID | Usuario ADMIN autenticado. Período con ID conocido existe. | 1. Login como ADMIN<br>2. Realizar GET /periodos/{id} | Se retorna período completo, respuesta 200 OK. | P2 | API | RF-17 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-003 | Obtener período activo | Usuario ADMIN autenticado. Existe período con estado ACTIVO. | 1. Login como ADMIN<br>2. Realizar GET /periodos/activo | Se retorna período con estado ACTIVO, respuesta 200 OK. | P1 | API | RF-18 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-004 | Filtrar períodos por estado | Usuario ADMIN autenticado. Existen períodos con diferentes estados. | 1. Login como ADMIN<br>2. Realizar GET /periodos/estado/ACTIVO | Se retorna solo períodos con estado ACTIVO, respuesta 200 OK. | P2 | API | RF-17 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-005 | Crear nuevo período | Usuario ADMIN autenticado. Nombre de período único. | 1. Login como ADMIN<br>2. Realizar POST /periodos con datos válidos | Período creado en BD, mensaje de éxito, respuesta 201 Created. | P1 | Funcional/API | RF-17 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-006 | Actualizar período existente | Usuario ADMIN autenticado. Período existe en BD. | 1. Login como ADMIN<br>2. Realizar PUT /periodos/{id} con datos modificados | Período actualizado, cambios reflejados, respuesta 200 OK. | P1 | Funcional/API | RF-17 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-007 | Eliminar período | Usuario ADMIN autenticado. Período existe sin eventos asociados. | 1. Login como ADMIN<br>2. Realizar DELETE /periodos/{id} | Período eliminado, respuesta 200 OK. | P2 | Funcional/API | RF-17 | Tester |
| Gestión Estructura Académica - Períodos | TC-PER-008 | Validar unicidad de nombre de
