# Bitácora

## Ejercicio 0 — ¿HTTP o WebSocket?

### Pregunta
Para cada acción, ¿por dónde viaja y por qué: pedir entrar, aceptar a alguien, mandar un mensaje y preguntar la dirección del túnel?

### Respuesta
- **Pedir entrar:** va por **HTTP**, porque quien pide entrar todavía no tiene token y no puede abrir el WebSocket.
- **Aceptar a alguien:** va por el **WebSocket del anfitrión**, porque ya está abierto y autenticado.
- **Mandar un mensaje:** va por **WebSocket**, porque el mensaje debe llegar a todos al instante.
- **Preguntar la dirección del túnel:** va por **HTTP**, porque es una pregunta que recibe una respuesta y solo se realiza una vez.

---

## Ejercicio D1 — ¿Cómo lo arreglarías?

### Pregunta
Cada callback recibe el `webSocket` que lo dispara. ¿Qué tendría que comprobar antes de tocar el estado?

### Respuesta
Debe comprobar que ese `webSocket` sea el **actual** antes de modificar el estado. Se debe comparar la identidad del objeto, no su igualdad.

Por ejemplo:

```kotlin
if (webSocket !== actual) return