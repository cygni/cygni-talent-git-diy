# Git: do it yourself
I den här övningen kommer vi att återskapa grundläggande git-funktionalitet för
att visa hur enkelt det konceptuellt är.

## Quickstart
```sh
# clone>a repo:t
git clone https://github.com/mbark/pytt
cd pytt
# installera alla dependencies
pipenv install
# aktivera ett shell med alla dependencies installerade
pipenv shell
# verifiera att pytt startar som det ska
pytt --help
```

## what to do
`pytt` har en hel del boilerplate uppsatt för att ni ska kunna komma igång
enkelt. Det kvarstår bara för er att skriva klart några funktioner i
`pytt.py`-filen. De funktioner som behöver implementeras är:
- `hash-object` (som är färdigimplementerad för att ge en liten headstart);
- `cat-file`;
- `update-index`;
- `ls-files`;
- `write-tree`;
- `commit-tree`;
- `update-ref`.

Det är rekommenderat att ni implementerar funktionerna i ordningen ovan.
Funktionerna har alla lite dokumentation som i korta drag beskriver vad dem gör,
utöver detta rekommenderas att ni kollar `--help` och git-boken (se hjälp
nedan).

### testing
Det finns ingen testkod skriver för att verifiera funktionerna istället får ni
göra det live, dvs testköra mot ett riktigt repo. Det är rekommenderat att ni
sätter upp ett nytt test-repo som ni kan ta bort om något blir fel.

Som guidning har ni filerna `part{1,2,3}.sh` i projektet till er hjälp,
framförallt `part3.sh` visar hur alla kommandona används för att tillsammans
skapa en commit.

### object
Alla tree-, commit- och index-klasserna uppfyller alla följande API:
- `from_string`: som användas för att från en sträng skapa en instans av
  klassen;
- och `pack`: som användas för att packa ihop klassen till en sträng som kan
  sparas ner.

Objekten har dokumentation som beskriver hur dem ser ut, annars får ni kolla
vilka fält som sätts om ni behöver komma åt något värde.

## hjälp
Om ni kör fast:
1. Kolla `git {kommando}` för att se vad kommandot ska göra;
2. Kolla i `object.py` eller `index.py` för att se om dokumentation hjälper;
3. Kolla i git-boken kapitel
[10.2](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) och
[10.3](https://git-scm.com/book/en/v2/Git-Internals-Git-References) om det finns
hjälp att få;
4. Fråga om hjälp.
