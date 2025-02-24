<h2 align="center">Hola 👋! Mi nombre es Angel.</h2>

###

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs?username=LuxuzDev&locale=es&hide_title=true&layout=compact&card_width=320&langs_count=5&theme=github_dark&hide_border=true" height="150" alt="languages graph"  />
  <img src="https://streak-stats.demolab.com?user=LuxuzDev&locale=es&mode=daily&theme=github_dark&hide_border=false&border_radius=5" height="150" alt="streak graph"  />
</div>

###

<br clear="both">

<img src="https://raw.githubusercontent.com/LuxuzDev/LuxuzDev/output/snake.svg" alt="Snake animation" />

###

<div align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/csharp/csharp-original.svg" height="40" alt="csharp logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" height="40" alt="github logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" height="40" alt="postgresql logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-plain.svg" height="40" alt="java logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/unity/unity-original.svg" height="40" alt="unity logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/dotnetcore/dotnetcore-original.svg" height="40" alt="dotnetcore logo"  />
</div>

###

<img align="right" src="https://profile-counter.glitch.me/LuxuzDev/count.svg?"  />

###

## Generación de Animación de Serpiente

Este repositorio incluye un flujo de trabajo de GitHub Actions que genera una animación de serpiente en formato SVG. La animación se actualiza automáticamente cada 12 horas y también se puede ejecutar manualmente.

### Configuración del Flujo de Trabajo

El flujo de trabajo está definido en el archivo `.github/workflows/generate-snake.yml` y se ejecuta en las siguientes condiciones:

- **Programado**: Se ejecuta automáticamente cada 12 horas.
- **Desencadenado manualmente**: Se puede ejecutar manualmente desde la interfaz de GitHub.
- **Al hacer push**: Se ejecuta cuando se realiza un push a la rama `master`.

### Contenido del Flujo de Trabajo

```yaml
name: Generate snake animation

on:
  schedule: # execute every 12 hours
    - cron: "* */12 * * *"

  workflow_dispatch:

  push:
    branches:
    - master

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: dist/snake.svg?palette=github-dark

      - name: push snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
