# La Recreativa

Jocs en pixel art per jugar al navegador del mòbil, sense instal·lar res.

| Joc | Jugadors | Ruta |
| --- | --- | --- |
| El Menjallapis | 1 | `/jocs/menjallapis/` (o `/llapis`) |
| Rei de l'Olla | 2 al mateix mòbil | `/jocs/rei-de-lolla/` (o `/olla`) |
| Blocaventura | 1 | `/jocs/blocaventura/` |
| Fiore contra el Turbocapitalisme | 1 | `/jocs/fiore/` |

## Estructura

```
index.html                    Portada amb l'accés als jocs
jocs/menjallapis/index.html   El Menjallapis (un sol fitxer: HTML + CSS + JS)
jocs/rei-de-lolla/index.html  Rei de l'Olla (un sol fitxer: HTML + CSS + JS)
jocs/blocaventura/index.html  Blocaventura (un sol fitxer: HTML + CSS + JS)
jocs/fiore/index.html         Fiore contra el Turbocapitalisme (un sol fitxer: HTML + CSS + JS)
assets/fonts/                 Tipografia Press Start 2P (llicència OFL, a OFL.txt)
assets/img/                   Captures per a la portada i favicon
netlify.toml                  Configuració de Netlify (sense build)
```

No hi ha dependències ni pas de build. Cada joc és un HTML autònom amb un `<canvas>` de 180×320 escalat en píxels enters.

## Provar-ho en local

```bash
python3 -m http.server 8000
# obre http://localhost:8000
```

Per provar-ho al mòbil, connecta'l a la mateixa wifi i obre `http://<ip-de-l-ordinador>:8000`.

## Publicar

Cada `git push` a `main` es publica sol a Netlify un cop el repositori està connectat. Els passos inicials són a [PROMPT.md](PROMPT.md).

## Afegir un joc nou

1. Crea `jocs/<nom>/index.html` (pots copiar l'estructura d'un dels existents: carrega la font des de `../../assets/fonts/` i porta l'enllaç `< JOCS` per tornar).
2. Afegeix una captura a `assets/img/<nom>.png`.
3. Duplica una targeta `<a class="machine">` a `index.html` i canvia'n el text.

## Notes

- Els personatges són originals; no reprodueixen cap personatge existent.
- La veu del Rei de l'Olla fa servir la síntesi de veu del navegador (Web Speech API). A Android funciona a Chrome; a iPhone pot caldre descarregar la veu catalana a Ajustes.
- El Menjallapis es pot jugar amb la pantalla en blanc i negre: cada color té el seu símbol.
