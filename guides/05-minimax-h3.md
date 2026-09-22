**Version : v2026-09-23.1 · 23/09/2026 00h39 Paris · sources : web, vérifié · résidence Écritures Liquides**

# MiniMax H3 : vidéo, références et conditions d'accès

**Pour la résidence en France, commencez par l'accès en ligne.** Les poids de MiniMax H3 sont téléchargeables, mais leur licence communautaire exclut l'Union européenne. « Poids ouverts » signifie que les fichiers appris par le modèle sont accessibles ; cela ne signifie pas que leur utilisation est autorisée partout. [Licence officielle](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/LICENSE), [FAQ officielle sur la différence entre API et poids](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/QA-about-License.md).

## Ce que H3 permet de faire

H3 combine texte, images, vidéos et sons pour produire de la vidéo accompagnée d'audio stéréo. Le système officiel annonce 4 à 15 secondes à 24 images par seconde, jusqu'à 2K. Il propose une famille **FL2VA**, pour partir du texte ou d'une première et/ou dernière image, et une famille **Ref2VA**, pour travailler avec plusieurs références. La fiche autorise jusqu'à 9 images, 3 vidéos et 3 sons, dans une limite totale de 12 fichiers ; les vidéos et sons ont également des limites de durée. [Fiche officielle du modèle](https://huggingface.co/MiniMaxAI/MiniMax-H3).

Les limites exactes d'un service hébergé peuvent différer de celles des poids : fal.ai annonce notamment des clips H3 de 5 à 15 secondes. Consultez les paramètres de la page choisie avant de préparer vos références. [H3 sur fal.ai](https://fal.ai/minimax-h3).

## Un premier essai en ligne

Sur **Hailuo**, l'application de MiniMax, ouvrez votre compte, vérifiez que le modèle sélectionné est H3, choisissez votre mode, joignez vos références et relisez le coût affiché avant de créer. La page publique annonce bien H3 et présente le mode **Omni Reference**. Le nombre de crédits et les options accessibles à votre compte après connexion ne sont pas vérifiés dans ce guide. [Hailuo](https://hailuoai.video/).

Sur **fal.ai**, choisissez la page correspondant à votre geste : [texte vers vidéo](https://fal.ai/models/minimax/h3/text-to-video), [image vers vidéo et première/dernière image](https://fal.ai/models/minimax/h3/image-to-video), ou [références vers vidéo](https://fal.ai/models/minimax/h3/reference-to-video). Utilisez d'abord le formulaire **Playground**, l'espace d'essai dans le navigateur. Si le compte fal.ai est partagé, la dépense se valide avec la personne qui le tient avant le lancement. [Présentation des trois modes](https://fal.ai/minimax-h3).

Pour votre premier essai, choisissez une action unique et expliquez le rôle de chaque référence. Exemple de consigne à adapter : « Utilisez l'image 1 pour le personnage et la vidéo 1 pour le mouvement du corps. Plan fixe dans une pièce vide. Le personnage s'assoit lentement. On entend le frottement de la chaise, sans musique. » Ce texte est un exemple pédagogique, pas un résultat garanti. [Guide de consignes MiniMax](https://design.minimax.io/h3).

Au relevé du 23 septembre, la page **H3 texte vers vidéo** affiche **0,06 $ par seconde en 768p**, soit **0,30 $ pour 5 secondes**, et **0,13 $ par seconde en 2K**, soit **0,65 $ pour 5 secondes**. Ces calculs concernent cette page précise. Ne transposez pas son prix aux références ou à **H3 Max**, une variante retravaillée par fal. [Tarif H3](https://fal.ai/models/minimax/h3/text-to-video), [présentation H3 Max](https://fal.ai/models/minimax/h3-max/text-to-video).

## La licence : ce qui est écrit, et ce que cela change ici

La **MiniMax H3 Community License Agreement**, datée du **2 août 2026**, définit ainsi les territoires exclus, section I.5 :

> “Excluded Territories” means the European Union, the United Kingdom, the Republic of Korea and the United States of America.

La section II limite les droits accordés au territoire autorisé. La section V.4 vise aussi l'utilisation et la diffusion des résultats hors de ce territoire. **La licence communautaire seule n'autorise donc pas la résidence à exploiter les poids localement en France ni à y entraîner un LoRA.** Déplacer le calcul hors de l'UE ne règle pas à lui seul la restriction sur les résultats. C'est une lecture du périmètre contractuel, pas un avis juridique. [Texte officiel, I.5, II et V.4](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/LICENSE).

MiniMax distingue l'API, annoncée disponible mondialement avec ses contrôles, de la distribution des poids. Les organisations situées dans les territoires exclus peuvent demander une **autorisation spécifique** : une demande n'est pas une autorisation acquise. Pour un entraînement hébergé ou l'export d'un LoRA, faites confirmer les droits du service et l'usage prévu ; un badge d'usage commercial ne constitue pas automatiquement une licence locale des poids. [FAQ officielle et lien vers la demande de licence](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/QA-about-License.md).

## En local : techniquement possible, sous autorisation adaptée

Les deux familles de poids existent. Le système complet comporte toutefois des étapes de préparation des références et de régénération en 2K qui ne sont pas toutes incluses dans la publication ouverte décrite par MiniMax. Un résultat local H3-Base n'est donc pas automatiquement celui du service complet. [Architecture et disponibilité des modules](https://github.com/MiniMax-AI/MiniMax-H3).

ComfyUI propose des modèles de travail dans **Template Library > Video > MiniMax H3**, avec les fichiers adaptés par Comfy-Org. Cette voie nécessite une version compatible de ComfyUI et tous les composants du modèle. Le guide décrit cette possibilité pour vous orienter ; il ne recommande pas de lancer les poids en France sans les droits appropriés. [Tutoriel ComfyUI](https://docs.comfy.org/tutorials/video/minimax/minimax-h3).

**32 Go permettent certaines configurations réduites, pas toutes.** La quantification réduit la précision des nombres stockés pour diminuer la mémoire nécessaire. L'offloading déplace une partie des données vers la RAM, la mémoire générale du PC. Un essai publié le 3 septembre 2026 sur une RTX 5090, sous Ubuntu avec 93 Go de RAM utilisables, fournit ces repères pour un clip de 5,17 secondes en 1344 × 768 :

| Configuration mesurée | Temps total | Pic de VRAM |
| --- | --- | --- |
| Poids réduits NVFP4, 20 étapes | 260,4 s, environ 4 min 20 | 27 Go |
| Poids réduits INT8, LoRA d'accélération, 4 étapes | 70,1 s | 31,3 Go |

Une étape est un passage de calcul, pas une image de la vidéo. Ce sont les mesures d'un auteur sur un cas, **pas un temps promis sur votre Windows**. Dans le même essai, les poids complets BF16 échouent par manque de RAM. [Protocole, chiffres et limites du test](https://umarsalim.com/blog/minimax-h3-on-one-rtx-5090/).

## Entraîner un LoRA : choisir la bonne tâche

Un **LoRA** est une adaptation légère chargée avec le modèle de base : par exemple pour apprendre un personnage ou une transformation. Un LoRA d'accélération sert, lui, à réduire les étapes de génération ; ce n'est pas votre LoRA de personnage. AI Toolkit prend en charge H3, et des outils d'intégration existent pour ComfyUI. Aucun minimum de VRAM ni temps d'entraînement universel, suffisamment documenté pour votre configuration Windows de 32 Go, n'a été établi dans cette vérification. [Panorama officiel des outils H3](https://design.minimax.io/h3), [AI Toolkit](https://github.com/ostris/ai-toolkit).

fal propose trois entraîneurs distincts. Une **étape d'entraînement** est une mise à jour de l'adaptation à partir des exemples, et non une seconde de vidéo :

| Tâche et page officielle | Prix par étape | Exemple calculé pour 2 000 étapes |
| --- | --- | --- |
| [Texte vers vidéo](https://fal.ai/models/minimax/h3/t2v/trainer) | 0,005 $ | 10 $ |
| [Première/dernière image](https://fal.ai/models/minimax/h3/flf2v/trainer) | 0,010 $ | 20 $ |
| [Références vers vidéo](https://fal.ai/models/minimax/h3/ref2va/trainer) | 0,015 $ | 30 $ |

Ces pages indiquent un minimum facturé de 100 étapes pour un entraînement réussi. Ajoutez le prix des générations de validation : produire le fichier LoRA ne prouve pas son efficacité. Le coût local, lorsqu'il est autorisé, dépend du temps de location de votre tour ; aucun tarif de location ni devis local H3 n'est établi ici.

Préparez des clips et des descriptions correspondantes dans une archive ZIP, selon le format exact de l'entraîneur. Pour le mode première/dernière image, fal demande des vidéos, recommande au moins dix clips et peut ignorer ceux qui sont trop courts. Ne lancez pas un entraînement avec un dossier d'images en supposant qu'il conviendra à tous les modes. [Format de données FLF](https://fal.ai/models/minimax/h3/flf2v/trainer).

Pour Ref2VA, les références doivent accompagner les exemples. Sans référence explicite, l'entraîneur peut prendre une image au milieu du clip ; sans bande-son, il peut apprendre sur du silence. Les options `debug_dataset` et `strict_dataset` servent respectivement à inspecter les données préparées et à refuser certains remplacements automatiques. [Préparation et contrôles Ref2VA](https://fal.ai/models/minimax/h3/ref2va/trainer).

## Si votre LoRA reste « muet »

Un LoRA de référence sans effet visible a été signalé dans le cadre de la résidence. **Ce cas n'est pas vérifiable publiquement ; sa cause n'est pas établie.** « Muet » signifie ici « sans effet observable », pas nécessairement « sans piste audio ». Gardez cette distinction au moment de décrire le problème.

Avant de payer un nouvel entraînement, faites un diagnostic comparatif :

1. Gardez le même modèle, la même consigne, les mêmes références et la même graine, le nombre qui initialise l'aléatoire. Comparez une génération sans LoRA, puis avec le LoRA et la force prévue par son exemple.
2. Vérifiez la famille de base, FL2VA ou Ref2VA, et les messages de chargement. Un problème de compatibilité des poids officiels non réduits a notamment été rapporté dans AI Toolkit 0.12.8 le 8 août 2026 ; ce rapport ne prouve pas que votre installation actuelle a ce défaut. [Signalement original](https://github.com/ostris/ai-toolkit/issues/1001).
3. Vérifiez que la préparation des vidéos est la même à l'entraînement et à la génération. Le nœud **AI-Toolkit H3 Reference Video**, publié par Ostris, vise précisément cet alignement : 24 images par seconde, durée, dimensions et découpe compatibles. Le nombre d'images suit une forme particulière, `17 × n + 5`, par exemple 124 images. [Outil et exemple d'Ostris](https://github.com/ostris/ComfyUI-AIToolkit-MiniMaxH3).
4. Si « muet » désigne réellement l'absence de son, écoutez les clips d'entraînement et vérifiez aussi la sortie audio de votre chaîne. Un entraînement sur des clips silencieux peut apprendre ce silence. [Gestion de l'audio par l'entraîneur](https://fal.ai/models/minimax/h3/ref2va/trainer).

Ce sont des vérifications à effectuer, pas un diagnostic rétrospectif du cas vécu. Arrêtez le lot tant qu'un petit test ne montre pas l'effet recherché.

## Deux alternatives pour le local en France

**Wan 2.2** : vidéo depuis texte ou image, poids sous Apache 2.0, sans exclusion générale de l'UE ; la version TI2V-5B documente une voie à 24 Go avec déchargement en RAM. [Projet et matériel](https://github.com/Wan-Video/Wan2.2), [licence](https://github.com/Wan-Video/Wan2.2/blob/main/LICENSE.txt).

**LTX-2.3** : génération audio et vidéo avec poids locaux, sans exclusion générale de l'UE ; sa licence communautaire impose néanmoins des conditions, notamment une licence payante pour les entités atteignant 10 millions de dollars de revenus annuels. [Modèle](https://huggingface.co/Lightricks/LTX-2.3), [licence](https://huggingface.co/Lightricks/LTX-2.3/blob/main/LICENSE).
