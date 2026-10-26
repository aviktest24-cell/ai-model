# NOVA AI

NOVA AI is a static, GitHub-ready chat workspace with a professional white interface, direct answers, conversation history, code formatting, publisher logos, live model discovery, and automatic provider fallback.

## Features

- Up to five real model choices: a fast anonymous-compatible text model when listed, plus currently active community text models.
- Lightweight community models are prioritized using model-name hints; active worker counts are shown.
- Real publisher logos are shown beside the model names and in assistant replies when the model family can be identified. Logos use the Simple Icons CDN; an in-repository generic mark is used if a publisher logo is not available.
- Requests use the exact model name selected from the live catalogue. NOVA does not label an answer as coming from a different model without showing the fallback model.
- If the selected model fails, the app tries up to three real alternatives from the current live list.
- A free-tier rate-limit response triggers fallback instead of a broken second GET request. If every backup fails, the fast route is retried once after its reported cooldown.
- Multiple conversations, local history search, delete individual chats, and clear all history with confirmation.
- Copy answers, copy code blocks, copy a whole conversation, and regenerate the latest answer.
- Stop generation, keyboard shortcuts, prompt starter cards, and responsive mobile layout.
- No manual API-key field and no downloaded local model.
- No build step required; plain HTML, CSS, and JavaScript.

## Use locally

1. Download or clone the repository.
2. Open the folder in VS Code or another editor.
3. Run a local static web server (for example, the VS Code Live Server extension).
4. Open the local server URL in a browser and wait for the active model list to load.
5. Choose a model, then send a short test such as `Reply with the word hello.`

Opening `index.html` directly using `file://` may cause browser network restrictions. A local server or HTTPS hosting is recommended.

## Publish on GitHub Pages

1. Upload the contents of this repository to your GitHub repository.
2. Open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select the `main` branch and `/(root)`, then save.
5. Open the Pages URL after deployment completes.

## Model selection and availability

The model list is queried at runtime. The app lists the fast anonymous-compatible text option only when returned by its catalogue, and community text models only when active workers are reported. At most five choices are shown. Model availability and worker counts change over time. Free/anonymous routes have limits and are not guaranteed to be unlimited. When the fast route returns a rate-limit response, NOVA tries currently active backup models and does not call the obsolete legacy GET route. If every route is unavailable, refresh the model list or retry after the provider cooldown. When the fast anonymous model returns HTTP 402, NOVA immediately tries live community-worker backups; if all backups also fail, it waits for the reported cooldown and retries the fast POST route once. It never tries the legacy GET route that returned 404 for unsupported model IDs.

Publisher logos are brand marks for the model publisher, not a claim that the publisher operates the community workers. Images load from the Simple Icons CDN and therefore require an internet connection; an in-repository generic icon is used as a fallback.

## Privacy

Conversation history and the selected model are stored in this browser's local storage. They do not sync between devices. Prompts are sent to the selected external inference route, with community-worker fallback when available. Do not submit passwords, private keys, or other sensitive information.

## Repository structure

```text
index.html
app/
  main.js
components/
  chat-view.js
hooks/
  chat-controller.js
lib/
  model-catalog.js
  providers.js
  markdown.js
  storage.js
public/
  favicon.svg
  logos/
    model-generic.svg
styles/
  app.css
```
