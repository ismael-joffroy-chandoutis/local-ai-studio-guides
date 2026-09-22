**Version : v2026-09-23.1 · 23/09/2026 00h39 Paris · sources : web, vérifié · résidence Écritures Liquides**

# Pinokio : produire sur votre tour

<img src="../images/04-pinokio.jpg" alt="" width="100%">

Votre point de départ : allumez votre station de travail. Ici, « local » signifie que le calcul se fait sur cette tour, même si vous la commandez à distance. Le présent guide concerne Pinokio, déjà installé, et non la création d'une nouvelle machine chez Scaleway.

Pinokio est un lanceur : il installe les logiciels nécessaires à une application, la démarre et affiche son interface. Ce n'est pas un modèle de génération. Une application peut faire du calcul local ou appeler un service payant : vérifiez sa fiche avant de l'utiliser. [Présentation officielle](https://raw.githubusercontent.com/pinokiocomputer/docs.pinokio.computer/main/index.md).

## Installer, lancer, arrêter

1. Ouvrez **Discover**, la bibliothèque d'applications. Cherchez le nom exact dans le tableau ci-dessous et vérifiez le dépôt associé, c'est-à-dire la page où son lanceur est maintenu. Deux fiches peuvent porter le même nom.
2. Ouvrez la fiche et choisissez **Install** ou **Download**, selon l'écran. Attendez la fin de l'installation : la première ouverture peut encore télécharger les fichiers du modèle.
3. Revenez à l'application installée et choisissez **Start** ou **Run**. Ouvrez le lien de son interface lorsqu'il apparaît. Le journal qui défile est le compte rendu du démarrage, pas encore l'outil de création.
4. Faites un seul petit essai. Téléchargez le résultat avant de passer à une autre application.
5. Pour arrêter le calcul, utilisez **Stop** dans le lanceur. Fermer seulement l'onglet de l'interface n'est pas une procédure d'arrêt du serveur. Les intitulés du menu dépendent du lanceur choisi. [Manuel Pinokio, scripts et lanceurs](https://desktop.pinokio.co/docs/), [commande d'arrêt documentée](https://github.com/pinokiocomputer/pterm).

**Règle : une seule application lourde à la fois sur les 32 Go de mémoire vidéo de votre RTX 5090.** Cela inclut un entraînement dans AI Toolkit. Cette mémoire, appelée VRAM, sert au calcul de la carte graphique ; elle est distincte de la mémoire générale du PC. Des mesures H3 sur une 5090 atteignent déjà 27 à 31,3 Go avec une seule génération. La règle garde donc une marge pratique, sans promettre que tout modèle tiendra. [Mesures publiées le 3 septembre 2026](https://umarsalim.com/blog/minimax-h3-on-one-rtx-5090/).

## Retrouver les fichiers

Le répertoire des applications est `PINOKIO_HOME/api`. Si votre installation utilise `C:\pinokio`, cela donne `C:\pinokio\api\<app>`, parfois avec `.git` à la fin du nom du dossier. Ouvrez le dossier depuis Pinokio plutôt que de deviner son nom. [Organisation des applications](https://github.com/pinokiocomputer/pterm).

```text
C:\pinokio\api\<app>\
    ENVIRONMENT    réglages propres à cette application
    start.js       exemple de script de lancement
    app\           souvent le logiciel installé, selon le lanceur
```

Le dossier de sortie dépend de l'application : il n'existe pas un unique dossier `output` valable pour toute la bibliothèque. Les caches de téléchargement peuvent également être placés dans le dossier de l'application ou dans un cache partagé. Utilisez le bouton de téléchargement du résultat et gardez une copie de travail dans un dossier à vous avant une réinstallation ou un **Reset**. [Structure d'un projet](https://desktop.pinokio.co/docs/), [définition des caches dans Pinokio](https://raw.githubusercontent.com/pinokiocomputer/pinokiod/main/kernel/environment.js).

## Quelles applications chercher ?

Les noms ci-dessous sont ceux des fiches publiques consultées le 23 septembre 2026. Leur présence dans la bibliothèque est vérifiée ; leur installation sur vos quatre tours n'a pas été testée pour ce guide. Commencez par l'application qui répond à votre essai, puis ajoutez les autres au besoin.

| Nom exact de la fiche | Pour faire quoi ? | Fiche et lanceur à reconnaître |
| --- | --- | --- |
| **Comfyui** | Construire une chaîne de génération d'images ou de vidéos avec des blocs reliés, appelés nœuds. Vous disposez déjà de ComfyUI : retrouvez l'installation existante avant d'en ajouter une seconde. | [pinokiofactory/comfy](https://beta.pinokio.co/apps/github-com-pinokiofactory-comfy) |
| **Wan2GP** | Produire des vidéos avec une interface à formulaires. Le projet annonce notamment Wan 2.1/2.2, Hunyuan Video, LTX Video et des modèles d'image. Le modèle choisi détermine les fonctions et la licence. | [pinokiofactory/wan](https://beta.pinokio.co/apps/github-com-pinokiofactory-wan) ; autre lanceur identifié : [6Morpheus6/wan2gp](https://beta.pinokio.co/apps/github-com-6morpheus6-wan2gp) |
| **FramePack** | Générer une vidéo progressivement, par sections successives. La fiche cible les cartes NVIDIA. | [pinokiofactory/Frame-Pack](https://beta.pinokio.co/apps/github-com-pinokiofactory-frame-pack) |
| **FramePack-Studio** | Travailler avec FramePack en ajoutant une file de tâches, des consignes qui changent dans le temps, des extensions de vidéo et des LoRA. Un LoRA est un fichier d'adaptation d'un modèle. | [FP-Studio/fp-studio](https://beta.pinokio.co/apps/github-com-fp-studio-fp-studio) |
| **LivePortrait** | Animer un portrait. À explorer pour une zone vivante dans une image ou un visage animé. | [pinokiofactory/liveportrait](https://beta.pinokio.co/apps/github-com-pinokiofactory-liveportrait) |

Pour l'image, Comfyui et les fonctions d'image de Wan2GP suffisent comme premiers points d'entrée. N'interprétez pas les statistiques communautaires de la bibliothèque comme une certification de compatibilité : elles recensent des configurations déclarées. Une fiche « installable » n'est pas la preuve d'une génération réussie sur votre PC. [Fiche Wan2GP et configurations déclarées](https://beta.pinokio.co/apps/github-com-6morpheus6-wan2gp).

## Partager une seule application avec un code

Un tunnel relie une application de votre tour à une adresse Internet. Toute personne qui dispose de l'accès peut alors utiliser cette application et mobiliser votre carte graphique. Pinokio prévoit un tunnel Cloudflare et une protection par code ; sans code, son réglage de partage public laisse l'application ouverte à quiconque possède le lien. [Réglages officiels du partage](https://raw.githubusercontent.com/pinokiocomputer/pinokiod/main/kernel/environment.js).

1. Faites d'abord fonctionner l'application sur le bureau de la tour.
2. Arrêtez-la. Dans son menu **Configure**, ouvrez les réglages de son fichier `ENVIRONMENT`. Si vous passez par l'Explorateur, prenez `C:\pinokio\api\<app>\ENVIRONMENT`, et non le fichier général `C:\pinokio\ENVIRONMENT`.
3. Renseignez ces deux valeurs, en remplaçant le texte du code par un code long que vous choisissez :

```dotenv
PINOKIO_SHARE_CLOUDFLARE=true
PINOKIO_SHARE_PASSCODE=REMPLACEZ_PAR_VOTRE_CODE_LONG
```

4. Enregistrez et relancez l'application. Copiez l'adresse de partage Cloudflare affichée pour cette application. Le mécanisme dépend du lien que son lanceur signale à Pinokio ; une application qui ne signale pas ce lien peut ne pas déclencher le tunnel.
5. Testez l'adresse dans une fenêtre privée : vous devez voir la demande de code avant l'application. Testez un mauvais code, puis le bon. Si l'application s'ouvre sans code, ne diffusez pas le lien et coupez le partage.
6. Pour fermer l'accès, repassez `PINOKIO_SHARE_CLOUDFLARE=false`, arrêtez puis relancez l'application, et vérifiez que l'ancien lien ne donne plus accès. [Édition des réglages](https://desktop.pinokio.co/docs/), [déclenchement et transmission du passcode dans le code officiel](https://raw.githubusercontent.com/pinokiocomputer/pinokiod/main/kernel/api/local/index.js).

Si le tunnel n'apparaît pas, conservez le message d'erreur et faites vérifier le lanceur. N'exposez pas à sa place l'interface générale de la machine.

## Les adresses et les ports à ne pas confondre

Le nombre après les deux-points d'une adresse, par exemple `:42000`, est un **port**, une entrée vers un service. Pinokio distingue son interface de commande de l'adresse de l'application. Son routeur attribue aussi des ports de partage : les adresses `420xx` peuvent changer lors d'un redémarrage. Recopiez le lien actuel ; ne remplacez pas un numéro au hasard. [Distinction entre commande et application](https://github.com/pinokiocomputer/pterm), [attribution des ports](https://raw.githubusercontent.com/pinokiocomputer/pinokiod/main/kernel/router/index.js).

**Consigne : ne partagez jamais `:42000`, ni `:42003`, ni un lien qui ouvre un shell.** Le shell est une console capable d'exécuter des commandes sur la machine. `:42000` apparaît comme port de commande dans la documentation. L'association exacte « shell = 42003 » de votre configuration n'a pas pu être confirmée comme règle générale dans les sources publiques : elle reste un repère à bloquer ici, pas une garantie qu'un autre port serait sans risque. [Port de commande](https://github.com/pinokiocomputer/pterm), [capacités d'exécution de Pinokio](https://raw.githubusercontent.com/pinokiocomputer/docs.pinokio.computer/main/index.md).

Le partage local et le tunnel public sont deux mécanismes distincts. Ne supposez pas que le passcode du tunnel protège une adresse directe `http://machine:420xx` : le code du partage local ne lui transmet pas ce passcode. Diffusez uniquement le lien de l'application dont vous venez de vérifier la protection. [Code du partage local et Cloudflare](https://raw.githubusercontent.com/pinokiocomputer/pinokiod/main/kernel/api/local/index.js).

En fin de séance : téléchargez vos résultats, arrêtez l'application, vérifiez la fermeture du partage, puis utilisez la procédure d'arrêt de la tour donnée par la résidence.
