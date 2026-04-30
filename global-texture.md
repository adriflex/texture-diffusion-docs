# Global Texture — texturer un modèle de A à Z

Mode pour générer une texture complète sur tout un objet en partant d'un mesh nu. Le plugin photographie l'objet sous plusieurs angles, demande à l'IA de générer chaque vue, puis combine et bake le tout en une seule texture finale.

> 🖼️ **[SÉRIE 5 — (1) mesh nu / (2) mesh avec les vues caméra autour / (3) image IA d'une vue / (4) assembly des projections / (5) texture finale bakée sur l'objet]**

## Le pipeline en 5 étapes

> 🖼️ **[FIGURE — capture du panel Global Texture montrant les 5 étapes alignées]**

| Étape | Ce qui se passe |
|---|---|
| **1. Setup** | Le plugin crée une scène de projection avec ton objet dupliqué sous N angles différents. |
| **2. Bake Masks & UVs** | Calcul des masques de fondu pour chaque vue + génération des UVs projetées depuis chaque caméra. |
| **3. Generate** | Capture caméra + envoi à l'IA pour chaque angle. |
| **4. Assemble Projections** | Création d'une scène de shading qui combine toutes les vues en utilisant les masques. |
| **5. Bake Final** | Bake d'une texture unique sur les UVs originales de ton objet. |

> ⚠️ **Pré-requis** : ton objet doit être unwrappé (avec une UV map valide) et tes transforms appliqués (`Object → Apply → All Transforms`).

## Étape 1 — Setup

> 🖼️ **[FIGURE — slider "Views" avec un nombre de vues, et le bouton Setup Projection]**

Tu choisis le nombre de vues (3 à 9) et tu cliques **Setup Projection**. Le plugin crée une nouvelle scène avec :
- ton objet dupliqué N fois, chaque copie tournée pour montrer une face spécifique (front, back, sides, etc.)
- une caméra cadrant l'ensemble.

> 🖼️ **[FIGURE — la scène de projection avec 6 instances de l'objet disposées en grille]**

> 💡 Plus de vues = meilleure couverture mais plus de coût IA et de masques à gérer. **6 vues** est un bon point de départ. Le maximum est de 7 vues sans symétrie ou 3 avec (Blender plafonne à 8 UV layers par mesh).

## Étape 2 — Bake Masks & UVs

> 🖼️ **[FIGURE — bouton Bake Masks with checkbox Symmetry X]**

Cette étape calcule deux choses pour chaque vue :

**Les UVs projetées** — chaque vue génère une nouvelle UV map qui correspond exactement à ce que la caméra voit. C'est cette UV qui sera utilisée pour appliquer l'image IA.

**Les masques de fondu** — une carte qui indique, pour chaque pixel de l'objet, quelle vue doit dominer. Sans ça, les vues se superposent sans logique et tu vois des coutures partout.

### Deux types de masques

> 🖼️ **[SÉRIE 2 — (1) facing mask : gradient blanc au centre noir sur les bords / (2) occlusion mask : binaire avec ombres dans les creux]**

- **Facing** : mesure à quel point la surface est de face par rapport à la caméra. Plus la surface est de face, plus la vue contribue. Donne un fondu doux entre les vues.
- **Occlusion** : tient compte de l'auto-ombrage. Si une partie de l'objet est cachée par une autre depuis la caméra, le masque est noir à cet endroit. Indispensable sur les objets concaves ou complexes.

> 💡 Le type est réglé dans les **préférences de l'addon** (par défaut : Occlusion). Active **Toggle Mask Preview** pour visualiser le masque sur l'objet avant de continuer.

### Résolution des masques

> 🖼️ **[FIGURE — préférence "Mask bake resolution" dans les Add-on Preferences avec ses options 256 / 512 / 1024 / 2048]**

La résolution des masques se règle aussi dans les **préférences de l'addon**, séparément de la résolution de la texture finale. Le défaut **512 px** convient à la majorité des cas et garde le bake rapide.

> ⚠️ **Sur les objets lourds (typiquement les modèles générés par IA, ou tout mesh dense en polygones), pense à monter à 1024 ou 2048.** Sinon, des petits points blancs (artefacts dus au sampling trop grossier des masques) apparaissent sur le rendu final. C'est l'un des pièges les plus communs sur les meshes denses.

### Symétrie X

> 🖼️ **[FIGURE — comparaison objet symétrique avec et sans Mirror activé]**

Si ton objet est symétrique sur l'axe X (un personnage de face, par exemple), active **Symmetry X**. Le plugin miroitera chaque vue, ce qui permet de couvrir les deux côtés avec moitié moins de générations IA.

## Étape 3 — Generate

> 🖼️ **[FIGURE — bouton Capture & Generate, image picker, et image générée affichée]**

Une fois en scène de projection, tu utilises le panel **Generate** classique pour lancer une génération sur la vue caméra (qui voit toutes tes copies en un seul rendu).

L'image générée arrive dans Blender. Si tu n'es pas satisfait, tu relances ; toutes les images générées restent disponibles dans **Image to project** et tu peux choisir laquelle utiliser pour la suite.

> 🖼️ **[FIGURE — sub-panel Color Match dans Global Texture]**

Comme en Live Paint, **Color Match** te permet de réajuster la teinte de l'image avant projection.

## Étape 4 — Assemble Projections

> 🖼️ **[FIGURE — bouton Assemble Projections avec checkbox "Use existing texture under projection"]**

Le plugin crée une **scène de shading** contenant trois collections :
- **Final Assembly** — l'objet final avec toutes les projections combinées (c'est ce qui sera baké).
- **Breakdown** — chaque vue isolément, pour ajuster ses paramètres individuellement.
- **Tweak** — copie de la scène de projection, utilisée pour ajuster manuellement les UVs si besoin.

> 🖼️ **[FIGURE — outliner avec les 3 collections développées]**

> 💡 La case **Use existing texture under projection** ajoute la texture actuelle de l'objet comme fond, sous les projections IA. Utile pour préserver une base existante.

## Étape 5 — Bake Final

> 🖼️ **[FIGURE — slider Resolution + bouton Bake Final]**

Tu choisis la résolution finale et tu cliques **Bake Final**. Le plugin bake le résultat de l'assembly sur les UVs originales de ton objet et te donne une nouvelle collection avec ton objet final + son matériau prêt à exporter.

---

## Ajustements après assembly

> 🖼️ **[FIGURE — panel Breakdown avec les sliders Facing Position / Size / Intensity / Custom mask intensity et le toggle Mirror]**

Quand tu sélectionnes une vue dans la collection **Breakdown**, le panel expose des réglages par vue :

- **Facing Position / Size / Intensity** — pousse le masque dans une direction, change sa taille, son intensité. Pratique pour donner plus de poids à une vue précise.
- **Custom mask intensity** — pondère le masque manuel.
- **Mirror on/off** — désactive le miroir sur cette vue spécifique si elle ne doit pas être symétrique.

### Custom Mask — peindre des zones manuellement

> 🖼️ **[GIF — bouton Paint custom mask : passage en Texture Paint avec un masque vide à peindre]**

Quand le masque automatique ne suffit pas (typiquement : faire dominer une vue précise sur une zone), le bouton **Paint custom mask** te bascule en mode peinture sur un masque vide associé à la vue. Tu peins en blanc les zones où tu veux que cette vue domine.

### Tweak — déformer pour aligner

> 🎞️ **[GIF — bouton Edit Tweak : déformation des UVs projetées pour recaler l'image sur le mesh]**

Si l'image générée par l'IA ne s'aligne pas parfaitement sur ton mesh (ce qui arrive quand l'objet a une silhouette atypique), le mode **Tweak** te permet de déformer la projection — pas le mesh — pour recaler manuellement. Bouton **Transfer Tweak** pour valider l'ajustement.
