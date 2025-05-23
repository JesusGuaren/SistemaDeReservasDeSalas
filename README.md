Corrección de Diagramas UML – Sistema de Reserva de Salas
Nombre: Francisco Zamorano y Jesús Vidal
Sección: [1, Jesús es de la segunda pero el dia de hoy 23 de mayo Jesús se ingreso a la seccion 1 por el dia de hoy]
Fecha: 23 de mayo de 2025
# 1. Diagrama de Casos de Uso
![CasodeUso](https://github.com/user-attachments/assets/cf829e9b-d80e-4b9f-894a-e5b59dc2ed5c)

## Error 1
- **Error identificado:** 'Agregar motivo de cancelación' está mal conectado a 'Cancelar reserva'.
  - **Justificación:** Debe usarse <<extend>> porque es opcional.
  - **Corrección propuesta:** Cambiar a <<extend>> y definir un punto de extensión.
## Error 2
- **Error identificado:** 'Consultar disponibilidad externa' está como caso de uso independiente.
  - **Justificación:** No tiene actor que lo inicie, es un subproceso técnico.
  - **Corrección propuesta:** Incluirlo como <<include>> dentro de 'Reservar sala'.
## Error 3
- **Error identificado:** 'Notificar cambio por correo' se muestra como caso de uso principal.
  - **Justificación:** Es parte de otros procesos, no una acción directa de un actor.
  - **Corrección propuesta:** Incluirlo como <<include>> en 'Aprobar', 'Rechazar' o 'Cancelar reserva'.
# 2. Diagrama de Clases
![ClasesDiagama](https://github.com/user-attachments/assets/8cd6d0b2-f992-4286-b37e-96cbed37342d)

## Error 1
- **Error identificado:** Administrador no hereda de Usuario.
  - **Justificación:** Ambos comparten atributos y un admin es un tipo de usuario.
  - **Corrección propuesta:** Establecer herencia: Administrador generaliza desde Usuario.
## Error 2
- **Error identificado:** GestorNotificaciones tiene métodos por cada tipo (correo y SMS).
  - **Justificación:** No sigue Bridge; debe delegar a una interfaz común.
  - **Corrección propuesta:** Usar interfaz Notificador y que cada tipo implemente 'notificar()'.
## Error 3
- **Error identificado:** Reserva no está asociada a Usuario ni a Sala.
  - **Justificación:** Pierde sentido de a quién pertenece y qué sala reserva.
  - **Corrección propuesta:** Agregar relaciones con multiplicidades adecuadas.
# 3. Diagrama de Implementación
![diagramaImplementacion](https://github.com/user-attachments/assets/5ace628f-39cb-4fbc-b6ed-fa33f46b5851)

## Error 1
- **Error identificado:** No aparece Adaptador para la API externa.
  - **Justificación:** El Adapter debe estar explícito como capa intermedia.
  - **Corrección propuesta:** Agregar componente AdaptadorDisponibilidad conectado a API.
## Error 2
- **Error identificado:** NotificadorCorreo y SMS están fuera del servidor.
  - **Justificación:** Son clases internas, no servicios externos.
  - **Corrección propuesta:** Moverlas al Servidor Web y conectar a un sistema externo único.
## Error 3
- **Error identificado:** GestorNotificaciones está mal ubicado o sin nodo.
  - **Justificación:** Debe estar dentro del Servidor Web y conectado explícitamente.
  - **Corrección propuesta:** Dibujarlo dentro del nodo y etiquetar conexiones (ej. <<HTTP>>, <<SMTP>>).
