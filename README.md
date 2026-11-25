# Panel de correo con agentes

Un agente principal revisa el correo de Outlook (Microsoft 365), detecta pendientes, tareas, correos sin responder o para derivar, y los clasifica en:

- **Autónomas**: el agente las prepara solo.
- **En conjunto**: el agente prepara y Victor decide o completa.
- **Directas**: las hace Victor personalmente.

Para ejecutarlas usa subagentes especializados: un **redactor** que escribe con el estilo de Victor (aprendido de la carpeta Enviados) y un **operador web** que usa Claude en Chrome para plataformas y paneles.

## Dos formas de usarlo

### 1. Panel web (claude.ai)
`panel/index.html` es el panel publicado como Artifact. Usa el conector Microsoft 365 y Claude desde la propia página:

- **Actualizar correo**: lee los últimos 50 correos de la bandeja y los 25 últimos enviados, y el agente principal los clasifica.
- **Ejecutar autónomas**: el redactor crea borradores en Outlook; el operador web prepara la instrucción para Claude en Chrome.
- En cada tarjeta: redactar respuesta, preparar derivación (pide confirmación antes de reenviar), instrucción web, mover de categoría, marcar hecha.
- **Mi estilo de escritura**: la guía que usa el redactor; se puede corregir.

El estado se guarda en un espacio privado por usuario. Nada se envía sin una confirmación explícita.

### 2. Claude Code + Claude en Chrome
- `/revisar-correo`: el agente principal, con el mismo flujo.
- `.claude/agents/redactor-correos.md`: el subagente redactor.
- `.claude/agents/operador-web.md`: el subagente que navega con la extensión Claude en Chrome (`claude --chrome`).

Opcional: crea un archivo `estilo.md` en la raíz con tu guía de estilo para que el redactor la use directamente.
