**Version : v2026-09-23.1 · 23/09/2026 00h39 Paris · sources : web, vérifié · résidence Écritures Liquides**

# fal.ai : lancer un calcul en connaissant son prix

<img src="../images/06-fal.jpg" alt="" width="100%">

fal.ai donne accès à des modèles hébergés, depuis un formulaire dans le navigateur ou depuis un programme. Vous n'avez pas à faire tenir leurs poids dans les 32 Go de votre tour. Utilisez-le pour un modèle absent du local, un calcul trop lourd ou une comparaison ponctuelle. [Démarrage officiel](https://fal.ai/docs/documentation/quickstart).

**Règle : annoncez une estimation et un plafond avant de lancer un lot, puis attendez l'accord du mentor.** Le compte fal.ai du mentor et vos clés OpenRouter plafonnées à 25 $ sont deux budgets distincts. Le plafond OpenRouter ne protège pas une dépense sur fal.ai.

## Ouvrir un compte et choisir qui paie

Allez sur [fal.ai](https://fal.ai/), ouvrez **Sign in** et suivez la création de compte. L'inscription ne signifie pas que les générations sont gratuites. Pour votre compte personnel, vérifiez le solde dans **Dashboard > Billing** avant d'acheter du crédit. Pour le compte de la résidence, utilisez l'accès ou l'équipe préparés par le mentor, sans recharger vous-mêmes son compte. fal fonctionne avec des crédits prépayés. [Démarrage](https://fal.ai/docs/documentation/quickstart), [facturation](https://fal.ai/docs/documentation/model-apis/pricing).

Vérifiez le compte ou l'équipe sélectionnés en haut du tableau de bord. Une clé d'API, le secret qui autorise un programme à appeler le service, appartient au compte qui l'a créée. Pour simplement générer, le niveau **API** suffit ; le niveau **ADMIN** donne des droits supplémentaires de déploiement. [Comptes et clés](https://fal.ai/docs/documentation/setting-up/authentication).

## Comprendre les unités

Une vidéo facturée « par seconde » l'est généralement **par seconde de vidéo produite**, pas par seconde passée à attendre. Une image peut être facturée à l'unité ou au **mégapixel**, un million de pixels. Certains autres services facturent le temps de calcul. Chaque page précise son unité ; ne transposez pas le tarif d'un modèle à un autre. Le temps passé dans la file d'attente et les erreurs du serveur ne sont pas facturés selon la documentation. [Unités de facturation](https://fal.ai/docs/documentation/model-apis/pricing).

Un résultat techniquement réussi mais artistiquement raté reste un résultat produit. Prévoyez plusieurs essais dans votre budget. Ne supposez pas non plus que toute erreur est gratuite : la FAQ distingue les erreurs serveur, non facturées, de certaines erreurs d'entrée détectées après du calcul. [FAQ de facturation](https://fal.ai/docs/documentation/model-apis/faq).

## Repères de prix au 23 septembre 2026

Prix publics en dollars américains, hors éventuels frais et taxes, à relire avant chaque lot. Les noms complets évitent de confondre versions rapides, standard et professionnelles. Les montants de la dernière colonne sont calculés à partir du tarif consulté, sans génération payante de contrôle.

| Modèle et page tarifaire | Réglage et unité | Coût d'un essai |
| --- | --- | --- |
| [Kling 3.0 Pro, image vers vidéo](https://fal.ai/models/fal-ai/kling-video/v3/pro/image-to-video) | 0,112 $/s sans son ; 0,168 $/s avec son ; 0,196 $/s avec contrôle de voix | 5 s : **0,56 / 0,84 / 0,98 $** |
| [Wan 2.2 A14B, texte vers vidéo](https://fal.ai/models/fal-ai/wan/v2.2-a14b/text-to-video) | 480p : 0,04 $/s ; 580p : 0,06 $/s ; 720p : 0,08 $/s. Facturation calculée sur **16 images/s** | 81 images : environ **0,20 / 0,30 / 0,41 $** |
| [Veo 3.1 standard](https://fal.ai/models/fal-ai/veo3.1) | 720p ou 1080p : 0,20 $/s sans son ; 0,40 $/s avec son | 8 s : **1,60 / 3,20 $** |
| [MiniMax H3, texte vers vidéo](https://fal.ai/models/minimax/h3/text-to-video) | 480p : 0,05 $/s ; 768p : 0,06 $/s ; 2K : 0,13 $/s ; 4K : 0,16 $/s | 5 s : **0,25 / 0,30 / 0,65 / 0,80 $** |
| [FLUX.1 [dev], image](https://fal.ai/models/fal-ai/flux/dev) | 0,025 $/mégapixel, arrondi au mégapixel supérieur | 768 × 1024 : **0,025 $** ; 1024 × 1024 : **0,05 $** selon cet arrondi |

Pour Wan, les 81 images représentent `81 ÷ 16 = 5,0625` secondes facturables : modifier la cadence de lecture ne constitue pas une réduction du nombre d'images calculées. Pour FLUX, `1024 × 1024 = 1 048 576` pixels dépasse un million. Vérifiez le prix affiché par la page avant de valider, notamment si votre compte bénéficie d'un tarif particulier. [Wan](https://fal.ai/models/fal-ai/wan/v2.2-a14b/text-to-video), [FLUX](https://fal.ai/models/fal-ai/flux/dev).

Le tarif H3 relevé sur sa page active est inférieur à celui de certains articles de lancement. Utilisez le prix de la page du modèle et de ses réglages actuels. La présence d'une option 4K chez fal ne prouve pas que le modèle ouvert local offre la même chaîne de traitement. [Page H3](https://fal.ai/models/minimax/h3/text-to-video), [article antérieur de fal](https://fal.ai/learn/tools/minimax-h3-explained).

## Estimer un lot avant de cliquer

Votre calcul de base est : **nombre d'essais × quantité facturée par essai × tarif unitaire**. Comptez tous les essais, y compris ceux que vous ne garderez pas.

Exemple : 10 clips H3 texte vers vidéo de 5 secondes en 2K représentent `10 × 5 × 0,13 = 6,50 $`. Avec deux essais supplémentaires prévus, le total estimé devient **7,80 $**. C'est une estimation arithmétique au tarif ci-dessus, pas un devis réservé.

Vous pouvez annoncer :

> Je prévois 10 clips H3 de 5 secondes en 2K sur fal.ai : 6,50 $ estimés. Avec deux reprises au maximum, plafond du lot à 7,80 $. Je commence par un clip et j'attends ton accord avant de lancer.

Si vous changez de modèle, de résolution, de durée ou de nombre d'essais, recalculez. Le prix doit couvrir également les entraînements, les agrandissements et les autres étapes que vous ajoutez.

## Faire le premier essai dans le Playground

1. Ouvrez la page exacte du modèle dans le tableau.
2. Dans **Playground**, remplissez la consigne et les champs obligatoires. Pour une image ou une vidéo d'entrée, utilisez le bouton d'import.
3. Dépliez les réglages supplémentaires : vérifiez durée, résolution, son et nombre de sorties. Notez-les avec le prix.
4. Après accord, cliquez une seule fois sur **Run** et attendez le résultat. Évitez de relancer simplement parce que l'affichage tarde.
5. Téléchargez la sortie, regardez-la en entier et notez ce qu'il faut changer. Modifiez un paramètre à la fois pour comprendre son effet.

Le Playground fournit aussi une vue **JSON**, un texte structuré contenant les paramètres, et du code correspondant aux entrées du formulaire. [Mode d'emploi officiel](https://fal.ai/docs/documentation/model-apis/playground).

## Passer à l'API, quand le premier essai fonctionne

L'API permet à un programme de soumettre les mêmes paramètres sans remplir le formulaire à chaque fois. Dans **Dashboard > Keys**, créez une clé de niveau **API** uniquement si le mentor vous a autorisé cet accès. Une clé fal ne se colle jamais dans une page HTML publique, un dépôt GitHub ou Discord. Gardez-la dans les réglages locaux du programme. [Authentification](https://fal.ai/docs/documentation/setting-up/authentication), [protection des clés côté navigateur](https://fal.ai/docs/documentation/model-apis/faq).

Voici un exemple pour **une seule image FLUX.1 [dev] en 768 × 1024**, estimée à **0,025 $** au tarif relevé. Il ne lance aucun lot. Dans PowerShell, depuis un nouveau dossier de travail, préparez Python et la clé autorisée. Python doit déjà être installé et la commande `py` disponible. [Environnement Python](https://docs.python.org/3/library/venv.html), [saisie PowerShell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/read-host?view=powershell-7.5).

La saisie ci-dessous reste visible dans la console : évitez de partager cet écran pendant la saisie de la clé.


```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install fal-client
# Saisissez la clé dans cette fenêtre, sans l'inscrire dans le script.
$env:FAL_KEY = Read-Host "Clé fal autorisée"
```

Le client Python officiel lit `FAL_KEY`. Créez un fichier `essai-fal.py` avec le code suivant. L'exemple utilise la file d'attente persistante afin de conserver un identifiant dès la soumission. [Client Python](https://fal-ai.github.io/fal/client/fal_client.html), [paramètres FLUX](https://fal.ai/models/fal-ai/flux/dev/api), [file d'attente](https://fal.ai/docs/documentation/model-apis/inference/queue).

```python
import json
from datetime import datetime, timezone
from pathlib import Path
from urllib.request import urlretrieve
import fal_client

modele = "fal-ai/flux/dev"
parametres = {
    "prompt": "Une chaise rouge dans une pièce vide, lumière du matin",
    "image_size": {"width": 768, "height": 1024},
    "num_images": 1,
    "seed": 104,
    "output_format": "png",
}

# Un dossier neuf par essai, sans écraser les précédents.
dossier = Path(datetime.now(timezone.utc).strftime("essai-%Y%m%d-%H%M%S-%f"))
dossier.mkdir()
def garder(nom, contenu):
    (dossier / nom).write_text(
        json.dumps(contenu, ensure_ascii=False, indent=2), encoding="utf-8"
    )

garder("entree.json", {"modele": modele, "parametres": parametres})
if input("Coût estimé : 0,025 $. Accord obtenu ? Tapez LANCER : ") != "LANCER":
    raise SystemExit("Aucune demande envoyée.")

# L'appel payant commence ici.
demande = fal_client.submit(modele, arguments=parametres)
garder("demande.json", {"request_id": demande.request_id})
print("Demande enregistrée :", demande.request_id, flush=True)
resultat = demande.get()
garder("sortie.json", resultat)
urlretrieve(resultat["images"][0]["url"], dossier / "image.png")
print("Résultat téléchargé dans", dossier.resolve())
```

Après validation de la dépense, lancez ` .\.venv\Scripts\python.exe essai-fal.py `. Si la connexion se coupe après la soumission, consultez l'identifiant dans `demande.json` et l'historique fal **avant de relancer le script** : une nouvelle exécution soumettrait une nouvelle demande. Le programme est fourni comme exemple ; aucun appel payant n'a été exécuté pour ce guide. [Fonctionnement de la file persistante](https://fal.ai/docs/documentation/model-apis/inference/queue).

## Garder les résultats et plafonner la dépense

Conservez ensemble les entrées, les réglages, l'identifiant de demande, la sortie téléchargée et le coût réellement relevé. Les données JSON de l'historique sont conservées **30 jours par défaut**. Les médias ont une durée de conservation distincte, configurable ; la FAQ annonce **au moins 7 jours par défaut**. Une URL fal n'est pas une archive : téléchargez vos images et vidéos dès la séance. [Historique et conservation](https://fal.ai/docs/documentation/model-apis/media-expiration), [durée par défaut des médias](https://fal.ai/docs/documentation/model-apis/faq).

Pour tenir le budget de la résidence, fixez un nombre maximal de demandes et lancez-les une par une au début. Réservez dans votre suivi le coût des demandes déjà envoyées, même si elles ne sont pas terminées. Avant chaque nouvelle demande, vérifiez que « dépensé + réservé + prochain essai » reste sous le plafond convenu. C'est votre contrôle de séance, pas une fonction automatique promise par fal.

Dans **Billing**, contrôlez le solde et les dépenses. Si votre compte propose une recharge automatique, laissez-la désactivée pour cette séance. **Un plafond individuel de dépense par clé fal, équivalent à celui de vos clés OpenRouter, n'a pas été confirmé dans les pages publiques consultées.** Ne le supposez pas actif. La FAQ décrit un blocage selon un seuil de solde du compte, et non une garantie de coupure exacte au centime pour chaque résident. [Suivi de facturation](https://fal.ai/docs/documentation/model-apis/pricing), [seuil de blocage](https://fal.ai/docs/documentation/model-apis/faq).

À la fin, notez le total réel avec le mentor et arrêtez les nouveaux appels. Une enveloppe de crédit partagée ne remplace pas le plafond de votre lot.
