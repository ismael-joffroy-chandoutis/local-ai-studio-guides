**Version : v2026-09-23.1 · 23/09/2026 00h27 Paris · sources : web, vérifié · résidence Écritures Liquides**

# Garder un essai que vous pourrez reprendre

Cette arborescence est une convention d'atelier, à créer dans `C:\AI\essais\vos-initiales\`. Un dossier correspond à une question : « Est-ce que mon LoRA conserve la matière du papier ? » Nommez-le `2026-09-23_papier_qwen21_v01`.

```text
2026-09-23_papier_qwen21_v01/
  00-matiere/       originaux, image de départ, son éventuel
  01-dataset/       img01.png + img01.txt, sélection pour le LoRA
  02-recette/       configuration.yaml, A.json, B.json, modeles.txt
  03-sorties/       PNG ou vidéos d'origine, LoRA retenu, échantillons
  notes.txt
```

Gardez les légendes **à côté** des images du dossier d'entraînement, avec le même nom : c'est le format attendu par [AI Toolkit](https://github.com/ostris/ai-toolkit#dataset-preparation). Les originaux restent dans `00-matiere` ; faites vos recadrages dans une copie.

Avant de lancer, nommez l'essai, fixez la graine (`seed` ou `noise_seed`, mode `fixed`) et exportez le workflow par **Workflows → Export**. La graine initialise le bruit du calcul ; le JSON conserve les réglages et les connexions entre blocs. Après le calcul, gardez aussi le JSON correspondant au résultat et le PNG original, dont les métadonnées peuvent contenir la recette. [RandomNoise](https://docs.comfy.org/built-in-nodes/RandomNoise), [export et réouverture](https://docs.comfy.org/get_started/first_generation), [SaveImage](https://docs.comfy.org/built-in-nodes/SaveImage).

Dans `notes.txt`, remplissez ce petit carnet après chaque essai :

```text
Question :
A : fichier, graine, prompt exact, modèle, résolution, étapes, guidage
B : mêmes réglages, sauf ce changement :
Vidéo : image de départ, nombre d'images, cadence, son
Durée de calcul : premier chargement / calcul suivant
Observation : ce qui tient, ce qui disparaît, ce que je garde
Prochaine modification : une seule
```

Pour comparer avec et sans LoRA, gardez tout identique et passez sa force de `0` à `1`. Le mot de code reste dans les deux prompts. Nommez les sorties `A_sans` et `B_avec`. La force zéro annule l'adaptation dans le [nœud de chargement](https://docs.comfy.org/built-in-nodes/LoraLoaderModelOnly). Pour changer de modèle, ouvrez un nouveau dossier et sa recette propre : vous conservez la matière et les légendes, sans supposer que le LoRA sera compatible.

Dans `modeles.txt`, notez les noms complets des poids, leurs liens, leur précision (`fp8`, `int8`…), le LoRA utilisé et les versions des logiciels. `git -C C:\AI\ComfyUI rev-parse HEAD` et `git -C C:\AI\ai-toolkit rev-parse HEAD` donnent les identifiants de version du code. [Git](https://git-scm.com/docs/git-rev-parse). Une graine seule ne garantit pas le même résultat après un changement de versions ou de matériel. [PyTorch](https://docs.pytorch.org/docs/2.11/notes/randomness.html).

Avant de quitter, rouvrez un JSON et vérifiez les noms de modèles, le prompt et la graine. Copiez le dossier sur votre stockage personnel. Cette copie est notre convention de sauvegarde : les sorties de la tour sont partagées. Les sources et leurs dates sont dans [SOURCES.md](SOURCES.md).
