# Project Approach

Using software development to finish dull tasks.

---
layout: center
---

# The Dull Tasks

- Resume writing
- Job search
- Paying bills

---
layout: fact
---

# Done

Unlike traditional software, dull tasks have a clear finish line.

---
layout: image-right
image: /resume-v0001-2018.png
---

# Case Study

<codicon-github-project /> `CodeMan99/ctaylor-resume`

Project used to generate my **resume.pdf**

Screenshot of an early iteration <bi-arrow-right />

---

# Why DIY

Various reasons why I rolled my own solution.

- Tired of fighting with Microsoft Office styling.
- Wanted a file format that could convert easily.

---

# Tips: Getting Started

- Prefer to start with existing solutions.
- Focus on getting to done quickly.
- Choose familiar tech.
- Operate in plain text.

<!--
Often the hardest part of any project is just getting started.
-->

---

# Action: Project Start

<vscode-icons-file-type-pug />

My resume project started with **Pug** templates.

```
doctype html
head
  title Example
body
  main.container
    p I like Pug templates
```

By leaning on the `pug` CLI, I was able to get to _done_ almost instantly.

<!--
I did learn CSS `display: flex` which I leverage for the column output
-->

---

# Tips: Continue Learning

<bi-journal-bookmark-fill />

- Helps to keep the project feeling fresh.
- A sandbox to freely make mistakes.

<!--
Making mistakes is very benefinial to learning.
-->

---

# Action: Replace Pug CLI

The Pug CLI was eventually deprecated.

This forced my hand in writing my own.

What I learned is that parsing option flags doesn't have to be hard.

<!--
Reminder that files starting with a shell bang line should **not** have an extension.
-->

---

# Action: Add Devcontainer

A devcontainer is a docker wrapper.

A bit of an experiment at the time.

Now my favorite way to create a development environment.

---

# Action: Add Build Watch

Tools to enable hot reload of my build

`inotify` - <codicon-bell /> Watch source files to build on change.

`reload` - <codicon-refresh /> Watch output files to reload web browser.

```
#!/usr/bin/env bash

FILENAME="resume.pug"

printf "Watching %s.\n" "$FILENAME"
./generate && npm exec -c "reload --start-page resume.html" &
while inotifywait -e close_write "$FILENAME"; do ./generate; done
```

<!--
Simple and effective.

Shell script.

A little wonky because there may have been some race conditions. A manual reload of the browser typically was enough.
-->

---

# Action: Use GH Actions

<devicon-githubactions />

Use of Github Actions allowed me to offload concerns.

This enabled meaningful edits while away from my development machine.

<!--
First solution was to store the rendered PDF as a _build artifact_.

Made use of LukaszLapaj/html-to-pdf-action@e4d6f4f8d68d7a69b8a096613336f9b1edd4b314
-->

---

# Failure: Delivery as OCI Artifact

The goal here was to allow distribution of my resume publically.

- Announced it on LinkedIn.
- Added to my Github profile.
- Over the last 5 months I received roughly 15 downloads.

<!--
Named: ghcr.io/codeman99/resume:latest

The boon is that I understand OCI Artifacts now!
-->

---

# Action: Reload Server

I decided to re-write the `reload` server for learning.

- Able to combine file watching!
- Had fun writing a WebSocket server (node)
- Had fun writing a WebSocket client (browser)

---

# Action: Local CD, Part I

<vscode-icons-file-type-htmlvalidate /> <bi-caret-right /> <vscode-icons-file-type-pdf2 />

I deperately wanted to replace the _HTML to PDF_ action I choose.

```
LukaszLapaj/html-to-pdf-action@e4d6f4f8d68d7a69b8a096613336f9b1edd4b314
```

See that commit hash? It means that my action has to build the container image.

---

# Action: Local CD, Part II

<bi-patch-exclamation /> Replacing this action took a bit of planning.

Reading the original action, revealing that it made use of

- <devicon-docker /> Docker
- <devicon-nodejs /> A `serve-static` node server
- <devicon-puppeteer /> Puppeteer
- <devicon-chrome /> A manual `apt-get install` of Chrome in the Docker image

<style>
    ul { list-style-type: none; }
    li { margin-left: 0; }
</style>

---

# Action: Local CD, Part III

I stopped developing for a moment to look broadly at other solutions. <bi-pause-circle />

### What I found is the _Reactive Resume_ project!

Achieves a lot of my personal goals.

- Simple text input
- Render to HTML
- Export / Print to PDF

The PDF bit was a perfect fit for what I needed next.

---

# Action: Local CD, Part IV

Plan was in place!

1. Replace Docker with a devcontainer. ...Yes, that's still just docker.
2. Replace `serve-static` with an alpine-based `nginx` container.
3. Learn puppeteer!
4. Replace Chrome with the `ghcr.io/browserless/chromium` image.

Lesson Learned: The fastest docker build? No build!

---

# Action: Local CD, Part V

<codicon-home /> Finally! Creating a PDF locally both looks good and is automated!

Now I just call `./print-pdf` and I receive a fully optimized `resume.pdf`.

---

# What About Github

<codicon-github-inverted />

Don't worry! I now have `devcontainer/ci` action that can execute anything!

---
layout: image
image: /resume-v0002-2024.png
backgroundSize: contain
title: Project Screenshot
---

<!-- Explain development -->

---

# Other Resume Solutions

Don't want to roll your own?

![QR Code containing Reactive Resume URL](/reactive-resume-qrcode.png)
Reactive Resume &mdash; [https://rxresu.me](https://rxresu.me/)

---
layout: two-cols
---

![QR Code containing LinkedIn URL](/codeman99-linkedin-qrcode.png)
[linkedin.com/in/codeman99/](https://www.linkedin.com/in/codeman99/)

::right::

![QR Code containing Github URL](/codeman99-github-qrcode.png)
[github.com/CodeMan99](https://github.com/CodeMan99)
