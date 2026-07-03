# Git Workshop – Branches, IMPL-Features, GFX-Features und Releases

## Inhaltsverzeichnis

- Ziel des Workshops
- Git-Grundlagen
- Branch-Hierarchie
- Workflow
- Git Bash
- SourceTree
- Pull Requests
- Tags
- Branches löschen
- Best Practices
- Cheat Sheet

---

# Ziel des Workshops

In diesem Workshop lernst du den Git-Workflow des Projekts kennen.

Die Branch-Hierarchie lautet:

```text
master
 ├── impl/feature-a
 │    ├── gfx/task-1
 │    ├── gfx/task-2
 │    └── gfx/task-3
 ├── impl/feature-b
 │    └── gfx/task-1
 └── impl/feature-c
```

## Regeln

- `master` enthält ausschließlich stabile Versionen.
- Ein `impl/*`-Branch wird immer von `master` erstellt.
- Ein `gfx/*`-Branch wird immer von einem `impl/*`-Branch erstellt.
- GFX wird zuerst in IMPL gemergt.
- IMPL wird anschließend per Pull Request in `master` übernommen.
- Release-Tags werden ausschließlich auf `master` erstellt.

---

# Git-Grundlagen

## Branch

Ein Branch ist ein Entwicklungszweig.

## IMPL-Branch

Enthält die vollständige Implementierung eines Features.

## GFX-Branch

Enthält Teilaufgaben oder grafische Arbeiten innerhalb eines IMPL-Features.

---

# Workflow

```text
master
   │
   ▼
impl/player
   │
   ├───────────────┐
   ▼               ▼
gfx/menu      gfx/animation
   │               │
   └──────┬────────┘
          ▼
      impl/player
          │
      Branch Tag
          │
          ▼
     Pull Request
          │
          ▼
        master
          │
      Release Tag
```

# Git Bash

## Repository klonen

```bash
git clone <url>
cd <repository>
```

## Aktuellen Branch anzeigen

```bash
git branch
git status
```

## IMPL-Branch erstellen

```bash
git switch master
git pull
git switch -c impl/player
git push --set-upstream origin impl/player
```

## GFX-Branch erstellen

```bash
git switch impl/player
git pull
git switch -c gfx/player-animation
git push --set-upstream origin gfx/player-animation
```

## Änderungen committen

```bash
git add .
git commit -m "Beschreibung"
git push
```

## GFX in IMPL mergen

```bash
git switch impl/player
git pull
git merge gfx/player-animation
git push
```

## IMPL in master mergen

```bash
git switch master
git pull
git merge impl/player
git push
```

## Branch Tag

```bash
git tag player-v1.0
git push origin player-v1.0
```

## Release Tag

```bash
git tag v1.0.0
git push origin v1.0.0
```

## Branch löschen

```bash
git branch -d gfx/player-animation
git push origin --delete gfx/player-animation

git branch -d impl/player
git push origin --delete impl/player
```

---

# SourceTree

## Repository klonen

1. Clone
2. URL eingeben
3. Ziel auswählen
4. Clone

## IMPL-Branch

1. master auswählen
2. Pull
3. Branch
4. Name: impl/player
5. Checkout new branch
6. Push

## GFX-Branch

1. impl/player auswählen
2. Branch
3. Name: gfx/player-animation
4. Push

## Commit

1. Dateien auswählen
2. Commit Message
3. Commit
4. Push

## Merge

1. Zielbranch auswählen
2. Merge
3. Quellbranch auswählen
4. Push

## Tag

1. Repository
2. Tag
3. Namen vergeben
4. Push

---

# Pull Requests

Alle Änderungen erfolgen über Pull Requests.

## GFX → IMPL

Source:

```text
gfx/player-animation
```

Target:

```text
impl/player
```

Nach Freigabe:

- Merge
- GFX-Branch löschen

## IMPL → master

Source:

```text
impl/player
```

Target:

```text
master
```

Nach Freigabe:

- Merge
- Release Tag
- IMPL-Branch löschen

---

# Tags

## Entwicklungsstände

```text
player-v0.1
player-v0.2
player-v1.0
```

## Releases

```text
v1.0.0
v1.1.0
v2.0.0
```

---

# Best Practices

- Kleine Commits erstellen
- Aussagekräftige Commit-Messages verwenden
- Regelmäßig pullen
- Nur über Pull Requests mergen
- Nach jedem Release einen Tag setzen
- Alte Branches löschen

---

# Git Cheat Sheet

| Aufgabe | Befehl |
|----------|---------|
| Status | `git status` |
| Branches | `git branch` |
| Alle Branches | `git branch -a` |
| Wechseln | `git switch <branch>` |
| Branch erstellen | `git switch -c <branch>` |
| Commit | `git commit -m "..."` |
| Push | `git push` |
| Pull | `git pull` |
| Merge | `git merge <branch>` |
| Tags | `git tag` |
| Log | `git log --oneline --graph --all` |

---

# Workshop-Aufgabe

1. Repository klonen
2. IMPL-Branch erstellen
3. GFX-Branch erstellen
4. Änderungen committen
5. Pull Request GFX → IMPL
6. IMPL taggen
7. Pull Request IMPL → master
8. Release-Tag erstellen
9. Branches löschen

