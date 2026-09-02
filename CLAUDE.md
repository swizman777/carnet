# carnet

<!-- Contrat de ce projet. Il est lu par tout agent au démarrage d'une session.
     Le remplir est la première tâche du projet, avant d'écrire du code. -->

## Ce que fait ce projet

Un carnet de notes en ligne de commande.

Écrire une note, les relire, les retrouver — sans quitter le terminal, et sans
dépendance à installer : **shell**, comme les onze outils de la station. Ce
choix se défend par le contexte plutôt que par le goût — un carnet doit
démarrer instantanément, survivre à un PATH réduit, et ne rien casser quand
Python change de version. Il n'est pas encore payé : aucun fichier n'existe, en
changer ne coûte rien aujourd'hui.

## Terminé veut dire

Un critère qu'une commande tranche, jamais une impression.

Pour la **première tâche**, celle qui donnera au projet son premier fichier :

> `carnet ajoute "essai"` puis `carnet liste` affiche `essai`, et `verifier`
> passe.

Rien n'est écrit tant que ce critère n'a pas de code derrière. Chaque tâche
suivante pose le sien avant de commencer — voir le skill `ouvrir-tache`.

### Les trois décisions, tranchées à la première tâche

Elles bloquaient, donc elles ont été prises — avec leur raison, qui compte plus
que le choix.

**Les notes vivent hors du dépôt**, dans `$CARNET_DIR` (défaut
`~/.local/share/carnet`). Ce sont des *données*, pas du code : les versionner
mélangerait l'historique de l'outil et celui de son contenu, et un carnet qui
grossit ferait échouer les captures de la station. La variable existe surtout
pour que le harnais écrive ailleurs — un test ne doit jamais toucher le vrai
carnet.

**Une note s'ajoute, elle ne se modifie pas.** Un carnet qu'on peut réécrire en
silence perd ce qui fait sa valeur : la trace de ce qu'on pensait à ce
moment-là. Ajouter un correctif est plus honnête qu'effacer. `carnet retire`
viendra si le besoin se présente, et devra laisser une trace.

**La recherche est un `grep`, sans index.** Un index se désynchronise et
devient faux au pire moment. À la taille d'un carnet humain, la recherche
linéaire est instantanée. On changera le jour où une mesure le demandera.

### Ce qui reste ouvert

- pas de `carnet retire` ni d'édition — voir la décision ci-dessus ;
- pas de catégories ni d'étiquettes : `cherche` suffit tant qu'on ne mesure
  pas le contraire.

## La commande qui prouve

```sh
verifier          # porte du projet, d'après .verifier
```

**État de la porte : NON ACTIVE.** Le fichier `.verifier` de ce projet ne
déclare encore aucun contrôle — un projet vide n'a rien d'honnête à vérifier,
et un manifeste qui passerait quand même ferait mentir la porte dès le premier
jour.

Déclarer les premiers contrôles fait partie de la première tâche réelle :
décommenter les lignes de `.verifier` et énumérer les cibles.

## Périmètre

Fichiers qu'une tâche a le droit de modifier : tout fichier de code qu'elle
crée, **à condition de le déclarer dans `.verifier` au même commit**. Un
fichier non déclaré n'est pas contrôlé, et personne ne s'en apercevra.
Fichiers à ne jamais toucher sans décision explicite : `.verifier`, ce fichier.

## Ce qu'il faut savoir avant de commencer

**Les notes sont des données, pas du code.** Elles vivront hors du dépôt, ou
dans un dossier ignoré : un carnet qui grossit ne doit pas faire échouer les
captures — le préflight de `snapshot` refuse au-delà de 100 Mio par fichier ou
250 Mio au total. À trancher à la première tâche, et à écrire ici.

**La porte est active, à deux niveaux — et l'écart compte.**

| | Contrôle | Coût |
|---|---|---|
| à chaque commit (`--rapide`) | `bash -n` sur les cibles | 0,03 s |
| à la promotion (complet) | `bash -n` **+ `t/comportement`** | 0,7 s |

Autrement dit : un commit ne prouve que la syntaxe, une **promotion** prouve le
comportement. C'est délibéré — le contrôle qui se paie vingt fois par jour doit
rester gratuit, celui qui décide de la livraison doit être honnête.

Vérifié pour de vrai : en plantant une régression qui faisait que `ajoute`
n'ajoutait plus rien, `bash -n` passait et **`t/comportement` a refusé**.

À consigner ensuite au fil de l'eau : pièges rencontrés, décisions et leur
raison. Un piège documenté ne se repaie pas deux fois.
