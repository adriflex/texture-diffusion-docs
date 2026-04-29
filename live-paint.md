# Live Paint — retouches rapides

Mode pour corriger une zone précise d'une texture existante sans repasser par tout un workflow de bake.

> 🖼️ **[SÉRIE 3 — (1) une zone du viewport entourée par un carré jaune / (2) l'image générée par l'IA / (3) la même zone repeinte avec le stencil sur l'objet]**

## Le pipeline

> 🖼️ **[FIGURE — capture du panel Generate avec ses 4 zones : Inputs, Prompt tags, Output, bouton Generate]**

1. Tu cadres la zone à retoucher dans le viewport (le carré jaune indique ce qui sera capturé).
2. Tu cliques **Generate AI Texture** — l'IA reçoit cette zone + ton prompt + tes images de référence éventuelles.
3. L'image générée revient et devient automatiquement le **stencil** de ton pinceau.
4. Tu cliques **Start Live Paint** : Blender bascule en Texture Paint avec le stencil en place sur le pinceau IA.
5. Tu peins sur ton modèle, le stencil s'applique pile à l'endroit que tu avais cadré.

## Le carré jaune

> 🖼️ **[FIGURE — vue 3D avec le carré jaune visible sur un objet]**

Il délimite la zone exacte que l'IA va voir. Sa résolution est réglable via **Capture** dans la box Inputs. Tu peux le masquer avec l'icône à droite.

## Le stencil — pourquoi pas un simple "remplacer la texture"

> 🖼️ **[FIGURE — exemple de fondu réussi entre la zone repeinte et le reste de la texture]**

Le stencil te laisse **doser** ce que tu appliques. Tu peux peindre seulement une partie de l'image générée, ajuster l'opacité, ou repasser plusieurs fois pour un fondu progressif. C'est ce qui permet aux retouches IA de se mélanger avec ce qui existe déjà au lieu d'écraser brutalement.

## Color Match — recoller la teinte

> 🖼️ **[FIGURE annotée — sub-panel Color Match avec l'algo et les boutons Apply / Reset]**

L'IA génère parfois avec une teinte décalée par rapport à ton existant (plus saturé, plus chaud, etc.). **Color Match** ajuste la palette de l'image générée pour qu'elle se rapproche de la zone source.

- **Apply** : applique le matching à la dernière génération.
- **Reset** : revient à l'image brute de l'IA.

Quatre algorithmes sont disponibles dans le menu déroulant ; ils donnent chacun un résultat un peu différent, le plus simple est d'essayer.

## Save All Modified Images

> 🖼️ **[FIGURE — bouton Save All Modified Images visible quand on est en Texture Paint]**

Une fois que tu as peint, ton image est modifiée en mémoire mais pas encore sur disque. Le bouton **Save All Modified Images** apparaît automatiquement en mode Texture Paint et flushe toutes les images modifiées en un clic — pratique avant de fermer le fichier ou de relancer une génération.
