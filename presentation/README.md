# Cygni - Talangprogrammet
## Mall för presentationer

Mallen är gjord i HTML med reveal.js.
Fördelarna med det är
- presentationen blir "standalone" och kan alltså enkelt köras offline eller distribueras via t.ex. mail eller Slack
- ren HTML gör att vi är i stort sett obegränsade i vad vi kan göra i presentationen
- det är lätt att producera enhetliga presentationer som ser bra ut
- den som tillverkar presentationen kan använda de verktyg/den editor han/hon känner sig bekväm med
- vi versionshanterar presentationen med git
- det är roligare att koda sin presentation!

### Installera och bygg
```bash
npm install && npm run build-all
```

Den färdiga presentationen hamnar under katalogen `target`.

## Att göra en presentation 

Att göra en ny presentation är enkelt. Använd presetnationen som heter `index.html` och skriv om den efter dina behov.
För en enkel presentation behöver du endast byta ut innehållet i HTML-filen för att få en snygg Cygni-brandad sida med animationseffekter.

För den som vill göra större utsvävningar så finns det lite tips i mallen. (Öppna filen i en browser - men se till att åtminstone bygga css först genom `npm run sass`)
För den som vill lära sig mer om reveal.js så finns det en bra demo [här](https://revealjs.com/#/).

### Bygg CSS

All CSS är skriven med SASS. För att kompilera SASS-filerna till CSS så kör du
```bash
npm run sass
```

Mallarna finns under katalogen `style` och CSS-filerna hamnar i under katalogen `assets/css`.

Det finns även en watch-funktion så att man kan kompilera SASS-filerna kontinuerligt
```
npm run watch
```

### Bygg presentationen
```bash
npm run build
```
