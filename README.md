
# Git Workshop – Branches, IMPL-Features, GFX-Features, Pull Requests und Tags

## Inhaltsverzeichnis

1. Ziel
2. Branch-Hierarchie
3. Workflow
4. Git Bash
5. SourceTree
6. Pull Requests
7. Tags
8. Branches löschen
9. Best Practices
10. Cheat Sheet

---

# Ziel

Dieser Workshop vermittelt den Git-Workflow des Projekts.

## Branch-Hierarchie

```text
master
├── impl/feature-a
│   ├── gfx/task-1
│   ├── gfx/task-2
│   └── gfx/task-3
├── impl/feature-b
│   └── gfx/task-1
└── impl/feature-c
```

## Regeln

- `master` enthält ausschließlich stabile Versionen.
- `impl/*` wird immer von `master` erstellt.
- `gfx/*` wird immer vom jeweiligen `impl/*` erstellt.
- `gfx/*` wird ausschließlich zurück in den zugehörigen `impl/*` gemergt.
- `impl/*` wird ausschließlich per Pull Request nach `master` gemergt.
- Release-Tags werden nur auf `master` erstellt.

# Workflow

```text
master
  │
  ▼
impl/player
  │
  ├────────────┐
  ▼            ▼
gfx/menu   gfx/animation
  │            │
  └─────┬──────┘
        ▼
   impl/player
        │
   Tag: player-v1.0
        │
 Pull Request
        │
        ▼
      master
        │
   Tag: v1.0.0
```

# Git Bash

## Repository klonen

```bash
git clone <repository-url>
cd <repository>
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

## GFX nach IMPL mergen

```bash
git switch impl/player
git pull
git merge gfx/player-animation
git push
```

## IMPL nach master mergen

```bash
git switch master
git pull
git merge impl/player
git push
```

# SourceTree

1. Repository klonen.
2. `master` auswählen und **Pull**.
3. **Branch** → `impl/player`.
4. Auf `impl/player` wechseln.
5. **Branch** → `gfx/player-animation`.
6. Änderungen committen.
7. **Merge** für `gfx/*` → `impl/*`.
8. Pull Request erstellen.
9. Nach Freigabe mergen.
10. Tags erstellen und pushen.

# Pull Requests

## GFX → IMPL

Source:

```text
gfx/player-animation
```

Target:

```text
impl/player
```

Ablauf:

1. Änderungen pushen.
2. Pull Request erstellen.
3. Code Review.
4. Merge.
5. GFX-Branch löschen.

## IMPL → master

Source:

```text
impl/player
```

Target:

```text
master
```

Ablauf:

1. IMPL-Tag erstellen.
2. Pull Request.
3. Review.
4. Merge.
5. Release-Tag erstellen.
6. IMPL-Branch löschen.

# Branch-Tags

## Wichtiger Hinweis

Git taggt **keinen Branch**, sondern immer den **aktuellen Commit**. Deshalb muss zuerst auf den gewünschten Branch gewechselt werden.

## IMPL-Branch taggen

```bash
git switch impl/player
git push
git tag player-v1.0
git push origin player-v1.0
```

oder

```bash
git push --tags
```

## GFX-Branch taggen

```bash
git switch gfx/player-animation
git tag gfx-player-animation-v0.5
git push origin gfx-player-animation-v0.5
```

## Release-Tag auf master

```bash
git switch master
git pull
git tag v1.0.0
git push origin v1.0.0
```

## Tags anzeigen

```bash
git tag
git show player-v1.0
```

## Tag löschen

Lokal:

```bash
git tag -d player-v1.0
```

Remote:

```bash
git push origin --delete player-v1.0
```

# Branches löschen

```bash
git branch -d gfx/player-animation
git push origin --delete gfx/player-animation

git branch -d impl/player
git push origin --delete impl/player
```

# Best Practices

- Kleine Commits erstellen.
- Aussagekräftige Commit-Messages verwenden.
- Vor dem Arbeiten `git pull` ausführen.
- Nur über Pull Requests mergen.
- IMPL-Branches vor dem Merge taggen.
- Releases ausschließlich auf `master` taggen.
- Nicht mehr benötigte Branches löschen.

# Git Cheat Sheet

| Aufgabe | Befehl |
|---|---|
| Status | `git status` |
| Branches | `git branch -a` |
| Wechseln | `git switch <branch>` |
| Branch erstellen | `git switch -c <branch>` |
| Commit | `git commit -m "..."` |
| Push | `git push` |
| Pull | `git pull` |
| Merge | `git merge <branch>` |
| Tags | `git tag` |
| Log | `git log --oneline --graph --all` |
