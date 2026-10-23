# Prompt per publicar La Recreativa

Copia el bloc de sota i enganxa'l a Claude Code (o a l'agent que facis servir) obert **dins d'aquesta carpeta**. Fa tota la feina: crea el repositori a GitHub, hi puja els fitxers i publica la web a Netlify connectada al repositori.

Si ho prefereixes fer a mà, els mateixos passos estan explicats més avall.

---

```text
Ets dins d'una carpeta amb una web estàtica anomenada "La Recreativa": una portada (index.html) amb l'accés a dos jocs infantils en pixel art, El Menjallapis (jocs/menjallapis/) i el Rei de l'Olla (jocs/rei-de-lolla/). No hi ha cap pas de build; la configuració de Netlify ja és a netlify.toml (publish = ".").

Objectiu: deixar-ho tot en un repositori de GitHub i publicat a Netlify, de manera que cada push a main es publiqui sol.

Fes-ho en aquest ordre i atura't a preguntar-me només si alguna cosa falla o necessites una decisió meva:

1. Comprovacions prèvies
   - Verifica que tens `git`, `gh` (GitHub CLI) i `netlify` (Netlify CLI) instal·lats. Si falta la CLI de Netlify, instal·la-la amb `npm install -g netlify-cli`.
   - Comprova que estic autenticat: `gh auth status` i `netlify status`. Si no ho estic, executa `gh auth login` o `netlify login` i espera que acabi el login al navegador.
   - Obre index.html, jocs/menjallapis/index.html i jocs/rei-de-lolla/index.html i confirma que totes les rutes relatives (assets/, ../../assets/, ../../) apunten a fitxers que existeixen.

2. Repositori local
   - Si la carpeta encara no és un repositori git, fes `git init -b main`.
   - Fes un commit amb tots els fitxers ("Primera versió de La Recreativa") si encara no n'hi ha cap.

3. GitHub
   - Crea un repositori públic al meu compte amb el nom `la-recreativa` i la descripció "Jocs en pixel art per jugar al mòbil", i puja-hi la branca main:
     `gh repo create la-recreativa --public --source=. --remote=origin --push --description "Jocs en pixel art per jugar al mòbil"`
   - Si el nom ja existeix, pregunta'm quin nom vull.

4. Netlify connectat a GitHub
   - Crea el lloc i connecta'l al repositori perquè es desplegui sol a cada push:
     `netlify init`
     Tria: crear un lloc nou, el meu equip, nom del lloc `la-recreativa` (si està agafat, prova `la-recreativa-jocs`), sense build command i directori de publicació `.`.
   - Si `netlify init` no pot enllaçar GitHub automàticament, fes un desplegament manual de producció amb `netlify deploy --prod --dir=.` i explica'm com connectar el repositori des de app.netlify.com (Add new site > Import an existing project > GitHub > la-recreativa).

5. Verificació
   - Obre la URL pública i comprova que carreguen: la portada, /jocs/menjallapis/, /jocs/rei-de-lolla/, /olla i /llapis (aquests dos són redireccions), la font assets/fonts/press-start-2p.woff2 i les dues captures de assets/img/.
   - Fes un `curl -I` a cada URL i confirma que torna 200 (o 301 a les redireccions).

6. Resum final
   - Dona'm la URL de GitHub, la URL de Netlify i una línia de com publicar canvis (editar, `git commit`, `git push`).
```

---

## Fer-ho a mà

### 1. Pujar-ho a GitHub

Des del Terminal, dins d'aquesta carpeta:

```bash
git init -b main          # només si encara no és un repositori
git add .
git commit -m "Primera versió de La Recreativa"
gh repo create la-recreativa --public --source=. --remote=origin --push
```

Sense la GitHub CLI: crea un repositori buit a github.com/new amb el nom `la-recreativa` i després:

```bash
git remote add origin https://github.com/<el-teu-usuari>/la-recreativa.git
git push -u origin main
```

### 2. Publicar-ho a Netlify

1. Entra a app.netlify.com i tria **Add new site > Import an existing project**.
2. Tria **GitHub** i autoritza Netlify si t'ho demana.
3. Selecciona el repositori `la-recreativa`.
4. Deixa **Build command** buit i **Publish directory** amb `.` (ja ve de `netlify.toml`).
5. Prem **Deploy**. En un minut tindràs una URL tipus `https://la-recreativa.netlify.app`.
6. A **Site configuration > Change site name** pots posar-hi un nom més curt.

A partir d'aquí, cada `git push` a `main` es publica sol.

### Enllaços curts

- `/llapis` porta al Menjallapis.
- `/olla` porta al Rei de l'Olla.
