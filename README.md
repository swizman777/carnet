# carnet

Un carnet de notes en ligne de commande. Écrire, relire, retrouver — sans
quitter le terminal, sans dépendance à installer.

```sh
carnet ajoute "réunion déplacée à jeudi"
carnet ajoute < brouillon.txt      # ou au bout d'un tube
carnet liste                       # les 20 dernières
carnet liste 5
carnet cherche jeudi               # insensible à la casse, rend 1 si rien
carnet chemin
```

## Où sont les notes

`$CARNET_DIR/notes.md`, par défaut `~/.local/share/carnet/notes.md`.

**Hors du dépôt, délibérément** : ce sont des données, pas du code. Les
versionner mélangerait l'historique de l'outil et celui de son contenu.

Le format est du Markdown lisible à l'œil et greppable — un en-tête `##
<horodatage UTC>` par note, le texte en dessous. Si l'outil disparaît, les
notes restent lisibles avec `cat`. C'est le principal critère qui a guidé le
format.

## Ce que l'outil ne fait pas

**Il ne modifie ni ne supprime.** Un carnet qu'on peut réécrire en silence perd
ce qui fait sa valeur : la trace de ce qu'on pensait à ce moment-là. Se tromper
et ajouter un correctif est plus honnête qu'effacer.

**Il n'indexe pas.** `cherche` est un parcours linéaire. Un index doit être
maintenu, se désynchronise, et devient faux au pire moment. À la taille d'un
carnet humain, la recherche est instantanée — on changera le jour où une mesure
le demandera, pas avant.

## Écriture concurrente

`ajoute` prend un verrou (`flock`) avant d'écrire. Deux terminaux, une session
ssh et un tmux peuvent écrire en même temps : un `>>` concurrent entrelacerait
deux notes multi-lignes, et **une note à moitié écrite est pire qu'une note
perdue, parce qu'on la croit entière**.

## Développer

```sh
./t/comportement     # 13 cas, dans un CARNET_DIR temporaire
verifier             # la porte : syntaxe + comportement
```

Le manifeste `.verifier` déclare `bash -n` par fichier et `t/comportement` en
contrôle global. Un commit ne prouve donc que la syntaxe (0,03 s) ; une
promotion prouve le comportement (0,7 s).

Les tests écrivent dans un répertoire temporaire et un cas vérifie qu'ils n'ont
**rien touché du vrai carnet** — cette famille de fuite s'est produite cinq
fois ailleurs sur cette station.
