# Sprite Offset Editor

Outil local standalone pour corriger manuellement les offsets frame par frame d’une spritesheet PNG (par défaut 4x3), afin de supprimer les tremblements/glissements en animation.

## Objectif

- Charger une spritesheet PNG locale.
- Ajuster `offsetX` / `offsetY` pour chaque frame.
- Visualiser l’impact en temps réel dans une preview animée.
- Exporter :
  - un JSON d’offsets,
  - un PNG réaligné.

## Ouverture

1. Ouvrir directement `tools/sprite-offset-editor/index.html` dans Chrome ou Edge récents.
2. Aucun serveur, aucun build, aucune dépendance externe.

## Workflow conseillé

1. Charger le PNG (`Charger PNG`) ou glisser-déposer.
   - Le chargement PNG applique maintenant un **Reset all** automatique des offsets.
2. Vérifier/ajuster `cols` et `rows` (4x3 par défaut).
3. Choisir la ligne d’animation (`Row 1`, `Row 2`, `Row 3`, `All`, ou `Custom`).
4. Lancer la preview (play/pause).
5. Corriger frame par frame avec les flèches clavier.
6. (Optionnel) Définir un `hitbox zoom` puis cliquer `Apply hitbox zoom` pour agrandir/réduire proportionnellement tous les sprites autour de leur hitbox.
7. Exporter `*.offsets.json`.
8. Exporter `*.png` (avec ou sans suffixe `-aligned` selon l’option) si besoin.

## Offsets

Chaque frame possède :

- `offsetX` : décalage horizontal (pixels)
- `offsetY` : décalage vertical (pixels)

La preview redessine chaque frame depuis le même point d’ancrage logique (`anchorX`, `anchorY`) puis applique les offsets.

## Export JSON vs Export PNG

### Export offsets JSON

Produit `nom-du-png.offsets.json` avec :

- source PNG
- dimensions image
- cols / rows
- cellWidth / cellHeight
- anchor
- animationOrder
- frames `{ index, offsetX, offsetY }`

Utile pour recharger et itérer sans toucher au sprite source.

### Export aligned PNG

Produit `nom-du-png-aligned.png` (ou `nom-du-png.png` si l’option de suffixe est décochée) :

- dimensions identiques à l’original,
- fond transparent conservé,
- mise à l’échelle optionnelle via `hitbox zoom`,
- offsets appliqués cellule par cellule.

Un warning est affiché si des pixels opaques risquent d’être coupés hors cellule après offset.

## Import JSON

`Import offsets JSON` recharge un travail précédent.

Si les dimensions du JSON ne correspondent pas au PNG chargé, un avertissement est affiché (sans crash).

## Raccourcis clavier

- `←` : `offsetX -1`
- `→` : `offsetX +1`
- `↑` : `offsetY -1`
- `↓` : `offsetY +1`
- `Shift + flèches` : déplacement par 5 px
- `R` : reset offset de la frame courante
- `Espace` : lecture / pause animation

## Bonus inclus

- Copy JSON to clipboard
- Reset all offsets
- Apply same offset to row
- Nudge selected row
- Warning clipping potentiel
- Autosave localStorage du dernier projet
