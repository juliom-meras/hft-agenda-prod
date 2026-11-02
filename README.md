# Mudanza de Pasti-agenda a Pasti-1

Esta carpeta es lo que se publica en la dirección antigua (`juliom-meras.github.io/hft-agenda-prod/`) como última
versión de Pasti-agenda: una página fija que avisa de la mudanza a Pasti-1
(`https://juliom-meras.github.io/pasti-1-prod/`) y un Service Worker que sustituye al de la 2.0.0 y borra sus cachés.

**Aviso para quien tenga la web instalada en iPhone o iPad:** no quites esta app de la pantalla de inicio hasta haber
restaurado su copia en Pasti-1; quitarla borra sus datos. Pulsa «Descargar copia de seguridad» en la página, guarda el
fichero y restáurala en Pasti-1 (Paciente → Datos → Restaurar copia).

- `index.html`: la página (sin `manifest`, CSS en línea).
- `descarga.js`: «Descargar copia de seguridad». Solo lee `localStorage` (`getItem`): no escribe, no borra y no muestra
  los datos. Datos 2.0.0 → copia `mediagenda-copia`; 1.x → el texto tal cual; datos rotos → texto crudo
  (`pasti-agenda-datos-antiguos.json`).
- `sw.js`: caché `hft-agenda-mudanza-v1`; al activarse borra solo las cachés `mediagenda-*` y recarga las pestañas.
- Compilar: `npm run mudanza:build` (`build/mudanza.mjs`) → `dist-mudanza/` (ignorado por git; reproducible). El build
  falla si el código escribe o borra en el almacenamiento, usa `innerHTML` o añade otro `<script>`.
- Publicar: el contenido de `dist-mudanza/` sustituye al de `hft-agenda-prod` (ver el plan, F9).
