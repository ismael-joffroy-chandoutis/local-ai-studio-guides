**Version : v2026-09-23.1 · 23/09/2026 00h27 Paris · sources : web, vérifié · résidence Écritures Liquides**

# Vos premières images dans ComfyUI

<img src="../images/02-images.jpg" alt="" width="100%">

L'objectif de cette séance : obtenir une image, en produire une variante, puis garder de quoi refaire les deux. Les réglages ci-dessous sont vérifiés dans la documentation et les workflows officiels disponibles le 23 septembre 2026. Ils n'ont pas été exécutés sur la tour de la résidence pendant cette vérification. Aucun temps de calcul ni pic de mémoire propre à cette machine n'est donc garanti.

## 1. Ouvrir le bon ComfyUI

Sur la tour, ouvrez `http://127.0.0.1:8188`. Depuis un autre ordinateur du même réseau, remplacez 127.0.0.1 par l'adresse de la tour. La fiche d'installation donne `C:\AI\ComfyUI` comme dossier du logiciel. Les calculs et les sorties sont communs : convenez d'un ordre de passage et ne lancez pas d'entraînement en même temps. Ces chemins et cette règle de partage viennent de [REF-installation-tour.md](), pas d'une vérification à distance de la machine.

Un **workflow** est une recette visuelle : des blocs, appelés **nœuds**, chargent les modèles, lisent votre texte et calculent l'image. Le fichier `.json` conserve cette recette. Il ne contient pas les gros fichiers de modèles, appelés **poids**. [Présentation de ComfyUI](https://github.com/Comfy-Org/ComfyUI#features).

La fiche d'installation citait Qwen-Image et Flux.1 pour les premières recettes. Ce guide utilise des versions différentes : **Qwen-Image 2.1** et **FLUX.2 [dev] quantifié**. N'utilisez pas automatiquement leurs anciens encodeurs ou leurs anciens VAE. L'encodeur traduit le texte pour le modèle ; le VAE convertit sa représentation interne en image. Les fichiers attendus figurent dans les [documents Qwen 2.1](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1) et [FLUX.2](https://docs.comfy.org/tutorials/flux/flux-2-dev).

## 2. Première recette : Qwen-Image 2.1

### Charger la recette

Téléchargez le [workflow officiel `image_qwen_image_2_1_t2i.json`](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_qwen_image_2_1_t2i.json). Enregistrez le fichier avec son extension `.json`, puis ouvrez-le dans **Workflows → Open**. Vous pouvez aussi chercher « Qwen-Image-2.1 » dans les modèles de workflows et sélectionner **Text to Image**, c'est-à-dire « texte vers image ». [Tutoriel Qwen](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1), [chargement des JSON](https://docs.comfy.org/get_started/first_generation).

### Télécharger les trois fichiers

Ouvrez chaque lien, puis utilisez le bouton de téléchargement de la page. Placez le fichier dans le dossier indiqué **sur la tour Windows**. Un téléchargement lancé dans le navigateur de votre portable arrive sur ce portable : il ne dépose pas le modèle dans `C:\AI` sur la tour. Pour éviter ce détour, téléchargez depuis la session Windows de la tour. Le guide officiel distingue également téléchargement et placement manuel. [Téléchargement depuis les modèles de workflows](https://docs.comfy.org/interface/features/template).

| Fichier à télécharger | Dossier sur la tour |
|---|---|
| [qwen_image_2.1_int8_convrot.safetensors](https://huggingface.co/Comfy-Org/Qwen-Image-2.1/blob/main/diffusion_models/qwen_image_2.1_int8_convrot.safetensors) | `C:\AI\ComfyUI\models\diffusion_models` |
| [qwen3vl_8b_int8_convrot.safetensors](https://huggingface.co/Comfy-Org/Qwen-Image-2.1/blob/main/text_encoders/qwen3vl_8b_int8_convrot.safetensors) | `C:\AI\ComfyUI\models\text_encoders` |
| [qwen_image_2.1_vae_bf16.safetensors](https://huggingface.co/Comfy-Org/Qwen-Image-2.1/blob/main/vae/qwen_image_2.1_vae_bf16.safetensors) | `C:\AI\ComfyUI\models\vae` |

Ce sont les variantes sélectionnées par défaut dans le workflow. `int8` désigne une précision numérique réduite pour diminuer l'occupation mémoire. Le tutoriel propose aussi du `bf16`, plus volumineux ; ce n'est pas notre point de départ. [Fichiers et emplacements officiels](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1).

### Régler et lancer

Après les téléchargements, cliquez sur le fond du workflow et appuyez sur **R** pour actualiser les listes. Choisissez les noms exacts dans les menus de chargement. [Actualisation des modèles](https://docs.comfy.org/basic-concepts/models).

| Réglage | Valeur de départ |
|---|---|
| Format | Carré, environ 1 mégapixel, soit 1024 × 1024 |
| `steps`, étapes de calcul | `25` |
| `cfg`, réglage de guidage | `1` |
| `sampler`, méthode de calcul | `euler` |
| `scheduler`, répartition des étapes | `simple` |
| `seed`, graine de départ | `42`, choix d'atelier arbitraire |
| `control_after_generate` | `fixed`, graine conservée |
| Texte négatif | Vide, comme dans le modèle de workflow |

Les paramètres sont ceux du [JSON officiel Qwen](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_qwen_image_2_1_t2i.json), sauf la graine choisie pour l'exercice. Si le sélecteur de résolution apparaît, choisissez `1:1` et `1.0 MP`. La documentation permet environ `4.0 MP` pour 2048 × 2048 ; gardez cette augmentation pour après le premier essai réussi. [Résolution Qwen](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1).

Remplacez le texte d'exemple dans `prompt` par votre description. Cliquez une seule fois sur **Run**, ou faites **Ctrl + Entrée**. Attendez l'image dans le bloc de sauvegarde. [Raccourcis ComfyUI](https://github.com/Comfy-Org/ComfyUI#shortcuts).

## 3. Deuxième recette : FLUX.2 [dev]

Ici, **FLUX.2 [dev] reste le modèle utilisé**. FLUX.2 [klein] est une autre variante, plus petite, avec d'autres poids et réglages. Ce n'est pas le nom d'un mode rapide que l'on active sur [dev]. Si vous l'essayez plus tard, ouvrez son [guide dédié](https://docs.comfy.org/tutorials/flux/flux-2-klein) et nommez l'essai « klein ».

### Charger le workflow et reconnaître sa version

Ouvrez le [JSON officiel `image_flux2_text_to_image.json`](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_flux2_text_to_image.json) dans **Workflows → Open**. Il ne demande pas d'image de départ. Attention : le fichier consulté le 23 septembre contient un petit décodeur et une option Turbo, alors que le tableau du [tutoriel](https://docs.comfy.org/tutorials/flux/flux-2-dev) indique encore `flux2-vae.safetensors`. Suivez les fichiers ci-dessous pour ce JSON précis.

| Fichier | Dossier sur la tour |
|---|---|
| [flux2_dev_fp8mixed.safetensors](https://huggingface.co/Comfy-Org/flux2-dev/blob/main/split_files/diffusion_models/flux2_dev_fp8mixed.safetensors) | `C:\AI\ComfyUI\models\diffusion_models` |
| [mistral_3_small_flux2_fp8.safetensors](https://huggingface.co/Comfy-Org/flux2-dev/blob/main/split_files/text_encoders/mistral_3_small_flux2_fp8.safetensors) | `C:\AI\ComfyUI\models\text_encoders` |
| [full_encoder_small_decoder.safetensors](https://huggingface.co/black-forest-labs/FLUX.2-small-decoder/blob/main/full_encoder_small_decoder.safetensors) | `C:\AI\ComfyUI\models\vae` |

**Adaptation explicite pour les 32 Go :** remplacez l'encodeur `mistral_3_small_flux2_bf16.safetensors` sélectionné dans le modèle de workflow par la variante `fp8` du tableau. Le dépôt officiel affiche 35,6 Go pour le premier et 18 Go pour le second. Ce changement réduit le volume des poids de l'encodeur ; il ne prouve pas que l'ensemble du calcul tient entièrement dans la carte. [Encodeurs officiels et tailles](https://huggingface.co/Comfy-Org/flux2-dev/tree/main/split_files/text_encoders).

Le modèle de diffusion FP8 mixte reste lui-même très lourd. ComfyUI sait déplacer des parties des modèles vers la mémoire de l'ordinateur, appelée **RAM**, pour ménager celle de la carte graphique, appelée **VRAM**. Gardez cette gestion automatique ; la recette ne suppose pas que tout réside dans les 32 Go. Le temps et la mémoire nécessaires avec cette combinaison précise restent à mesurer sur la tour. [Gestion mémoire ComfyUI](https://github.com/Comfy-Org/ComfyUI#features), [poids du modèle](https://huggingface.co/Comfy-Org/flux2-dev/blob/main/split_files/diffusion_models/flux2_dev_fp8mixed.safetensors).

### Paramètres du premier essai

Gardez `enable_turbo_mode = false`. Réglez 1024 × 1024, une image, `20` étapes, `euler`, `Flux2Scheduler` et `FluxGuidance = 4`. Mettez `noise_seed = 42` et `control_after_generate = fixed`. Dans le sous-graphe, la quantité se règle avec `batch_size = 1` dans [EmptyFlux2LatentImage](https://docs.comfy.org/built-in-nodes/EmptyFlux2LatentImage). Le guidage Flux ne se règle pas dans le même bloc que le CFG de Qwen. Ces valeurs et ces blocs sont visibles dans le [JSON FLUX.2 consulté](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_flux2_text_to_image.json).

Le workflow regroupe certains blocs dans un **sous-graphe**, une recette contenue dans un seul bloc. Pour voir `Steps` ou `FluxGuidance`, double-cliquez dans son fond, hors des champs. **Échap** ramène au niveau précédent. [Manipulation des sous-graphes](https://docs.comfy.org/interface/features/subgraph).

Si l'interface signale le LoRA Turbo manquant même en mode désactivé, le fichier référencé est [Flux_2-Turbo-LoRA_comfyui.safetensors](https://huggingface.co/ByteZSzn/Flux.2-Turbo-ComfyUI/resolve/main/Flux_2-Turbo-LoRA_comfyui.safetensors), à placer dans `models\loras`. Le télécharger n'impose pas de l'activer. Le JSON comporte une branche Turbo à 8 étapes ; gardez-la désactivée pour comparer vos premiers essais. [Branche Turbo du workflow](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_flux2_text_to_image.json).

## 4. Écrire quelque chose que vous pourrez évaluer

Conseil d'atelier : décrivez un sujet, ce qu'il fait, sa place dans le cadre, le lieu, la lumière et la matière de l'image. Commencez par une scène simple. Cette organisation reprend la méthode « sujet, action, style, contexte » du [guide de formulation Black Forest Labs](https://docs.bfl.ai/guides/prompting_guide_flux2). Ce guide concerne surtout les versions Pro et Max : l'exemple suivant est un exercice à tester sur nos modèles locaux, pas une promesse de résultat identique.

> Dans un atelier vide, une chaise en bois rouge est posée de trois quarts, au centre du cadre. Une fenêtre hors champ à gauche éclaire doucement le sol en béton. Plan large à hauteur d'une personne assise. Photographie aux couleurs peu saturées, détails nets dans le bois et les traces du sol.

Conseil d'atelier : pour une image dessinée, remplacez seulement la dernière phrase par « Dessin au crayon de couleur sur papier rugueux, contours irréguliers, aplats légers ». Vous pourrez juger si le changement de matière vous intéresse. Si l'image se disperse, retirez une demande et relancez avec la même graine. Gardez le texte effectivement testé dans votre dossier.

## 5. Garder une image, sa graine et sa recette

Avant le calcul, donnez un préfixe personnel au bloc `Save Image` ou `Save Image Advanced`, par exemple `amina_2026-09-23_chaise_qwen_A`. Les sorties des nœuds de sauvegarde vont dans le dossier `output` de ComfyUI, soit ici `C:\AI\ComfyUI\output`. Le préfixe permet de les reconnaître. [SaveImage](https://docs.comfy.org/built-in-nodes/SaveImage), [SaveImageAdvanced](https://docs.comfy.org/built-in-nodes/SaveImageAdvanced).

Une fois l'image calculée, enregistrez le PNG original depuis son aperçu et faites **Workflows → Export** pour conserver le JSON à côté. Rouvrez ensuite le JSON par **Workflows → Open** et vérifiez le prompt, les noms des modèles et la graine. Les PNG ComfyUI peuvent contenir le workflow dans leurs métadonnées ; les glisser dans le canevas permet de le retrouver quand ces informations sont présentes. Gardez tout de même le JSON séparé. [Export et réouverture](https://docs.comfy.org/get_started/first_generation), [métadonnées PNG](https://docs.comfy.org/built-in-nodes/SaveImage).

La **graine** initialise le bruit à partir duquel le calcul commence. Dans FLUX.2, le modèle de workflow est livré avec `randomize`, qui change cette graine : passez sur `fixed` avant de comparer. Le nombre seul n'archive ni le modèle, ni ses réglages. [RandomNoise](https://docs.comfy.org/built-in-nodes/RandomNoise), [workflow FLUX.2](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_flux2_text_to_image.json).

Un changement de version logicielle ou de matériel peut modifier le résultat malgré une même graine. Conservez donc les versions avec le dossier d’essai. [Limites de reproductibilité PyTorch](https://docs.pytorch.org/docs/2.11/notes/randomness.html).

## 6. Comparer sans se perdre

Méthode d'atelier : appelez le premier essai **A**. Exportez sa recette. Changez une seule chose, par exemple la dernière phrase du prompt, et appelez ce nouvel essai **B**. Conservez modèle, format, graine et paramètres. Ouvrez les deux PNG côte à côte et notez trois observations : cadrage, matière, détail qui compte pour votre projet. « B garde mieux la chaise entière mais efface les traces du sol » est plus utile que « B est mieux ».

Pour comparer Qwen et FLUX.2, gardez la même intention, le même texte de départ et le même format, mais leurs réglages respectifs. Traitez cela comme une comparaison de deux recettes complètes. Le chiffre `42` sert à retrouver chaque essai ; il ne constitue pas une image de départ commune aux deux modèles. La graine ne fixe que le bruit de son propre processus. [Rôle de RandomNoise](https://docs.comfy.org/built-in-nodes/RandomNoise).

## 7. Ce qui coince

| Ce que vous voyez | Première vérification |
|---|---|
| Modèle absent, `Value not in list`, menu vide | Contrôlez le nom et le dossier sur la tour, attendez la fin du téléchargement, puis actualisez avec **R**. Un fichier présent sur votre portable ne suffit pas. [Chargement et actualisation](https://docs.comfy.org/basic-concepts/models). |
| Blocs inconnus en rouge | Le logiciel peut être trop ancien pour les nouveaux blocs natifs, ou leur import a échoué au démarrage. Vérifiez la version de ComfyUI et les journaux `C:\AI\logs\comfy.stderr.log` prévus dans la fiche d'installation. Les tutoriels signalent qu'une fonction peut précéder la publication stable. [Qwen 2.1](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1). |
| `Error while deserializing header` | Le téléchargement peut être incomplet ou corrompu. Comparez la taille avec la page du fichier avant de le télécharger de nouveau. [Diagnostic officiel](https://docs.comfy.org/troubleshooting/model-issues). |
| Erreur de dimensions ou de canaux au décodage | Recontrôlez les trois fichiers de la même recette, surtout le VAE. Ne mélangez pas les fichiers Qwen d'origine, Qwen 2.1, Flux.1 et FLUX.2. [Diagnostic de compatibilité](https://docs.comfy.org/troubleshooting/model-issues), [fichiers Qwen 2.1](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1). |
| `CUDA out of memory` | La mémoire graphique manque. Revenez à une image et à la résolution de départ, vérifiez qu'aucun entraînement ne tourne, puis réessayez. Si cela persiste, conservez l'erreur et le JSON ; les modes mémoire relèvent du lancement du serveur partagé. [Modes mémoire ComfyUI](https://docs.comfy.org/troubleshooting/model-issues). |
| FLUX.2 réclame un VAE différent de celui d'un tutoriel | Le JSON texte-vers-image actuel utilise `full_encoder_small_decoder.safetensors`. Contrôlez le menu VAE de ce workflow. [JSON consulté](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_flux2_text_to_image.json). |
| Le calcul semble long | Distinguez chargement des poids et calcul des étapes. Chronométrez le premier essai puis le suivant. Les chargements et changements de modèle peuvent prendre du temps ; aucune durée vérifiée sur cette tour n'est disponible. [Diagnostic des chargements lents](https://docs.comfy.org/troubleshooting/model-issues). |

Avant de quitter : gardez les deux PNG, leurs deux JSON et une phrase sur le changement testé. Le [guide d'organisation](GUIDE-ORGANISER-SES-ESSAIS.md) propose un rangement commun. Les sources sont regroupées dans [SOURCES.md](SOURCES.md).
