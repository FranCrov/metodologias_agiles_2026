# **Ejercicio 18 – Scrum con IA**

**Proyecto:** Sistema de Gestión de Inventario para un comercio  
**Contexto general:** Una pequeña empresa comercial necesita digitalizar el control de su stock. El sistema debe permitir registrar productos, actualizar cantidades, emitir alertas de reposición y generar reportes de movimiento.

---

## **Prompt 1 – Product Owner: Creación del Product Backlog**

### **Prompt desarrollado**

Rol: Eres un Product Owner experimentado en metodología Scrum.

Contexto: El proyecto es un Sistema de Gestión de Inventario para una   
comercio con \~20 empleados. El sistema debe permitir: registrar productos con   
código, nombre, categoría y precio; controlar stock con entradas y salidas;   
emitir alertas automáticas cuando el stock mínimo se alcance; y generar reportes   
de movimiento mensual. El equipo de desarrollo tiene 3 personas y trabaja en   
Sprints de 2 semanas.

Tarea: Crea un Product Backlog inicial con al menos 10 User Stories priorizadas   
usando el formato "Como \<usuario\> quiero \<acción\> para que \<objetivo\>".   
Incluye criterios de aceptación para cada historia y una estimación relativa   
(S/M/L).

Formato de respuesta: Tabla Markdown con columnas: ID | User Story | Criterios de Aceptación | Tamaño | Prioridad (Alta/Media/Baja).

### **Resultado de la aplicación**

| ID | User Story | Criterios de Aceptación | Tamaño | Prioridad |
| ----- | ----- | ----- | ----- | ----- |
| US-01 | Como administrador quiero registrar un producto con código, nombre, categoría y precio para poder identificarlo unívocamente en el sistema | El producto se guarda con todos sus campos; el código es único; se muestra mensaje de confirmación | S | Alta |
| US-02 | Como operario quiero registrar una entrada de stock indicando cantidad y proveedor para mantener el inventario actualizado | El stock aumenta correctamente; queda registro con fecha y usuario | M | Alta |
| US-03 | Como operario quiero registrar una salida de stock con motivo (venta/uso interno) para reflejar el consumo real | El stock disminuye; no permite salida mayor al stock disponible; queda trazabilidad | M | Alta |
| US-04 | Como administrador quiero definir un stock mínimo por producto para configurar el umbral de alerta de reposición | El campo stock mínimo se puede establecer y editar por producto | S | Alta |
| US-05 | Como administrador quiero recibir una alerta cuando el stock de un producto baje del mínimo configurado para poder reabastecer a tiempo | La alerta aparece en el dashboard y se envía por email; no se duplica si ya existe | M | Alta |
| US-06 | Como gerente quiero ver un reporte de movimientos del mes actual filtrado por producto o categoría para analizar el consumo | El reporte muestra entradas, salidas y saldo; es exportable a PDF/Excel | L | Alta |
| US-07 | Como administrador quiero buscar productos por nombre o código para encontrarlos rápidamente | La búsqueda devuelve resultados en tiempo real (\< 1 s); soporta búsqueda parcial | S | Media |
| US-08 | Como administrador quiero gestionar categorías de productos para organizar el catálogo | Se pueden crear, editar y desactivar categorías; no se elimina una con productos asociados | S | Media |
| US-09 | Como gerente quiero ver un dashboard con los indicadores clave (productos con bajo stock, total de movimientos del día) para tener visibilidad rápida del inventario | El dashboard carga en \< 2 s; los datos se actualizan al refrescar la página | M | Media |
| US-10 | Como administrador quiero gestionar usuarios con roles (administrador, operario, gerente) para controlar el acceso a las funciones del sistema | Cada rol ve solo las secciones habilitadas; el acceso se aplica inmediatamente tras guardar | L | Baja |

## **Prompt 2 – Scrum Master: Facilitación del Sprint Planning**

### **Prompt desarrollado**

Rol: Eres un Scrum Master certificado que facilita el Sprint Planning de un   
equipo de desarrollo.

Contexto: El equipo tiene 3 desarrolladores (capacidad total: 90 puntos de   
historia por Sprint de 2 semanas). La velocidad histórica es de 75 puntos.   
El Product Backlog priorizado incluye las US-01 a US-10 del sistema de   
inventario descritas anteriormente. Las US de alta prioridad son: US-01 (S=3),   
US-02 (M=5), US-03 (M=5), US-04 (S=3), US-05 (M=8), US-06 (L=13).

Tarea: Facilita el Sprint Planning del Sprint 1\. Define el Sprint Goal,   
selecciona las User Stories que entran al Sprint (respetando la velocidad),   
desglosa las US seleccionadas en tareas técnicas y asígnalas a los   
desarrolladores (Dev1: backend, Dev2: frontend, Dev3: full-stack).

Formato de respuesta:   
1\. Sprint Goal (1 oración)    
2\. Sprint Backlog: tabla con US , Tareas , Responsable , Estimación (en horas)    
3\. Capacidad utilizada vs disponible

### **Resultado de la aplicación**

**1\. Sprint Goal**

Permitir el registro completo de productos y el control básico de entradas y salidas de stock, garantizando la trazabilidad de cada movimiento.

**2\. Sprint Backlog – Sprint 1**

| US | Tarea | Responsable | Horas |
| ----- | ----- | ----- | ----- |
| US-01 | Diseñar modelo de datos (tabla productos) | Dev1 | 3 |
| US-01 | Crear endpoint REST POST /productos | Dev1 | 4 |
| US-01 | Crear formulario de alta de producto | Dev2 | 5 |
| US-01 | Validaciones de campo único en código | Dev1 | 2 |
| US-02 | Endpoint POST /movimientos (entrada) | Dev1 | 4 |
| US-02 | Pantalla de registro de entrada con selector de proveedor | Dev2 | 5 |
| US-02 | Actualización automática de stock al registrar entrada | Dev3 | 3 |
| US-03 | Endpoint POST /movimientos (salida) con validación de stock | Dev1 | 5 |
| US-03 | Pantalla de registro de salida con selector de motivo | Dev2 | 4 |
| US-03 | Control de concurrencia (evitar stock negativo) | Dev3 | 4 |
| US-04 | Campo stock\_minimo en modelo \+ endpoint PATCH /productos/:id | Dev1 | 3 |
| US-04 | Input de stock mínimo en formulario de producto | Dev2 | 2 |

**3\. Capacidad**

| Concepto | Puntos |
| ----- | ----- |
| Velocidad de referencia | 75 pts |
| Puntos seleccionados (US-01+02+03+04) | 16 pts (3+5+5+3) |
| Capacidad en horas (3 devs × 10 días × 6 h efectivas) | 180 h |
| Horas planificadas | 44 h |
| Margen disponible para imprevistos | 136 h → reserva para US-05 si avanza bien |

## **Prompt 3 – Equipo de Desarrollo: Daily Scrum simulado**

### **Prompt desarrollado**

Rol: Simula a tres desarrolladores de software (Dev1-backend, Dev2-frontend,   
Dev3-full-stack) en el contexto de un Daily Scrum del día 3 del Sprint 1\.

Contexto: El equipo trabaja en un Sistema de Gestión de Inventario para un comercio .   
El Sprint Goal es: "Permitir el registro completo de productos y el control   
básico de entradas y salidas de stock". Al día 2, Dev1 terminó el modelo de   
datos y el endpoint de alta; Dev2 tiene el formulario de productos al 80%;   
Dev3 aún no comenzó su tarea de actualización de stock.

Tarea: Simula el Daily Scrum del día 3 con las 3 preguntas estándar para   
cada desarrollador. Incluye al menos un impedimento real y cómo el Scrum   
Master debería gestionarlo fuera del daily.

Formato de respuesta: Diálogo breve por desarrollador y una sección con impedimentos y acciones al final.

### **Resultado de la aplicación**

**Daily Scrum – Día 3 – Sprint 1**

---

**Dev1 (Backend):**  
✅ Ayer: Completé el endpoint POST /movimientos para entradas y salidas, con validación de stock disponible.  
🎯 Hoy: Voy a implementar el campo stock\_mínimo y el PATCH de actualización de producto.  
🚧 Impedimento: Ninguno por ahora.

---

**Dev2 (Frontend):**  
✅ Ayer: Terminé el formulario de alta de producto al 100% y lo integré con el endpoint de Dev1.  
🎯 Hoy: Empiezo la pantalla de registro de entradas.  
🚧 Impedimento: El diseño de la pantalla de salidas no está definido. No sé si usar un modal o una página separada. Necesito una decisión del PO.

---

**Dev3 (Full-stack):**  
✅ Ayer: Estuve revisando la lógica de concurrencia para evitar stock negativo; encontré un edge case cuando dos salidas se procesan simultáneamente.  
🎯 Hoy: Voy a implementar un bloqueo optimista a nivel de base de datos para resolverlo.  
🚧 Impedimento: No tengo acceso al entorno de staging para probar la concurrencia. Se lo pedí a IT ayer pero no respondieron.

---

**Impedimentos y acciones (post-Daily – Scrum Master)**

| \# | Impedimento | Responsable de resolución | Acción | Deadline |
| ----- | ----- | ----- | ----- | ----- |
| 1 | Dev2 no tiene definición de UI para pantalla de salidas | Scrum Master → escalar a PO | Agendar reunión de 15 min con PO hoy a las 11:00 | Mismo día |
| 2 | Dev3 sin acceso a staging | Scrum Master → contactar IT | Enviar mail formal a IT con urgencia; si no responde en 2 h, escalar al sponsor | Antes de las 16:00 |

### **Técnica utilizada**

**Persona prompting \+ escenario contextualizado:** Se asignaron tres personas distintas con roles diferentes dentro del mismo prompt. Proveer el estado exacto al día 2 permite que la IA genere respuestas coherentes y no contradictorias entre desarrolladores. La instrucción explícita de incluir un impedimento real activa razonamiento de situaciones de bloqueo típicas en proyectos de software, generando salidas más útiles que pedir un "daily genérico".

---

## **Prompt 4 – Sprint Review: Demostración y feedback del cliente**

### **Prompt desarrollado**

Rol: Eres el Scrum Master facilitando una Sprint Review al final del Sprint 1\.   
Los participantes son: el equipo de desarrollo, el Product Owner y el cliente   
(dueño del comercio).

Contexto: El Sprint 1 duró 2 semanas. Se completaron US-01, US-02, US-03 y   
US-04. No se completó US-05 (alertas de reposición) porque tomó más tiempo del esperado. El incremento funciona en el entorno de demo.

Tarea: Redacta el script de la Sprint Review con:   
(a) apertura del Scrum Master,    
(b) demo de cada US completada (qué muestra cada dev),    
(c) preguntas del cliente y respuestas del equipo,    
(d) ajustes al Product Backlog propuestos por el cliente,    
(e) cierre con acuerdos.

Formato de respuesta: Script con hablantes identificados.   
Máximo 400 palabras.

### **Resultado de la aplicación**

**\[Scrum Master\]:** Bienvenidos a la Sprint Review del Sprint 1\. El objetivo de hoy es inspeccionar el incremento construido y adaptar el backlog según el feedback. Completamos 4 de 5 historias; US-05 (alertas) pasa al Sprint 2\. Empecemos la demo.

**\[Dev1\]:** Muestro el registro de productos. Aquí creamos un artículo nuevo: código "ART-001", categoría "Electrónica", precio $1500, stock mínimo 10 unidades. El sistema valida que el código no se repita. *(demo en vivo)*

**\[Dev2\]:** Ahora registro una entrada de 50 unidades para ART-001, indicando el proveedor. El stock pasa de 0 a 50 y queda registrado con fecha y usuario. *(demo en vivo)*

**\[Dev3\]:** Por último, registro una salida de 5 unidades por "Venta". El stock baja a 45\. Si intento sacar 100 unidades, el sistema lo rechaza con un mensaje de error claro. *(demo en vivo)*

**\[Cliente\]:** Muy bien. ¿Puedo hacer una búsqueda de producto por nombre? Necesito encontrarlos rápido cuando tengo un cliente esperando.

**\[Product Owner\]:** Eso es US-07 del backlog, con prioridad Media. ¿Lo subimos a Alta para el Sprint 2?

**\[Cliente\]:** Sí, definitivamente. Y otra cosa: ¿el sistema avisa cuando el stock baja? Eso es lo que más necesito.

**\[Scrum Master\]:** US-05 (alertas) ya está planificada para Sprint 2 como Alta prioridad. La concurrencia fue la causa del retraso; ya está resuelta.

**\[Cliente\]:** Perfecto. También quiero que la alerta llegue a mi celular por WhatsApp, no solo por email.

**\[Product Owner\]:** Entendido, agrego US-11: "Como gerente quiero recibir alertas de bajo stock por WhatsApp para actuar desde cualquier lugar". Lo evaluamos para Sprint 3\.

**\[Scrum Master\]:** Acordamos: (1) US-07 sube a prioridad Alta para Sprint 2, (2) US-05 entra al Sprint 2, (3) US-11 (WhatsApp) se agrega al backlog para Sprint 3\. ¿Conforme?

**\[Cliente\]:** Conforme. Buen trabajo.

## **Prompt 5 – Sprint Retrospective: Mejora continua del equipo**

### **Prompt desarrollado**

Rol: Eres un Scrum Master facilitando una Sprint Retrospective usando la   
técnica MAD / GLAD / SAD con el equipo de desarrollo (3 personas).

Contexto: Sprint 1 finalizado. Hechos relevantes del sprint:  
\- Se resolvió un bug complejo de concurrencia que no estaba planificado (+4 h)  
\- El acceso a staging llegó tarde (día 7 de 10\)  
\- La comunicación con el PO para definir la UI de salidas tardó 1 día  
\- El equipo logró integrar frontend y backend sin conflictos de merge  
\- La demo fue bien recibida por el cliente

Tarea: Simula la retro con al menos 2 ítems por categoría (MAD/GLAD/SAD),   
luego define 3 acciones de mejora concretas con responsable y fecha límite.

Formato de respuesta:  
\- Tabla MAD / GLAD / SAD  
\- Tabla de acciones de mejora

### **Resultado de la aplicación**

**Tabla MAD / GLAD / SAD**

| Categoría | Ítem |
| ----- | ----- |
| 😡 MAD | El acceso a staging llegó en el día 7; perdimos tiempo de testing en entorno real |
| 😡 MAD | Tuvimos que esperar 1 día para que el PO definiera la UI de la pantalla de salidas |
| 😊 GLAD | Resolvimos el edge case de concurrencia sin impactar la calidad final |
| 😊 GLAD | La integración frontend–backend fue limpia; cero conflictos de merge |
| 😊 GLAD | La demo impresionó al cliente y generó feedback valioso (nueva US de WhatsApp) |
| 😢 SAD | US-05 (alertas) no entró al Sprint por el retraso no planificado |
| 😢 SAD | No teníamos un canal claro para escalar bloqueos a IT con urgencia |

**Acciones de mejora**

| \# | Acción | Responsable | Fecha límite |
| ----- | ----- | ----- | ----- |
| 1 | Solicitar acceso a staging al inicio de cada Sprint (día 1), no cuando se necesite | Scrum Master | Inicio Sprint 2 |
| 2 | Agregar slot fijo de 30 min con el PO los lunes para resolver dudas de UI/UX antes de que bloqueen al equipo | Scrum Master \+ PO | Sprint 2 semana 1 |
| 3 | Crear canal de Slack "\#impedimentos-it" para escalar bloqueos de infraestructura con SLA de 2 horas | Scrum Master | Antes del Daily del lunes |

