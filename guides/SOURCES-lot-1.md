**Version : v2026-09-23.1 · 23/09/2026 00h27 Paris · sources : web, vérifié · résidence Écritures Liquides**

# Sources des guides

Toutes les sources ci-dessous ont été consultées le **23/09/2026**. Lorsqu'aucune date de publication n'est indiquée, la date vaut pour la consultation seulement. Les branches `main` et `master` ainsi que les pages de documentation évoluent : conservez les JSON et les configurations effectivement utilisés.

« Officiel » signifie publié par l'équipe du logiciel ou du modèle. Un signalement GitHub est le témoignage de son auteur, avec sa machine et sa configuration ; il ne prouve ni une panne générale ni un correctif. Les conseils d'atelier sont identifiés comme tels dans les guides. Aucun entraînement, rendu vidéo ou benchmark n'a été exécuté sur la tour pendant cette vérification.

## Installation locale

Fiche d'installation de la station de travail (document interne, non publié), fiche du 07/09/2026 fournie avec le dossier : chemins `C:\AI`, environnements distincts, ports 8188 et 8675, tâche `IA104-ComfyUI`, accès Tailscale, partage du GPU. Cette référence décrit une installation cible, pas un inventaire contrôlé en direct. Elle ne démontre pas que les résident·es disposent des droits Windows pour arrêter la tâche, ni que le port 8675 leur est accessible à distance. Ses versions de pilotes et de dépendances n'ont pas été requalifiées dans ces guides.

## LoRA et AI Toolkit

| Source consultée | Date ou état | Ce qui en a été retenu |
|---|---|---|
| [AI Toolkit, README](https://github.com/ostris/ai-toolkit) ; [texte brut](https://raw.githubusercontent.com/ostris/ai-toolkit/main/README.md) | Branche main, consultée le 23/09 | Modèles pris en charge, légendes appariées aux images, formats, redimensionnement, interface, sorties, risque d'interruption pendant une sauvegarde. |
| [Dossier config/examples](https://github.com/ostris/ai-toolkit/tree/main/config/examples) | Arborescence affichée lors de la consultation | Noms réellement listés ; aucun YAML dédié Qwen-Image 2.1 ou FLUX.2 trouvé. Flux.1 et Flex.2 ne sont pas FLUX.2. |
| [train_lora_qwen_image_24gb.yaml](https://raw.githubusercontent.com/ostris/ai-toolkit/main/config/examples/train_lora_qwen_image_24gb.yaml) | Exemple pour Qwen-Image original | Rang 16, 2 000 pas, cache des textes, quantification uint3 avec adaptateur de compensation ; avertissement sur trigger et cache. Ces réglages ne sont pas transposés à Qwen 2.1. |
| [Entrées des modèles dans l'interface](https://raw.githubusercontent.com/ostris/ai-toolkit/main/extensions_built_in/diffusion_models/ui.tsx) | Main | Qwen 2.1 : architecture qwen_image_2, dépôt Comfy-Org, convrot8. FLUX.2-dev et klein : entrées distinctes. Défauts du logiciel, sans garantie de mémoire. |
| [Configuration générale des jobs](https://raw.githubusercontent.com/ostris/ai-toolkit/main/ui/src/app/jobs/new/jobConfig.ts) | Main | Rang 32, lot 1, lr 0,0001, 3 000 pas, sauvegarde 250 et rétention de quatre sauvegardes. |
| [Page de création](https://raw.githubusercontent.com/ostris/ai-toolkit/main/ui/src/app/jobs/new/page.tsx) | Main | Import YAML/JSON, Show Advanced, Create Job ; l'import peut reprendre le dossier de sorties des paramètres de l'interface. |
| [Formulaire SimpleJob](https://raw.githubusercontent.com/ostris/ai-toolkit/main/ui/src/app/jobs/new/SimpleJob.tsx) ; [options](https://raw.githubusercontent.com/ostris/ai-toolkit/main/ui/src/app/jobs/new/options.tsx) | Main | Champs de graine, échantillons, quantification et accès aux réglages. |
| [Chargement des entrées de modèles](https://raw.githubusercontent.com/ostris/ai-toolkit/main/ui/src/extensions/modelArchs.ts) | Main | Recoupement : les valeurs spécifiques viennent des extensions ; l'ancien emplacement des options ne suffit plus. |
| [Code Qwen 2.1](https://raw.githubusercontent.com/ostris/ai-toolkit/main/extensions_built_in/diffusion_models/qwen_image_2/qwen_image_2.py) ; [transformer](https://raw.githubusercontent.com/ostris/ai-toolkit/main/extensions_built_in/diffusion_models/qwen_image_2/src/transformer.py) ; [initialisation](https://raw.githubusercontent.com/ostris/ai-toolkit/main/extensions_built_in/diffusion_models/qwen_image_2/__init__.py) | Main | Architecture propre, provenance des poids et noms LoRA ; invalide le remplacement du seul nom dans un vieux YAML. Lecture du code, pas validation d'un correctif d'entraînement. |
| [Gestionnaire CLI](https://raw.githubusercontent.com/ostris/ai-toolkit/main/manager/__main__.py) ; [chemins des environnements](https://raw.githubusercontent.com/ostris/ai-toolkit/main/manager/util.py) | Main | launch --no-browser ; .venv préféré, venv également reconnu ; lancement avec le Python de l'environnement. |
| [LoRA sans effet, #1054](https://github.com/ostris/ai-toolkit/issues/1054) | Ouvert le 21/09/2026, affiché ouvert | RTX 4060 Ti 16 Go, Windows, entraînement Qwen 2.1 dont les poids restent nuls ; contournement déclaré incomplet par l'auteur. Test avec/sans avant entraînement long. |
| [Qwen et mémoire 5090, #484](https://github.com/ostris/ai-toolkit/issues/484) | Ouvert le 26/10/2025 ; affiché fermé sans correctif associé | Échec au calcul des échantillons sur l'ancien Qwen. Les réponses indexées incluent février 2026 ; ce n'est pas un test Qwen 2.1. |
| [FLUX.2-dev et mémoire, #872](https://github.com/ostris/ai-toolkit/issues/872) | Ouvert le 08/06/2026, affiché ouvert | Échec de chargement/quantification Mistral malgré 32 Go VRAM et 128 Go RAM. Pas de garantie « 24 à 32 Go suffisent ». |
| [Klein 9B et mémoire virtuelle, #1003](https://github.com/ostris/ai-toolkit/issues/1003) | Ouvert le 09/08/2026 | Retour Windows 10, RTX 3080 12 Go, RAM 64 Go ; charge mémoire et lenteur propres à cette configuration. |
| [Klein 9B sous WSL, #836](https://github.com/ostris/ai-toolkit/issues/836) | 19/05/2026, affiché fermé | Lu pour recoupement : erreur de chargement, RTX 6000 Blackwell sous WSL. Non transposé à Windows natif sur la tour. |
| [Klein, qfloat8, 5090 et WSL, #989](https://github.com/ostris/ai-toolkit/issues/989) | 01/08/2026, affiché ouvert | Retour de pertes du GPU pendant les transferts ; contexte WSL et pile différents. Aucun correctif repris. |
| [Chargement LoRA ComfyUI](https://github.com/Comfy-Org/ComfyUI/blob/master/comfy/lora.py) | Master | Recoupement des correspondances de noms Qwen 2.1. Un chargement accepté ne démontre pas un apprentissage effectif. |
| [LoraLoaderModelOnly](https://docs.comfy.org/built-in-nodes/LoraLoaderModelOnly) | Documentation courante | Dossier loras, entrée/sortie MODEL, force zéro et comparaison avec/sans. |
| [FLUX.2-dev, dépôt BFL](https://huggingface.co/black-forest-labs/FLUX.2-dev) ; [CLI Hugging Face](https://huggingface.co/docs/huggingface_hub/guides/cli) | Pages courantes | Conditions d'accès au modèle, authentification hf auth login. |

Arborescences supplémentaires consultées pour trouver les bons fichiers : [ui/src](https://github.com/ostris/ai-toolkit/tree/main/ui/src), [jobs/new](https://github.com/ostris/ai-toolkit/tree/main/ui/src/app/jobs/new), [diffusion_models/flux2](https://github.com/ostris/ai-toolkit/tree/main/extensions_built_in/diffusion_models/flux2). Ces pages servent à localiser le code, pas à justifier un réglage.

## Anciennes références du guide LoRA

| Référence relue | Date | Décision |
|---|---|---|
| [Kombitz, entraînement Qwen](https://www.kombitz.com/2025/09/15/how-to-train-a-qwen-image-lora-with-ai-toolkit-with-ai-toolkit/) | 15/09/2025 | Témoignage direct, mais ancien Qwen. Le temps annoncé pour sa 5090 et les réglages ne sont pas transférés à Qwen 2.1. |
| [Local AI Master](https://localaimaster.com/blog/ai-toolkit-lora-training-guide) | Date de publication non établie dans cette vérification | Consulté, non retenu pour des réglages techniques faute de preuve primaire associée à notre recette. |
| [RunComfy, Qwen-Image 2.1](https://www.runcomfy.com/trainer/ai-toolkit/qwen-image-2-1-lora-training) | Date de publication non établie | Page peu extractible lors de la consultation ; aucune promesse de VRAM ou de durée reprise. |
| [Diffusion Doodles, Chris Green](https://diffusiondoodles.substack.com/p/how-to-train-a-lora-ostris-ai-toolkit) | Date non relevée | Consulté pour recoupement ; les instructions opératoires des guides reposent sur le dépôt officiel courant. |

## Images : Qwen-Image 2.1 et FLUX.2

| Source consultée | Date ou état | Apport |
|---|---|---|
| [Tutoriel Qwen 2.1](https://docs.comfy.org/tutorials/image/qwen/qwen-image-2-1) | Documentation consultée le 23/09 | Trois composants, résolution, 25 étapes, CFG 1, Euler/simple, avertissement de version. |
| [JSON Qwen texte vers image](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_qwen_image_2_1_t2i.json) | Main | Champs et fichiers exacts, sortie du workflow. |
| [Poids Qwen 2.1 int8](https://huggingface.co/Comfy-Org/Qwen-Image-2.1/blob/main/diffusion_models/qwen_image_2.1_int8_convrot.safetensors) | Page de fichier | Nom et existence du modèle de diffusion. |
| [Encodeur Qwen3-VL int8](https://huggingface.co/Comfy-Org/Qwen-Image-2.1/blob/main/text_encoders/qwen3vl_8b_int8_convrot.safetensors) | Page de fichier | Nom et existence de l'encodeur. |
| [VAE Qwen 2.1](https://huggingface.co/Comfy-Org/Qwen-Image-2.1/blob/main/vae/qwen_image_2.1_vae_bf16.safetensors) | Page de fichier | Nom et existence du VAE dédié. |
| [Équipe Qwen, README 2.1](https://github.com/QwenLM/Qwen-Image-2.1/blob/main/README.md) | Source indexée lors de la recherche | Recoupement de la nouvelle architecture et de l'intégration ComfyUI. |
| [Tutoriel FLUX.2-dev](https://docs.comfy.org/tutorials/flux/flux-2-dev) | Documentation courante | Usage local ; écart avec le VAE du JSON actuel signalé. |
| [JSON FLUX.2 texte vers image](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/image_flux2_text_to_image.json) | Main | Petit décodeur, branche standard 20 étapes, guidage 4, Turbo désactivé, graine et lot. |
| [FLUX.2 dev FP8 mixte](https://huggingface.co/Comfy-Org/flux2-dev/blob/main/split_files/diffusion_models/flux2_dev_fp8mixed.safetensors) | Page de fichier | Modèle sélectionné pour la recette locale. |
| [Encodeur Mistral FP8](https://huggingface.co/Comfy-Org/flux2-dev/blob/main/split_files/text_encoders/mistral_3_small_flux2_fp8.safetensors) ; [liste des encodeurs](https://huggingface.co/Comfy-Org/flux2-dev/tree/main/split_files/text_encoders) | Pages de fichiers | Variante proposée à la place du BF16, tailles respectives 18 et 35,6 Go. |
| [Petit décodeur BFL](https://huggingface.co/black-forest-labs/FLUX.2-small-decoder/blob/main/full_encoder_small_decoder.safetensors) | Page de fichier | VAE réellement demandé par le JSON, commun aux branches standard et Turbo. |
| [Guide FLUX.2-klein](https://docs.comfy.org/tutorials/flux/flux-2-klein) | Documentation courante | Distinction klein/dev, pas de substitution implicite. |
| [Guide de prompt BFL](https://docs.bfl.ai/guides/prompting_guide_flux2) | Documentation courante, surtout Pro/Max | Structure de description ; adaptation comme exercice local, pas garantie de résultats équivalents. |

Le lien binaire [Flux_2-Turbo-LoRA_comfyui.safetensors](https://huggingface.co/ByteZSzn/Flux.2-Turbo-ComfyUI/resolve/main/Flux_2-Turbo-LoRA_comfyui.safetensors) est relevé dans le JSON officiel consulté. Le binaire n'a pas été téléchargé ni validé ; cette branche reste désactivée dans l'exercice.

## Gestes communs, organisation et Windows

| Source consultée | Ce qui en a été pris |
|---|---|
| [Première génération ComfyUI](https://docs.comfy.org/get_started/first_generation) | Import/export JSON, glisser un PNG, Run et actualisation. |
| [Modèles ComfyUI](https://docs.comfy.org/basic-concepts/models) | Poids séparés du workflow, placement et sélection. |
| [Bibliothèque de workflows](https://docs.comfy.org/interface/features/template) | Recherche, fichiers manquants et téléchargement depuis le navigateur. |
| [Sous-graphes](https://docs.comfy.org/interface/features/subgraph) | Accéder aux paramètres regroupés. |
| [SaveImage](https://docs.comfy.org/built-in-nodes/SaveImage) ; [SaveImageAdvanced](https://docs.comfy.org/built-in-nodes/SaveImageAdvanced) | Préfixe, sorties et métadonnées. |
| [RandomNoise](https://docs.comfy.org/built-in-nodes/RandomNoise) ; [EmptyFlux2LatentImage](https://docs.comfy.org/built-in-nodes/EmptyFlux2LatentImage) | Graine et taille du lot. |
| [Dépôt ComfyUI](https://github.com/Comfy-Org/ComfyUI) | Gestion des modèles entre RAM et VRAM. |
| [Diagnostic des modèles](https://docs.comfy.org/troubleshooting/model-issues) | Fichiers incomplets, incompatibilités et mémoire. |
| [Reproductibilité PyTorch 2.11](https://docs.pytorch.org/docs/2.11/notes/randomness.html) | Limites entre versions et matériels ; graine insuffisante pour archiver une expérience. |
| [Git rev-parse](https://git-scm.com/docs/git-rev-parse) | Relever l'identifiant de version du code. |
| [NVIDIA nvidia-smi](https://docs.nvidia.com/deploy/nvidia-smi/index.html) | Lecture de la mémoire et des processus GPU. |
| [Microsoft Stop-ScheduledTask](https://learn.microsoft.com/en-us/powershell/module/scheduledtasks/stop-scheduledtask?view=windowsserver2025-ps) ; [Start-ScheduledTask](https://learn.microsoft.com/en-us/powershell/module/scheduledtasks/start-scheduledtask?view=windowsserver2025-ps) | Arrêt et relance de la tâche prévue par la fiche de la tour. |

## Vidéo : Wan 2.2 et LTX-2.3

| Source consultée | Date ou état | Apport |
|---|---|---|
| [Tutoriel Wan](https://docs.comfy.org/tutorials/video/wan/wan2_2) | Documentation courante | Fichiers 5B, activation de l'image, offload ComfyUI annoncé dès 8 Go ; variantes 14B distinctes. |
| [JSON Wan 5B](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/video_wan2_2_5B_ti2v.json) | Main | 1280 × 704, 121 images, 24 fps, 20 étapes, CFG 5, uni_pc/simple, shift 8, image désactivée initialement, sortie sans audio. |
| [Dépôt Wan](https://github.com/Wan-Video/Wan2.2) | Documentation courante | Commande 5B avec transfert en RAM dès 24 Go ; annonce de cinq secondes 720p en moins de neuf minutes ; exigences des commandes 14B. Ce n'est pas une mesure ComfyUI Windows. |
| [Poids Wan Comfy-Org](https://huggingface.co/Comfy-Org/Wan_2.2_ComfyUI_Repackaged) | Dépôt de fichiers | Provenance des poids reconditionnés pour ComfyUI. |
| [Tutoriel LTX-2.3](https://docs.comfy.org/tutorials/video/ltx/ltx-2-3) | Documentation courante | Cinq fichiers du I2V actuel ; différence avec le workflow première/dernière image. |
| [JSON LTX-2.3 I2V](https://raw.githubusercontent.com/Comfy-Org/workflow_templates/main/templates/video_ltx2_3_i2v.json) | Main | Valeurs effectives, deux passes 8 + 3 étapes, CFG 1, durée × cadence + 1 ; écart de dimensions entre défaut visible et contraintes du modèle signalé. |
| [Fiche Lightricks LTX-2.3](https://huggingface.co/Lightricks/LTX-2.3) | Fiche du modèle | Anglais, génération audiovisuelle, multiples de 32 et 8n + 1, limites du son sans parole. |
| [Dépôt LTX-2](https://github.com/Lightricks/LTX-2) | Documentation courante, section legacy 2.3 | Séparation entre composants 2.3 et 2.5. |
| [Checkpoint BF16](https://huggingface.co/Lightricks/LTX-2.3/blob/main/ltx-2.3-22b-dev.safetensors) ; [checkpoint FP8](https://huggingface.co/Lightricks/LTX-2.3-fp8/blob/main/ltx-2.3-22b-dev-fp8.safetensors) | Pages de fichiers | Tailles 46,1 et 29,1 Go ; la taille sur disque ne mesure pas la consommation totale GPU. |
| [Guide de prompt LTX](https://docs.ltx.io/open-source-model/usage-guides/prompting-guide) | Page désormais aussi consacrée à 2.5 | Conseils généraux de rédaction seulement : action, caméra, son. |
| [Négatif inopérant, workflow_templates #919](https://github.com/Comfy-Org/workflow_templates/issues/919) | 03/06/2026 | Retour d'utilisateur sur le CFG 1 ; valeur recoupée dans le JSON. |
| [Variation de vitesse, LTX-2 #224](https://github.com/Lightricks/LTX-2/issues/224) | 30/05/2026 | Retour RTX 5090 avec SageAttention, environ 34 puis 60 à 70 secondes. Nombre d'images ambigu, non utilisé comme benchmark transférable. |
| [Mémoire LTX, ComfyUI #14683](https://github.com/Comfy-Org/ComfyUI/issues/14683) | 30/06/2026 | Débordement 5090 avec RAM 200 Go ; nœuds tiers dans les traces, aucune généralisation au workflow natif. |
| [KSampler](https://docs.comfy.org/built-in-nodes/sampling/ksampler) | Documentation courante, extrait code daté du 15/05/2025 | Graine, CFG et étapes. |
| [Workflows ComfyUI](https://docs.comfy.org/basic-concepts/workflow) | Documentation courante | Nœuds, JSON, conservation des réglages. |
| [Code SaveVideo](https://raw.githubusercontent.com/Comfy-Org/ComfyUI/master/comfy_extras/nodes_video.py) | Master | Préfixe, dossier output, compteur, format MP4 automatique. |
| [Métadonnées des workflows](https://docs.comfy.org/development/api-development/workflow-metadata) | Documentation courante | Métadonnées vidéo ; garder séparément JSON, sources et poids. |
| [Configuration matérielle LTX](https://docs.ltx.io/open-source-model/getting-started/system-requirements) ; [I2V LTX](https://docs.ltx.io/open-source-model/usage-guides/image-to-video) | Pages décrivant désormais 2.5 | Consultées, non utilisées pour attribuer un minimum mémoire ou des paramètres à 2.3. |

## Recoupements et navigation complémentaires

[Sources MDX du tutoriel FLUX.2](https://raw.githubusercontent.com/Comfy-Org/docs/main/tutorials/flux/flux-2-dev.mdx) et [Qwen 2.1](https://raw.githubusercontent.com/Comfy-Org/docs/main/tutorials/image/qwen/qwen-image-2-1.mdx) : liens des JSON officiels. [Index ComfyUI](https://docs.comfy.org/llms.txt) et [arborescence des templates](https://github.com/Comfy-Org/workflow_templates/tree/main/templates) : navigation, liste GitHub partiellement tronquée. [Dépôt small-decoder](https://huggingface.co/black-forest-labs/FLUX.2-small-decoder) et [arborescence des poids FLUX.2](https://huggingface.co/Comfy-Org/flux2-dev/tree/main/split_files/diffusion_models) : recoupement des noms. [Discussion FLUX.2 n°16](https://huggingface.co/Comfy-Org/flux2-dev/discussions/16) : ajout d'un guide de placement ; aucun conseil supplémentaire repris.

## Limites de consultation

Des adresses présumées ont renvoyé une erreur ou aucun contenu exploitable : `train_lora_qwen_image_2_1.yaml`, `train_lora_flux2_24gb.yaml`, `manager/paths.py`, `jobs/new/options.ts`, `qwen_image_2/ui.tsx`, et plusieurs anciennes adresses de documentation ComfyUI. Elles ne sont pas utilisées comme preuves d'absence : les conclusions reposent sur les arborescences et les fichiers effectivement lus. L'API GitHub n'était pas accessible par le terminal ; les pages GitHub et leurs sources brutes ont été consultées sur le web.

Les durées propres à la tour, ses pics de mémoire, les droits d'accès effectifs et la réussite d'un LoRA Qwen 2.1 dans cet environnement restent **non vérifiés**. Les guides donnent des essais de qualification explicites, sans les présenter comme déjà réussis.
