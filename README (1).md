# 🤖 Asistente de portafolio con IA (n8n + Gemini)

Agente conversacional construido con **n8n** que responde preguntas sobre mi perfil profesional, proyectos y habilidades, y que **me avisa por correo** cuando alguien muestra interés en contratarme.

## ¿Qué hace?

1. Recibe un mensaje a través del chat de n8n.
2. Un **AI Agent** (Google Gemini) responde usando la información de mi perfil definida en el *system message*.
3. Si detecta interés en contratarme, usa la herramienta de **Gmail** para enviarme un resumen del contacto.

## Arquitectura

```
Chat Trigger  →  AI Agent  ←  Google Gemini Chat Model
                    ↑
                Gmail Tool (envía el aviso)
```

| Componente | Nodo de n8n | Función |
|---|---|---|
| Entrada | `Chat Trigger` | Recibe los mensajes del usuario |
| Cerebro | `AI Agent` + `Google Gemini Chat Model` | Razona y decide cuándo usar la herramienta |
| Acción | `Gmail Tool` (Send a message) | Envía el correo de aviso, con asunto y mensaje generados por la IA |

## Tecnologías

- n8n (autoalojado con Docker)
- Google Gemini API (capa gratuita)
- Gmail API (OAuth2)

## Cómo usarlo

1. Levanta n8n con Docker:
   ```bash
   docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
   ```
2. Abre `http://localhost:5678` e importa `agente-ia-portafolio.json` (*Workflows → Import from file*).
3. Crea tus propias credenciales:
   - **Google Gemini**: API key gratuita en [aistudio.google.com/apikey](https://aistudio.google.com/apikey).
   - **Gmail OAuth2**: cliente OAuth creado en Google Cloud Console.
4. En el nodo **Gmail**, cambia el campo *To* por tu correo.
5. Edita el *System Message* del AI Agent con tu propio perfil.
6. Abre el chat y escribe, por ejemplo: *"¿Qué proyectos tiene Yeimi?"*

> 🔒 El archivo JSON no incluye claves ni tokens. Cada persona debe configurar sus propias credenciales.

## Aprendizajes

- Diseño de agentes con herramientas (*tool calling*) en n8n.
- Configuración de OAuth2 con Google Cloud y manejo de usuarios de prueba.
- Prompt engineering para definir el comportamiento y el contexto del agente.

## Próximas mejoras

- [ ] Agregar memoria de conversación (Simple Memory).
- [ ] Publicar el chat con una URL pública.
- [ ] Guardar los contactos en Google Sheets.

## Autora

**Yeimi Ortega** · [LinkedIn](https://linkedin.com/in/yeimi-ortega-666552381) · [GitHub](https://github.com/yeimiortega)
