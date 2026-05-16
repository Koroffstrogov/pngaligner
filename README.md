# pngaligner

`pngaligner` est un outil local pour réaligner des spritesheets PNG frame par frame, corriger les offsets d’animation et exporter le résultat.

## Logiciel inclus

- **Sprite Offset Editor** : `/home/runner/work/pngaligner/pngaligner/tools/sprite-offset-editor/index.html`
- Application standalone (HTML/CSS/JS) : aucun build, aucune dépendance externe, aucun serveur requis.

## Fonctions du logiciel

### Chargement et import

- Charger un PNG local (`Charger PNG`)
- Glisser-déposer un PNG ou un JSON dans la zone de drop
- Importer un fichier d’offsets JSON (`Import offsets JSON`)
- Restauration automatique du dernier projet via `localStorage` (si même PNG)
- Reset automatique de tous les offsets lors du chargement d’un nouveau PNG

### Configuration spritesheet

- Réglage `cols` / `rows` (grille)
- Calcul automatique `cellWidth` / `cellHeight`
- Avertissement si l’image n’est pas divisible par la grille
- Réglage de l’ancre (`anchorX`, `anchorY`)
- Réglage de la vitesse (`fps`) et de l’échelle d’affichage (`scale`)

### Édition des offsets

- Sélection de frame par clic sur la spritesheet
- Navigation frame précédente/suivante
- Édition `offsetX` / `offsetY` de la frame courante
- Déplacement clavier :
  - `← → ↑ ↓` : déplacement de 1 px
  - `Shift + flèches` : déplacement de 5 px
- Reset de la frame courante (`R` ou bouton)
- Reset global de tous les offsets
- Application de l’offset courant à toute la ligne (`Apply offset to row`)
- Nudge de toute la ligne (`-1` / `+1` sur X et Y)

### Prévisualisation animation

- Lecture/pause animation (`Espace` ou bouton)
- Sélection d’ordre d’animation :
  - Row 1 / Row 2 / Row 3
  - All frames
  - Custom (liste d’indices)
- Validation de l’ordre custom avec fallback automatique si invalide
- Affichage en temps réel de l’impact des offsets

### Affichages et overlays

- Vue spritesheet complète
- Vue frame courante
- Vue preview animation
- Options d’affichage activables :
  - `Show grid`
  - `Show anchor`
  - `Show frame index`
  - `Show original ghost`
  - `Show hitbox`
- Badge de sélection (frame + offsets)
- Métadonnées affichées : fichier, dimensions image/cellule, nombre de frames, cols/rows, ancre

### Hitbox et zoom

- Calcul automatique de hitbox par frame (boîte minimale des pixels opaques)
- Réglage `hitbox zoom` (0.1 à 4)
- Application du zoom autour d’un pivot basé sur la hitbox de référence
- Visualisation des hitbox dans les canvases

### Export et partage

- Export `*.offsets.json`
- Copie du JSON dans le presse-papiers
- Export PNG réaligné (`Export aligned PNG`)
- Option de suffixe `-aligned` activable/désactivable
- Avertissement de clipping si des pixels sortent d’une cellule après transformation

### Robustesse et sécurité d’usage

- Validation des entrées numériques
- Gestion des JSON invalides
- Avertissements de mismatch de dimensions lors de l’import JSON
- Messages d’état utilisateur (`ok`, `warn`, `error`)

## Format JSON exporté

Le JSON contient :

- `source`
- `imageWidth`, `imageHeight`
- `cols`, `rows`
- `cellWidth`, `cellHeight`
- `anchor` (`x`, `y`)
- `hitboxZoom`
- `animationOrder`
- `frames` avec `{ index, offsetX, offsetY }`

## Utilisation rapide

1. Ouvrir `/home/runner/work/pngaligner/pngaligner/tools/sprite-offset-editor/index.html` dans Chrome/Edge.
2. Charger un PNG.
3. Ajuster les offsets frame par frame.
4. Vérifier le rendu dans la preview animée.
5. Exporter JSON et/ou PNG réaligné.
