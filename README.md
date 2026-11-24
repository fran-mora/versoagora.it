# versoagora.it

Website of the association Verso l'Agorà APS. A static site served by GitHub Pages from the `main` branch: every push to `main` goes live.

## How the content is organised

Everything is in `index.html`, except three kinds of content that change often. Those live in JSON files in `data/`, and a script at the bottom of `index.html` reads them and builds the matching sections when the page loads.

| File | Section of the page |
| --- | --- |
| `data/eventi.json` | "In programma" (events from today onwards) and "Eventi Pubblici" (all public events) |
| `data/attivita.json` | "Attività Svolte": the groups and their cards |
| `data/foto.json` | The scrolling photo strip |

Rules the script applies to events:

- An event is listed under "In programma" while its date is today or later (Italian time), soonest first. It drops out by itself the day after. With no upcoming events a short message is shown instead.
- "Eventi Pubblici" lists every event of type `pubblico`, newest first. Events with no date go last, in file order.
- Events of type `soci` only ever appear under "In programma".

Images are stored in `images/` and referenced as `images/name.jpg`.

## Editing without touching the code

The files in `data/` are edited through [Pages CMS](https://pagescms.org), a free editor that shows them as forms and saves each change as a commit to this repository. Its forms are defined in `.pages.yml`.

- Editor: <https://app.pagescms.org>, signing in with a GitHub account that has access to this repository.
- People without a GitHub account can be invited by email from the "Collaborators" page of the editor. They can edit content and upload images, nothing else.
- To make something else editable, move it into a file in `data/`, render it from the script in `index.html`, and describe its fields in `.pages.yml`.

Anything not listed above (texts, layout, colours, new sections) is changed directly in `index.html`.

## Previewing locally

The page loads the data files with `fetch`, so it has to be opened through a local server rather than by double-clicking the file:

```
python3 -m http.server 8000
```

then open <http://localhost:8000>.
