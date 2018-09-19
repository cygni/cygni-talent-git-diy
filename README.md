# Git: do it yourself
I den här övningen kommer vi att återskapa gits fundamentala funktionalitet.

## Quickstart
```sh
# clone:a ner det här repo:t
git clone git@github.com:cygni/cygni-talent-git-diy.git
# clone:a pytt-repo:t
git clone git@github.com:mbark/pytt.git
cd pytt
# applicera patch:en som sätter koden i rätt läge
git apply ../cygni-talent-git-diy/0001-pass.patch
# installera alla dependencies
pipenv install
# aktivera ett shell med alla dependencies installerade
pipenv shell
# verifiera att pytt startar som det ska
pytt --help
```

## what to do
Ni ska köra igenom filerna `part{1,2,3}.sh` (`part2.sh` gör inga
ändringar i repo:t) och då avsluta med en `git log` som ser ut
som följer: 
```bash
$ git log
commit e6a5d58581a1e5116bf9a1c0cab3a6d1934967db (HEAD -> master)
Author: Foo Bar <foo.bar@email.com>
Date:   Tue Jul 17 17:07:35 2018 +0200

    Oops! Wrong dude, this is the real one!

commit 5b9765189979ceb9eb81762e510f6f4efcfff139
Author: Martin Barksten <martin.barksten@gmail.com>
Date:   Thu Apr 7 22:13:13 2005 +0200

    Add legit quote by e = mc2 dude
```

De funktioner som ni behöver implementera (i ordning) är:
- `hash-object` (som är färdigimplementerad för att ge en liten headstart);
- `cat-file`;
- `update-index`;
- `ls-files`;
- `write-tree`;
- `commit-tree`;
- `update-ref`.

I repo:t har jag skrivit en del boilerplate för att ni ska komma igång
fort -- det som kvarstår är de ovan nämnda funktionerna som alla
finns i `pytt.py`-filen.

Funktionerna har alla lite dokumentation som i korta drag beskriver vad dem gör,
utöver detta rekommenderas att ni kollar `git {kommando} --help` eller boken om
`git` (se [hjälp](#hjälp) nedan).

### tester
Det finns ingen testkod skriver för att verifiera funktionerna istället får ni
göra det live, dvs testköra mot ett riktigt repo. Det är rekommenderat att ni
sätter upp ett nytt test-repo som ni kan ta bort om något blir fel.

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
3. Kolla i boken om `git` kapitel
[10.2](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) och
[10.3](https://git-scm.com/book/en/v2/Git-Internals-Git-References) om det finns
hjälp att få;
4. Fråga om hjälp eller kolla facit (dvs git diff:en pga patch:en).
