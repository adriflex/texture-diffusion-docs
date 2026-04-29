# Modèles & tips

Le plugin parle à plusieurs IA via trois fournisseurs (Replicate, fal.ai, Gemini). Chaque modèle a ses forces — vitesse, coût, type de rendu, capacité à recevoir des images de référence.

## Comparatif rapide

> 🖼️ **[FIGURE — galerie : un même prompt rendu par 4-5 modèles différents côte-à-côte avec le nom de chaque modèle]**

| Modèle | ⚡ Vitesse | 💲 Coût | Force | Bon pour |
|---|---|---|---|---|
| **Nano Banana** | ~10 s | $ | Polyvalent, rapide | Itérations, tests rapides |
| **Nano Banana 2** | ~15 s | $$ | Meilleure qualité que Nano 1 | Le default conseillé |
| **Nano Banana Pro** 💎 | ~30 s | $$$ | Top qualité, suit bien le prompt | Rendu final, propre |
| **FLUX 2 Pro Edit** | ~25 s | $$$ | Photoréalisme, détails fins | Textures réalistes |
| **Seedream v5 Lite** | ~10 s | $ | Style stylisé, anime/cartoon | Rendus non-photo |
| **Grok Imagine Edit** | ~15 s | $$ | Variété de styles | Exploration |
| **GPT-Image-2 (Low/Med/High)** | 15-30 s | $-$$$ | Cohérence avec le prompt | Quand le prompt est précis |

> 💡 Les badges dans le menu déroulant te résument ça d'un coup d'œil : ⚡ rapide · 💎 top qualité · 💲 / 💲💲 cher.

## Trois fournisseurs, mêmes modèles

> 🖼️ **[FIGURE — dropdown Provider avec les 3 options : Replicate, fal.ai, Gemini]**

Plusieurs modèles (Nano Banana family, GPT-Image-2, FLUX 2 Pro) sont disponibles chez plusieurs fournisseurs. Le rendu est identique mais :

- **Replicate** — facturation à l'image, dashboard des credits clair, large catalogue.
- **fal.ai** — souvent un peu moins cher, certains modèles facturés à la seconde de calcul.
- **Gemini** — accès direct aux modèles Google (Nano Banana family), facturation Google Cloud.

> 💡 Tu peux mettre une clé sur les trois fournisseurs et switcher selon le besoin. Le panel **🔑 API Keys** centralise tout.

## Suivre tes dépenses

> 🖼️ **[FIGURE — panel 💰 Cost avec le coût total et le bouton Reset]**

Le panel **💰 Cost** suit le coût cumulé de la scène en cours. Bouton **Reset** pour repartir à zéro.

Sur Replicate, un avertissement apparaît automatiquement quand tes credits restants passent sous **$5**, pour éviter de te retrouver à sec en pleine génération.

---

## Tips bonus

### Les prompt tags vs un prompt long

> 🖼️ **[FIGURE — box "Prompt tags" avec plusieurs tags ajoutés et toggleables]**

Le plugin n'utilise pas un champ texte libre mais un système de **tags**. Chaque tag est :
- réutilisable (ajout en un clic depuis la liste)
- toggleable (case à cocher pour activer/désactiver sans le supprimer)
- réordonnable
- persistant dans le `.blend` (tes tags habituels sont là à chaque ouverture)

Concrètement : compose ton prompt en empilant des petits éléments ("metallic surface", "scratched paint", "rust details") plutôt qu'une longue phrase. C'est plus rapide à itérer.

### Reference images

> 🖼️ **[FIGURE — box "Inputs" avec une image de référence ajoutée et la checkbox Use]**

Certains modèles acceptent jusqu'à plusieurs **images de référence** en plus du viewport. Utile pour :
- imposer un style (référence d'un autre asset que tu veux matcher)
- guider la palette
- montrer un détail spécifique

Tous les modèles ne supportent pas les refs — le slot est masqué automatiquement quand le modèle ne les gère pas.

### Capture resolution

> 🖼️ **[FIGURE — slider Capture dans la box Inputs]**

C'est la résolution **envoyée à l'IA**, pas la résolution de retour. Plus elle est grande, plus l'IA voit de détails de ton viewport, mais plus c'est lourd à transférer. **768** est un bon défaut.

### Output resolution

C'est la résolution de **l'image qui revient**. Pour les modèles qui le supportent (Nano family, FLUX 2 Pro), le menu **Output** te laisse choisir entre 0.5K, 1K, 2K, voire 4K. **Le coût varie** selon la résolution choisie — le prix affiché s'adapte automatiquement.

### Dernière génération à portée de clic

> 🖼️ **[FIGURE — miniature "Open in Image Editor" sous le bouton Generate]**

Sous le bouton **Generate**, une miniature de la dernière image générée reste affichée. Clic sur **Open in Image Editor** pour l'ouvrir directement et l'inspecter.
