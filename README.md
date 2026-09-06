# Obviously Vulnerable HTML Lab

This repository contains intentionally insecure, dependency-free HTML applications
for local security training and scanner testing.

> **Warning:** Every application in this repository is deliberately vulnerable.
> Run it only on a local machine, never deploy it, and never reuse its code in a
> real application.

## Run locally

From this directory:

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

Then open <http://127.0.0.1:8000>.

Binding to `127.0.0.1` keeps the lab unavailable to other devices on the network.
Most pages also work when opened directly, but the `postMessage` demo is more
reliable through the local server.

## Included applications

| Application | Deliberate vulnerability | Suggested test |
| --- | --- | --- |
| Search | DOM-based XSS via `innerHTML` | Search for `<img src=x onerror=alert('XSS')>` |
| Admin login | Hard-coded credentials and client-side authorization | Inspect source or set `sessionStorage.isAdmin` to `true` |
| Redirector | Unvalidated client-side redirect | Use `?next=https://example.com` |
| Preferences | Sensitive information stored in `localStorage` | Inspect browser storage in developer tools |
| Message center | Origin-free `postMessage` receiver using `innerHTML` | Use the included sender page |

## Purpose

The examples make bad patterns unmistakable so developers can learn to recognize
them. Each page names the vulnerability and briefly identifies the unsafe line.
This is a static front-end lab; it does not model server-side issues such as SQL
injection, SSRF, or broken server authorization.
