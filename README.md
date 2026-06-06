# LorHels Tickets

## LorHels Tickets: Arquitectura y Funcionalidades Principales

**LorHels Tickets** es una aplicación web de página única (SPA) diseñada para la gestión de solicitudes de soporte técnico en tiempo real. Combina un diseño moderno y responsivo con un backend serverless, garantizando velocidad y seguridad.

### 1. Stack Tecnológico

* **Frontend Estático:** HTML5 y Vanilla JavaScript (ES6+), operando sin depender de frameworks complejos.
* **Motor de Estilos:** Tailwind CSS configurado con un tema oscuro profesional (paleta *Slate* y *Blue*).
* **Iconografía e Interfaz:** Lucide Icons para la representación gráfica minimalista y SweetAlert2 para notificaciones emergentes (toasts) y modales de confirmación interactivos.
* **Backend (BaaS):** Firebase SDK (v12.4.0).
* **Base de Datos:** Cloud Firestore, utilizando listeners (`onSnapshot`) para sincronización bidireccional en tiempo real.
* **Autenticación:** Firebase Auth, implementando un sistema híbrido de sesiones anónimas (para creadores de tickets) y credenciales de correo/contraseña (para gestión administrativa).



### 2. Experiencia del Usuario Final (Cliente/Empleado)

* **Generación de Solicitudes:** Formulario intuitivo que captura nombre, correo electrónico, departamento (Ventas, Administración, Tráfico, etc.), asunto, descripción detallada y nivel de prioridad.
* **Panel de Control en Vivo:** Lista centralizada de tickets que se renderiza y actualiza instantáneamente en todos los clientes conectados sin necesidad de recargar la página.
* **Filtros y Búsqueda Avanzada:** Barra de texto unificada para buscar por ID, nombre del solicitante o contenido, complementada con menús desplegables para aislar tickets por Estado, Prioridad y Departamento.
* **Dashboard Estadístico:** Tarjetas de métricas dinámicas en la parte superior que reflejan el volumen total de operaciones y su distribución actual (Abiertos, En Progreso, Cerrados).

### 3. Módulo de Administración (Agente)

* **Acceso Protegido:** Un interruptor de "Modo Administrador" en la cabecera que despliega un modal de autenticación segura enlazado a Firebase Auth.
* **Gestión del Ciclo de Vida:** Controles de un solo clic para avanzar el estado operativo del ticket (Abierto $\rightarrow$ En Progreso $\rightarrow$ Cerrado).
* **Auditoría e Historial:** Registro inmutable, integrado en el modal de detalles, que documenta qué usuario modificó un estado y en qué momento exacto (con formato local).
* **Colaboración Interna:** Capacidad de agregar "Notas Internas" privadas (visibles de forma exclusiva bajo la sesión de administrador), selladas con el nombre del agente y la marca de tiempo.
* **Depuración de Datos:** Función de eliminación permanente de registros en Firestore, protegida por una barrera de confirmación visual para prevenir borrados accidentales.

### 4. Seguridad e Integridad de Datos

* **Reglas de Firestore en la Nube:** Los usuarios estándar (sesión anónima) poseen privilegios exclusivos de lectura y creación. Únicamente el UID criptográfico específico del administrador cuenta con permisos de actualización (estados/notas) y eliminación en el servidor.
* **Protección de Interfaz (Cliente):** Lógica condicional en JavaScript que oculta proactivamente botones destructivos, opciones de estado y formularios de notas si la sesión validada de administrador no se encuentra activa.
* **Diseño Interactivo y Limpio:** Elementos estructurales como el ID del documento se truncan visualmente y los datos de conexión se manejan en segundo plano, finalizando con un pie de página corporativo enlazado directamente a LorHels Systems.
