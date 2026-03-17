# LorHels Tickets

1. Arquitectura y Tecnologías
Front-end Estático: Un único archivo HTML (index.html) que contiene todo: estructura, estilos y lógica. Es muy fácil de desplegar en cualquier lado.

Estilos y UI:

Tailwind CSS (vía CDN): Utilizado para todo el diseño responsivo (se adapta a móviles y escritorio).

Tema Oscuro (Dark Mode): Implementamos un diseño basado en tonos slate (grises azulados oscuros) con acentos en blue (azul) para botones y enlaces, dándole un aspecto moderno de panel de control (dashboard).

Iconografía: Integración de Lucide Icons (<i data-lucide="..."></i>) para iconos limpios y consistentes en toda la interfaz.

Notificaciones: Uso de SweetAlert2 para modales emergentes y "toasts" (notificaciones pequeñas en la esquina) que confirman acciones sin ser invasivos.

Back-end y Base de Datos:

Firebase SDK: Conectado directamente desde el navegador.

Firestore: Base de datos NoSQL en tiempo real (onSnapshot). Los cambios que haces se reflejan instantáneamente en la pantalla sin tener que recargar.

Firebase Authentication: Manejo de sesiones (anónimas para usuarios normales y con correo/contraseña para el administrador).

2. Funcionalidades Principales
A. Para el Usuario Final (Cliente/Empleado)
Creación de Tickets: Un formulario a la izquierda donde ingresan su nombre, correo, departamento (Ventas, Administración, etc.), asunto, descripción y prioridad.

Vista de Tickets: Una lista central donde pueden ver todos los tickets creados, su estado actual y quién los está atendiendo.

Búsqueda y Filtros: Pueden buscar tickets específicos usando una barra de texto, o usar menús desplegables para filtrar por Estado, Prioridad o Departamento.

B. Para el Administrador (Modo Agente)
Acceso Seguro: Un interruptor (switch) en la esquina superior derecha que, al activarse, lanza un modal de SweetAlert2 pidiendo correo y contraseña de Firebase.

Gestión de Estados: Una vez autenticado, los tickets muestran un botón para avanzar su estado (De "Abierto" a "En Progreso", y luego a "Cerrado").

Detalles Extendidos: Al hacer clic en un ticket, se abre un modal con toda la información. El administrador tiene acceso a una pestaña de "Notas Internas" donde puede escribir comentarios que se guardan con su nombre y fecha.

Eliminación Segura: Capacidad para borrar permanentemente un ticket. Esto incluye una confirmación de seguridad (vía SweetAlert2) para evitar borrados accidentales.

Historial de Cambios: Una pestaña que registra cada vez que un ticket cambia de estado, guardando quién hizo el cambio y cuándo.

3. Estadísticas en Tiempo Real
Un panel superior con 4 tarjetas que se actualizan solas mostrando:

Total de tickets.

Tickets Abiertos (en rojo).

Tickets En Progreso (en amarillo).

Tickets Cerrados (en verde).

4. Seguridad
Reglas de Firestore (Configuradas en la consola): Implementamos reglas estrictas donde cualquier persona puede leer o crear un ticket, pero solo la cuenta con el UID del administrador (tu cuenta) tiene permisos para modificar estados, agregar notas o eliminar documentos en la base de datos.

Sin contraseñas en el código: Eliminamos la contraseña que estaba escrita directamente en el JavaScript, pasando toda la responsabilidad de seguridad al sistema de Firebase Auth.
