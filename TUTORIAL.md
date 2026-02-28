# Vibe Coding Tutorial (Edición Web)
# Requisitos previos

1. Crea una cuenta en [GitHub](https://github.com/)

2. Descarga e instala [git](https://git-scm.com/install/windows).
    
    Verifica la instalación:
    ```bash
    git -v
    ```
    
3. Descarga e instala [node](https://nodejs.org/en/download).

    Verifica la instalación:
    ```bash
    node -v
    ```
    ```bash
    npm -v
    ```

4. Descarga e instala [Visual Studio Code](https://code.visualstudio.com/docs/setup/windows#_install-vs-code-on-windows).

5. Descarga e instala [Fork](https://git-fork.com/).

6. Añade nombre y email de GitHub en cmd:
    ```bash
    git config --global user.email “name@email.com”
    ```
    ```bash
    git config --global user.name “Your GitHub Name”
    ```

7. Añade extensión [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) a Visual Studio Code y haz log in con tus credenciales de GitHub.


### (_OPCIONAL_) Si tienes cuenta de Claude Code y quieres usarla

1. Instala Claude Code desde `cmd` con el siguiente [comando](https://code.claude.com/docs/en/setup):
```bash
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

2. Al terminar su ejecución, el comando anterior da instrucciones sobre cómo añadir claude al PATH, sígue dichas instrucciones.
> _Me puedes pasar foto y preguntar si hay dudas, es que no me acuerdo de los pasos exactos jeje lol_

3. Añade la extensión de [Claude Code for VS Code](https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code) y haz log in siguiendo las indicaciones.
> _Más de lo mismo, pero deberían ser indicaciones sencillas rollo loguearte desde el navegador, recibir un correo, poner un código etc._


# Cosas que aprendimos en este tutorial:

Una vez todos los requisitos previos están listos, podemos hacer cosas como:

### Crear un repositorio

Desde Github, en el navegador, podemos crear un nuevo repositorio para después clonarlo a nuestro ordenador y empezar a vibecodear.

> No es obligatorio, pero los repositorios suelen tener nombres en minúscula (solo se usan mayúsculas si hay una razón para ello) y con "-" en vez de espacios.

### Clonar un repositorio ya existente
Si tenemos el enlace de un repositorio, por ejemplo, https://github.com/Takajs/vibe-coding-web-windows-tutorial, podemos clonar el repositorio a una carpeta de nuestro ordenador desde Visual Studio Code en el menú `Source Control (CTRL+Shift+G, no debe hacer ninguna carpeta abierta en Visual Studio Code) -> Clone Repository` pegando el enlace https://github.com/Takajs/vibe-coding-web-windows-tutorial.git que podemos encontrar visitando el repositorio en github.

Esto funciona para cualquier repositorio público.

### Utilizar Fork para manejar git

Desde Fork, tenemos una interfaz visual en la que podemos abrir un repositorio ya existente y copiado a nuestro ordenador. Nos permite además:

- Ver los cambios actuales comparándolo con la versión remota (la que está en github).

- Crear, eliminar y mezclar (merge) ramas (branches). También podemos desplazarnos de una rama a otra.

- Manejar las distintas fases que ocurren entre tener nuestros cambios localmente y que llguen al repositorio:

    1. **Unstaged**: los archivos están guardados, existen en mi ordenador, pero no han sido preseleccionados como parte de un Commit. No existen aún en el repositorio remoto.

    2. **Staged**: una vez stageados, los archivos existen en mi ordenador, están guardados y han sido preseleccionados como parte de un futuro Commit. No existen aún en el repositorio remoto.
    
        Para continuar, se requiere de un mensaje que describe los cambios que hemos preseleccionado.

        Ejemplos:

            feature(midi player): add pause/play buttons

            chore(animations): upgrade tone.js to latest version "14.7.39"

            improve(track muter): do not try to mute empty tracks for performance

            fix(log in): correctly read cookies' session if many profiles exist in the same browser

            ...

    3. **Commit**: una vez commiteados, los archivos están guardados, existen en mi ordenador y han sido seleccionados como parte de un Commit con un mensaje y descripción en una rama concreta. No existen aún en el repositorio remoto.

    4. **Push**: una vez pusheados, los archivos están guardados, existen en mi ordenador, han sido seleccionados como parte de un Commit con un mensaje y descripción en una rama concreta. Existen en el repositorio remoto. Ahora hacen parte del proyecto en Github, se pueden clonar desde otra máquina, no pasa _nada_ si tu ordenador explota etc.


### Enlaces recomendados

- [Skills](https://code.claude.com/docs/en/skills) y similares : Archivos `.md` con reglas y skills para agentes. Podemos mangarlos para nuestros proyectos y mejorar/condicionar como actuarán. Basta con copiar lo que pone, crear un archivo en la carpeta local de nuestro proyecto y, cuando lo necesitemos, pedirle al agente que lo tenga en cuenta.

- [AskUserQuestion tool](https://code.claude.com/docs/en/best-practices#let-claude-interview-you) y más utilidades/consejos disponibles en el resto de la documentación oficial.

# Finalmente, en este tutorial intentamos vibecodear alguna app de verdad".

Yo utilicé el siguiente workflow de prompts para mi [app de ejemplo](https://github.com/Takajs/midi-player-visualizer):

```prompt 1
I want to build a web midi visualizer player that allows the user to load a midi file and see in real time animations, defined by the notes that are played at each instant, while the song is played
Interview me in detail using the AskUserQuestion tool.
Ask about technical implementation, UI/UX, edge cases, concerns, and tradeoffs. Don't ask obvious questions, dig into the hard parts I might not have considered.
Keep interviewing until we've covered everything, then write a complete spec to SPEC.md.
```

```prompt 2
I want to create the IMPLEMENTATION_STEPS.md for this project. Read the SPEC.md and interview me in detail using the AskUserQuestion tool.
Ask about architechture, technical implementation, UI/UX, edge cases, concerns, and tradeoffs. Do it only when needed, do not ask questions already answered in SPEC.md.
Don't ask obvious questions, dig into the hard parts I might not have considered.
Keep interviewing until we've covered everything, then write a complete IMPLEMENTATION_STEPS.md and update if necessary the specs in SPEC.md.
```

```prompt 3
Implement the web midi visualizer player defined by SPEC.md following IMPLEMENTATION_STEPS.md. Continue until all the requirements are implemented and ensure everything works as expected without any errors.
Avoid over-engineering. Only make changes that are directly requested or clearly necessary. Keep solutions simple and focused:
- Scope: Don't add features, refactor code, or make "improvements" beyond what was asked. A bug fix doesn't need surrounding code cleaned up. A simple feature doesn't need extra configurability.
- Documentation: Don't add docstrings, comments, or type annotations to code you didn't change. Only add comments where the logic isn't self-evident.
- Defensive coding: Don't add error handling, fallbacks, or validation for scenarios that can't happen. Trust internal code and framework guarantees. Only validate at system boundaries (user input, external APIs).
- Abstractions: Don't create helpers, utilities, or abstractions for one-time operations. Don't design for hypothetical future requirements. The right amount of complexity is the minimum needed for the current task.
```
