# Gateway · Ads témoignages : charte de montage commune

> **Statut** : la charte commune aux 6 pubs est prête et le master peut être monté dès maintenant.
> Les plans A1 à A6 (extraits, timecodes, textes) seront remplis dès réception des transcriptions.
> **Mot d'ordre** : minimaliste, simple, clean, dynamique.

---

## 1. Specs de sortie (identiques pour les 6)

| | |
|---|---|
| Format | 9:16 · 1080 × 1920 |
| Cadence | celle des rushs (25 ou 30 i/s), sans conversion |
| Durée cible | 20 à 35 s (45 s max) |
| Vidéo | H.264, VBR 1 passe, 15 Mbit/s cible / 20 max |
| Audio | AAC 48 kHz, 320 kbit/s · **−14 LUFS intégré, crête vraie −1 dBTP** (Export › Effets › Normalisation du volume) |
| Nommage | `GW_TEMO_A1_<angle>_v1.mp4` … `GW_TEMO_A6_<angle>_v1.mp4` |

**Pour que le test mesure bien l'angle**, garde tout le reste constant sur les 6 pubs : même habillage, même musique (ou 2 maximum), même écran de fin et des durées proches (±5 s). Seuls l'accroche et les extraits changent.

## 2. Zone sûre (Reels / Stories + recadrage 4:5 du fil)

- Texte et visages importants entre **y = 300 et y = 1240 px**, et à au moins 70 px des bords.
  - En haut, 14 % de l'écran est masqué par l'interface des Reels.
  - En bas, 35 % est masqué par la légende, les boutons et le CTA.
  - Dans le fil, Meta recadre la vidéo en 4:5 (≈ 285 px coupés en haut et en bas).
- **Sous-titres** : bas de la zone utile, centre vers y ≈ 1150 px.
- **Cartons** (accroche, phrases fortes) : haut de la zone utile, centre vers y ≈ 420 px, sans masquer les yeux.

## 3. Habillage minimaliste

- **Une seule police** : Montserrat Bold/ExtraBold (gratuite sur Google Fonts et Adobe Fonts), ou la police de la marque.
- **Trois couleurs** : blanc, noir et une couleur d'accent (celle de la marque, sinon jaune `#FFD60A`).
- **Sous-titres, présents tout le long** (la plupart des gens regardent sans le son) :
  - blanc, 64 à 72 px, ombre portée douce (noir à 60 %, flou de 8 à 10 px), sans contour épais ;
  - 2 lignes max et 3 à 5 mots par bloc ;
  - **un seul mot-clé** par phrase en couleur d'accent.
- **Fidélité** : tu peux retirer les « euh », les répétitions et les faux départs, mais **jamais reformuler ni ajouter**.
- **Cartons d'emphase** :
  - texte noir sur cartouche blanc aux coins arrondis (rayon ≈ 16 px), 7 mots max ;
  - 1,5 à 2,5 s à l'écran, **3 ou 4 cartons max par pub** ;
  - quand un carton reprend la phrase dite, masque le sous-titre pendant ce temps pour ne pas doubler le texte.
- **Animation** : une apparition « pop » (échelle de 90 à 100 % et opacité de 0 à 100 %, 4 images), puis disparition en coupe sèche. Pas d'effet machine à écrire, pas de rebond.
- **Bandeau nom** (prénom + contexte) : petit et discret, 2 s, uniquement avec des infos vérifiées que la personne a validées.

## 4. Rythme et image

- **Couper tous les blancs**, respirations et hésitations (jump cuts), sans jamais couper au milieu d'un mot.
- **Alterner le cadrage à chaque coupe** : 100 % puis 115 à 120 % (punch-in). Ça cache les jump cuts et ça donne du rythme ; sur des rushs 4K, on peut zoomer sans perte.
- **Jamais plus de 3 s sans changement** : une coupe, un zoom, un carton ou un insert.
- **Sur la phrase clé**, faire un léger push-in (de 100 à 106 % sur la durée de la phrase).
- **Étalonnage** léger et homogène entre les témoignages (balance des blancs, expo, un peu de contraste, peau naturelle). Pas de LUT créative.
- **Inserts visuels** : 2 ou 3 max par pub, uniquement s'ils illustrent ce qui est dit (capture, produit, logo). Pas d'éléments génériques ni de faux visuels.

## 5. Transitions (une seule famille pour les 6 pubs)

| Où | Quoi |
|---|---|
| Entre deux coupes d'un même témoignage | coupe sèche + punch-in (pas de transition) |
| Entre deux témoignages ou deux parties | zoom croisé (*Cross Zoom*) de 6 à 8 images **ou** fondu au blanc de 3 ou 4 images, calé sur un temps fort de la musique, avec un whoosh discret |
| Vers l'écran de fin | fondu de 6 images vers un fond uni |

## 6. Musique et mix (les voix d'abord)

- **Musique** : instrumentale (**sans paroles**, sinon elle se bat avec les voix), entraînante et positive, 110 à 128 BPM, énergie montante (pop ou électro légère).
- **Licence publicitaire obligatoire** : Bibliothèque sonore de Meta (gratuite pour les pubs Meta), Artlist, Epidemic Sound (licence commerciale), ou la Commercial Music Library de TikTok. Pas de son tendance sous droits.
- **Voix** :
  - Son essentiel › Dialogue › *Améliorer la voix* (Enhance Speech) entre 40 et 70 % s'il y a du bruit ou de l'écho ;
  - passe-haut à 80 Hz ;
  - niveau homogène d'un témoignage à l'autre.
- **Musique sous la voix** (Son essentiel › Musique › Atténuation / Ducking) :
  - réglages : contre le dialogue, sensibilité 6, réduction de −15 à −18 dB, fondus de 500 ms ;
  - la musique remonte sur les 0,5 premières secondes et sur l'écran de fin.
- **SFX** : un whoosh sur les transitions (vers −20 dB) et un petit « pop » à l'apparition des cartons (vers −24 dB). Pas de SFX sur les sous-titres.

## 7. Écran de fin (identique sur les 6)

- 2 à 3 s, fond uni (blanc ou couleur de la marque), texte noir, et la musique remonte.
- Contenu : logo Gateway, **[offre]** et **[CTA]**, les deux restant à confirmer.

## 8. Garde-fous (véracité et validation Meta)

- **Textes à l'écran** : seulement des **citations exactes** ou des résumés fidèles. Aucun chiffre, résultat ou promesse ajouté.
- **Chiffres et résultats** : affichés tels qu'ils sont dits, **au moment où la personne les dit**. S'ils sortent de l'ordinaire, ajouter en petit « Résultats individuels, non garantis ».
- **Pas d'interpellation sur un attribut personnel** (« Tu es endetté ? », « Tu galères avec ton poids ? ») : Meta refuse ce type de pub. La citation à la 1re personne passe (« J'étais endettée… »).
- **Pas de faux éléments d'interface** (faux boutons, fausses notifications) ni d'avant/après trompeur.
- **Autorisation écrite** de chaque personne (droit à l'image) pour une utilisation publicitaire payante.

## 9. Méthode express dans Premiere (6 pubs en une journée)

1. **Monter la séquence master** en 1080 × 1920. Elle contient :
   - le calque d'effets d'étalonnage ;
   - le style de piste des sous-titres `GW_Sous-titres` ;
   - le carton `GW_Carton` (Objets graphiques essentiels) ;
   - l'écran de fin ;
   - la piste musique avec l'atténuation déjà réglée.

   Ensuite, **la dupliquer 6 fois** (A1 à A6).
2. **Transcrire les rushs** (Texte › Transcription), puis **monter par le texte** : on sélectionne les phrases du plan dans la transcription et on les insère.
3. **Sous-titres** : Texte › Sous-titres › *Créer des sous-titres* depuis la transcription de la séquence. Appliquer le style, puis relire.
4. Ajouter les punch-ins, cartons, inserts et la musique, puis faire le mix.
5. **Exporter en lot** depuis Media Encoder, avec le même préréglage pour les 6.

## 10. Check-list avant envoi

- [ ] L'accroche est lisible dès la 1re seconde et l'image d'ouverture est forte (elle sert de vignette).
- [ ] Pub regardée sur un téléphone, **sans le son puis avec le son**.
- [ ] Textes dans la zone sûre, orthographe vérifiée.
- [ ] Aucun propos ni chiffre ajouté ou déformé.
- [ ] Voix toujours intelligible sous la musique, sans saturation (crête ≤ −1 dBTP).
- [ ] Licence musicale OK.
- [ ] Nommage et export conformes.

---

## 11. Les 6 angles proposés (à confirmer avec les témoignages et le contenu du dossier Ads)

Chaque pub teste une famille d'accroche différente. L'accroche est toujours une **phrase réellement prononcée** : si un angle ne trouve pas de citation qui le porte, je le remplace.

| Pub | Angle | Accroche (type) | Structure |
|---|---|---|---|
| A1 | Résultat | la phrase de résultat la plus forte, telle quelle | résultat → avant → déclic → recommandation → CTA |
| A2 | Sceptique → convaincu | « J'étais sceptique… » (si quelqu'un le dit) | doute → essai → surprise → recommandation → CTA |
| A3 | Avant / après | la situation de départ (la douleur) | avant → bascule → après → CTA |
| A4 | Compilation | 3 à 5 voix, une phrase forte chacune | rafale de phrases fortes → CTA |
| A5 | Objection | la réponse vécue à l'objection n°1 (prix, temps, confiance) | objection → réponse → résultat → CTA |
| A6 | Recommandation | « Si tu hésites… », un conseil direct | conseil → pourquoi → CTA |

## 12. Gabarit de chaque plan (A1 à A6)

1. **Extraits** : fichier, TC d'entrée et de sortie, citation exacte.
2. **Accroche (0 à 2 s)** : image d'ouverture, carton et départ audio.
3. **Ordre des séquences** : tableau avec les TC de la timeline.
4. **Textes à l'écran** : texte exact, moment d'apparition et style (sous-titre ou carton).
5. **Visuels, transitions et musique** : inserts, points de transition et cue musical.
