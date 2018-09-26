# git: do it yourself

I den här övningen kommer vi att återskapa gits fundamentala funktionalitet.

## läs före:

* gitboken kapitel [10.1-10.3](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain).

## prerequisites

* `python3.7`;
* [pipenv](https://github.com/pypa/pipenv).

## quickstart

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

## mål

* _slutgiltigt_: köra först `create_repo.sh` och sedan `pytt_commit.sh` och då se två commits från `git log`.
* _delsteg_: implementera följande funktioner i ordning (alla finns i `pytt.py`>):
* `hash-object` (som är färdigimplementerad för att ge en liten headstart);
* `cat-file`;
* `update-index`;
* `ls-files`;
* `write-tree`;
* `commit-tree`;
* `update-ref`.

### tester

Finns ej, göre live.

### api

`{Tree,Commit}{,.Entry}` uppfyller alla följande api:

* `unpack`: packa upp data från ett git objekt och skapa klassen;
* och `pack`: packa ihop objektet till data.

## editor

Visual Studio Code med dess officiella Python-plugin rekommenderas.

### setup

1. Installera [Python-plugin:et](https://marketplace.visualstudio.com/items?itemName=ms-python.python);
2. Klicka `cmd-shift-p` (eller `ctrl-shift-p` för icke-mac), och välj alternativet `Python: Select Interpreter`;
3. Välj den som heter `Python 3.7.0 (virtualenv)`
4. Om ni vill kunna köra script med shift-enter från VSCode så lägg till denna keybinding:

```json
{
  "key": "shift+enter",
  "command": "workbench.action.terminal.runSelectedText",
  "when":
    "editorFocus && !findInputFocussed && !replaceInputFocussed && editorLangId == 'shellscript'"
}
```

## vanliga fel

Här har ni några vanliga fel ni kan stöta på.

### `pipenv shell` skiter sig

Se till att du har följande i `.profile` eller `.zshenv`:

```shell
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```

### jag vet inte hur man skapar en klass-instans i Python

Om du vill skapa exempelvis ett nytt träd:

```python
Tree.Entry(
    entry.name,
    entry.sha,
    mode_type=entry.mode_type,
    mode_permissions=entry.mode_permissions,
)
```

### vad fan är `self` i python-metoderna?

En referens till objektet du anropar metoden på och skickas in "av sig själv".

Du anropar alltså exempelvis metoden `pack` i `Tree` på följande sätt:

```python
instance_of_tree_object.pack()
```

### men vad är då `cls` i python-metoderna???

En referens till klassen du anropar den statiska klassmetoden på. Det skickas också in "av sig själv".

Du anropar alltså metoden `unpack` i `Tree` på följande sätt:

```python
Tree.unpack(data)
```

### `TypeError: %b requires a bytes-like object, or an object that implements __bytes__, not 'str'` (eller något liknande)

Python skiljer på byte-strängar (`bytes`) som är råa och inte har en encoding och strängar (`str`) som har en encoding.
Ni måste arbeta med en sort åt gången, antingen `bytes` eller `str`.

😭 VA!???

* `bytes -> str`: `some_bytes.decode()` (antar UTF-8 som encoding, vilket ju bör vara rimligt);
* `str -> bytes` `some_str.encode()`;
* rå `bytes`-sträng: sätt ett `b` framför ba: `b"our bytes string"`
* öppna en fil och läs som `str`: `file.open(our_file, 'r')`;
* öppna fil och läs som `bytes`: `file.open(our_file 'rb')`;

_Tips_:

* om det är text ni håller på med är det ju oftast `str`;
* om det är någon form av data som kan vara lite vad som helst är det oftast `bytes`.

### vi fattar inte alls vad vi ska göra!??!?!?

Diskutera vad funktionen har för syfte "i det stora hela", dvs vad ska ni åstadkomma.

### vi får något skitkonstigt Python-fel som inte står ovan

Be om hjälp dirr.
