---
title: "dialogs"
---

Keikai renders all dialogs, e.g. sheet protection warning, upon templates, so you can modify a dialog's style by changing its template.

# Steps
1. Modify a template

Templates are under `keikai/src/templates/*.pug`

2. compile

run the command below to produce new dialog: (no need to restart Keikai server, only reload the browser page)

`$ ./tool/keikai-cli template`

# Template syntax
The syntax used in a template is from [Pug template engine](https://pugjs.org/api/getting-started.html)
