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

### Ce qui n'est pas encore décidé

Ces questions se trancheront **au moment où elles bloqueront**, pas avant :

- où vivent les notes (un fichier, un répertoire, un dépôt git à part) ;
- si une note est modifiable ou seulement ajoutable ;
- comment on cherche : `grep` suffit-il, ou faut-il un index.

Les inscrire ici quand elles seront tranchées, avec la raison.

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

**La porte n'est pas encore active.** C'est délibéré : un projet sans code n'a
rien d'honnête à vérifier, et un manifeste qui passerait quand même ferait
mentir la porte dès le premier jour. Elle s'active avec le premier fichier —
voir le skill `specifier-projet`.

À consigner ensuite au fil de l'eau : pièges rencontrés, décisions et leur
raison. Un piège documenté ne se repaie pas deux fois.
