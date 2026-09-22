**Version : v2026-09-23.2 · 23/09/2026 00h27 Paris · sources : web, vérifié · résidence Écritures Liquides**

# Entraîner un LoRA sur vos propres images, de A à Z

Guide pour les résident·es. Un LoRA est un fichier d'adaptation d'un modèle à vos images. Travaillez dans la session Windows de la tour : `C:\AI\ai-toolkit`, interface `http://localhost:8675`. Sur votre ordinateur personnel, « localhost » désignerait votre ordinateur ; la [fiche d'installation](la fiche d installation de la tour, interne) n'expose que ComfyUI aux artistes à distance. [Fonctionnement AI Toolkit](https://github.com/ostris/ai-toolkit#ai-toolkit-ui).

Qwen-Image 2.1 est pris en charge, mais un défaut d'apprentissage a été signalé le 21 septembre. Commencez par un essai court et contrôlez son effet, avant de réserver plusieurs heures. La consommation et la durée exactes sur cette tour ne sont pas vérifiées. [Signalement #1054](https://github.com/ostris/ai-toolkit/issues/1054).

## 0 · Avant de commencer : décidez ce que le modèle doit apprendre

Pour commencer, choisissez une personne, un lieu ou une matière. C'est une méthode d'atelier, pas une limite technique à un seul sujet. Faites des séries séparées pour pouvoir comprendre ce qui change.

Pour chaque image, gardez deux lignes : ce qu'on voit, et ce qu'elle fait dans votre film. Une image floue peut compter pour le film sans être utile à cet essai précis. Gardez ce carnet.

## 1 · Le dossier d'images

- Proposition d'atelier : commencez avec 20 à 40 images choisies. Aucun seuil universel de 15 images n'a été vérifié pour Qwen-Image 2.1.
- Utilisez `.jpg`, `.jpeg` ou `.png`, avec des angles et fonds variés. AI Toolkit adapte les dimensions et regroupe les formats ; il n'agrandit pas les petites images. Vérifiez les cadrages. [Préparation officielle](https://github.com/ostris/ai-toolkit#dataset-preparation).
- Créez une série simple : `C:\AI\datasets\famille-1993\`. Gardez les originaux ailleurs et ne mettez ici que les images choisies.

## 2 · Les légendes

À côté de `img01.jpg`, créez `img01.txt`, contenant seulement sa description. `[trigger]` peut être remplacé par `trigger_word`, mais l'ancien exemple Qwen avertit d'une incompatibilité avec le cache des textes. Pour éviter cette ambiguïté, écrivez directement votre code, ici `amll93`, dans chaque légende et chaque prompt de test. [README](https://github.com/ostris/ai-toolkit#dataset-preparation), [avertissement de l'exemple](https://github.com/ostris/ai-toolkit/blob/main/config/examples/train_lora_qwen_image_24gb.yaml).

```text
amll93, black and white photograph, a woman sitting on a doorstep, soft daylight, slight grain
```

L'anglais est notre convention d'essai, pas une obligation démontrée. Décrivez ce qui est visible ; relisez les légendes automatiques. Choisissez un code distinctif et gardez-le identique partout.

## 3 · La configuration

Dans PowerShell sur la tour, ouvrez l’interface ainsi, puis allez à `http://localhost:8675`. [Gestionnaire officiel](https://github.com/ostris/ai-toolkit/blob/main/manager/__main__.py).

```powershell
Set-Location C:\AI\ai-toolkit
py -3.12 -m manager launch --no-browser
```

1. Ne reprenez pas l'ancien YAML en changeant seulement le nom du modèle. Dans le [dossier d'exemples consulté](https://github.com/ostris/ai-toolkit/tree/main/config/examples), `train_lora_qwen_image_24gb.yaml` concerne Qwen-Image et `train_lora_flux_24gb.yaml` Flux.1. Aucun exemple dédié Qwen-Image 2.1 ou FLUX.2 n'y a été trouvé. `train_lora_flex2_24gb.yaml` concerne **Flex.2**, autre modèle.
2. Dans l'interface, créez un job, c'est-à-dire un entraînement, et choisissez `Qwen-Image-2.1`. Les [réglages officiels de cette entrée](https://github.com/ostris/ai-toolkit/blob/main/extensions_built_in/diffusion_models/ui.tsx) donnent `arch: qwen_image_2`, `name_or_path: Comfy-Org/Qwen-Image-2.1`, quantification modèle et texte `convrot8`, `low_vram: true`. La quantification réduit la précision des poids pour économiser la mémoire. Gardez ces choix ; laissez les images de contrôle vides pour apprendre vos images seules.
3. FLUX.2 a une entrée distincte : `FLUX.2`, architecture `flux2`, modèle `black-forest-labs/FLUX.2-dev`, quantification `qfloat8`. Les variantes `FLUX.2-klein-base-4B` et `9B` ont leurs propres entrées. Ne les intervertissez pas. Ces options ne garantissent pas un entraînement dans 32 Go. [Entrées officielles](https://github.com/ostris/ai-toolkit/blob/main/extensions_built_in/diffusion_models/ui.tsx), [échec FLUX.2 sur 32 Go](https://github.com/ostris/ai-toolkit/issues/872).
4. Nommez l'essai `famille-1993-test`, indiquez `folder_path: C:/AI/datasets/famille-1993`, lot `batch_size: 1`. Proposition d'atelier : rang et alpha 16, résolution `[512]`, 250 pas, sauvegarde et échantillons tous les 125 pas. Le rang règle la taille de l'adaptation. Gardez `lr: 0.0001`, le taux d'apprentissage, et les autres réglages du modèle. Ce test réduit est une proposition à qualifier, pas une recette 5090 validée. Les [valeurs générales de l'interface](https://github.com/ostris/ai-toolkit/blob/main/ui/src/app/jobs/new/jobConfig.ts) sont rang 32, 3 000 pas, lot 1 et sauvegarde tous les 250 pas.
5. Ajoutez trois prompts avec `amll93`, dont une situation absente du dossier. Gardez les graines d'échantillonnage. Dans `Show Advanced`, copiez la configuration complète dans `config\famille-1993-test.yaml` : conservez son indentation. [Éditeur officiel](https://github.com/ostris/ai-toolkit/blob/main/ui/src/app/jobs/new/page.tsx).

## 4 · Lancer

Réservez la tour et attendez que la file ComfyUI soit vide. Fermer l'onglet ne libère pas le serveur. Si la tâche prévue par la fiche est installée, arrêtez-la dans PowerShell avec `Stop-ScheduledTask -TaskName IA104-ComfyUI`, puis vérifiez avec `nvidia-smi` qu'aucun calcul ComfyUI ne reste actif. [Lecture des processus GPU](https://docs.nvidia.com/deploy/nvidia-smi/index.html). Accès refusé : les droits locaux nécessaires ne sont pas établis par la fiche, ne forcez pas l'arrêt. [Microsoft](https://learn.microsoft.com/en-us/powershell/module/scheduledtasks/stop-scheduledtask?view=windowsserver2025-ps).

Dans l’interface, faites `Create Job`, puis démarrez le job enregistré. [Création](https://github.com/ostris/ai-toolkit/blob/main/ui/src/app/jobs/new/page.tsx).

L'alternative pour un YAML enregistré est `& .\.venv\Scripts\python.exe run.py config\famille-1993-test.yaml`. Si l'installation utilise `venv`, remplacez `.venv` par `venv` ; utilisez l'environnement du Toolkit. Les sorties suivent `training_folder`, normalement `output\famille-1993-test\`. [Environnement](https://github.com/ostris/ai-toolkit/blob/main/manager/util.py), [lancement et sorties](https://github.com/ostris/ai-toolkit#training).

## 5 · Regarder pendant que ça tourne

Ouvrez `samples\` et testez le LoRA sauvegardé selon l'étape 6. S'il fonctionne, créez un nouvel essai avec 2 000 pas et sauvegarde tous les 250 : proposition de départ, pas seuil d'apprentissage. Gardez assez de sauvegardes avec `max_step_saves_to_keep: 10`, car le défaut 4 élimine les plus anciennes. [Configuration officielle](https://github.com/ostris/ai-toolkit/blob/main/ui/src/app/jobs/new/jobConfig.ts).

Choisissez selon vos images : ressemblance, variété, capacité à sortir des cadrages appris. Aucun résultat à 2 000 pas ne prouve que vos légendes sont mauvaises. N'interrompez jamais pendant une sauvegarde. [Précaution officielle](https://github.com/ostris/ai-toolkit#training).

## 6 · Utiliser le LoRA dans ComfyUI

1. Arrêtez l'entraînement, puis relancez la tâche ComfyUI : `Start-ScheduledTask -TaskName IA104-ComfyUI`. [Microsoft](https://learn.microsoft.com/en-us/powershell/module/scheduledtasks/start-scheduledtask?view=windowsserver2025-ps).
2. Copiez le `.safetensors` choisi dans `C:\AI\ComfyUI\models\loras\`. Dans le workflow du **même modèle**, insérez `LoraLoaderModelOnly` sur le câble MODEL qui va du chargeur vers la suite du calcul. Rafraîchissez la liste si nécessaire. [Nœud officiel](https://docs.comfy.org/built-in-nodes/LoraLoaderModelOnly).
3. Comparez `strength_model: 0` puis `1`, même prompt avec `amll93`, même graine et mêmes réglages. Essayez ensuite 0,7 si l'effet est excessif. Le code aide à demander le sujet ; son absence ne désactive pas l'adaptation. C'est la force 0 qui annule son effet. [Paramètres du nœud](https://docs.comfy.org/built-in-nodes/LoraLoaderModelOnly).

## 7 · Garder les traces

Gardez images, légendes, YAML, LoRA, échantillons et notes. Relevez `git rev-parse HEAD` dans le dossier du Toolkit : [identifiant du code](https://git-scm.com/docs/git-rev-parse). Suivez la [fiche d'organisation](GUIDE-ORGANISER-SES-ESSAIS.md). La même graine ne garantit pas une image identique après changement de logiciel ou de matériel. [Reproductibilité PyTorch](https://docs.pytorch.org/docs/2.11/notes/randomness.html).

## Ce qui coince le plus souvent

- **Téléchargement refusé** : pour [FLUX.2-dev](https://huggingface.co/black-forest-labs/FLUX.2-dev), acceptez d’abord les conditions d’accès sur Hugging Face. Dans PowerShell, depuis le Toolkit, lancez `& .\.venv\Scripts\hf.exe auth login` et suivez la connexion proposée ; adaptez en `venv` si nécessaire. Ne copiez pas de jeton dans le YAML partagé. [Authentification officielle](https://huggingface.co/docs/huggingface_hub/guides/cli#hf-auth-login).
- **LoRA chargé mais sans effet** : le [signalement #1054 du 21/09/2026](https://github.com/ostris/ai-toolkit/issues/1054), encore ouvert lors de la consultation, décrit des poids restés nuls après 2 000 pas sous Windows, RTX 4060 Ti, avec checkpointing et transfert de couches en RAM. Une courbe d'erreur normale ne prouve donc pas l'apprentissage. Si vos comparaisons restent identiques, gardez les fichiers et le numéro de version ; ne lancez pas plus longtemps. L'auteur dit son contournement incomplet, aucun correctif fiable pour cette tour n'est établi ici.
- **Mémoire pleine avant le premier pas** : [#484](https://github.com/ostris/ai-toolkit/issues/484) décrit un échec pendant les échantillons sur une 5090, avec l'ancien Qwen. Réduisez leur résolution avant d'accuser le dossier d'images. Pour FLUX.2-dev, [#872, 08/06/2026](https://github.com/ostris/ai-toolkit/issues/872), décrit un débordement au chargement de Mistral malgré 32 Go de VRAM et 128 Go de RAM. Aucun volume universel de téléchargement ou de mémoire n'est retenu.
- **Tout devient très lent** : [#1003, 09/08/2026](https://github.com/ostris/ai-toolkit/issues/1003), rapporte environ 80 Go de mémoire virtuelle avec Klein 9B sur une RTX 3080 de 12 Go. C'est un témoignage sur une autre machine, pas le temps attendu ici. Notez vos secondes par pas après chargement pour estimer votre créneau.

## Vérifié le 23/09/2026

Sources consultées : [README](https://github.com/ostris/ai-toolkit), [exemples YAML](https://github.com/ostris/ai-toolkit/tree/main/config/examples), [paramètres des modèles](https://github.com/ostris/ai-toolkit/blob/main/extensions_built_in/diffusion_models/ui.tsx), signalements et documentations liés dans chaque étape. Le [registre complet](SOURCES.md) précise dates, limites et anciennes références écartées. Vérification documentaire ; aucun entraînement exécuté sur la tour pour ce guide.
