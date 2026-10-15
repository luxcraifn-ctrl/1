# Ads témoignages Gateway : mission complète (session locale)

## Mission
Tu es monteur vidéo senior et créatif « performance », spécialisé dans les publicités Meta et TikTok. Tu travailles **en local sur mon PC Windows**, en autonomie.

**Objectif** : préparer 6 publicités vidéo pour un **lancement demain**. Elles sont construites **uniquement à partir de témoignages clients** de Gateway, pour tester un angle publicitaire « témoignages ».

Je monte ensuite dans Premiere Pro. Tes livrables doivent donc être **directement exploitables** : timecodes exacts, textes exacts, fichiers importables.

Mot d'ordre : **minimaliste, simple, clean, dynamique**, avec des montages rapides à réaliser. C'est urgent : vise d'abord un premier jeu complet des 6 plans, puis affine.

## Dossiers
- **Témoignages (sources)** : `C:\Users\luxcr\Downloads\Temoignage`
- **Pubs à monter (6)** : `C:\Users\luxcr\Documents\Montage\Client\Gateway\Ads`
- **Dossier client** (charte, logo, musiques, SFX, anciennes pubs éventuelles) : `C:\Users\luxcr\Documents\Montage\Client\Gateway`
- **Sortie** : crée `C:\Users\luxcr\Documents\Montage\Client\Gateway\Ads\_PLANS`. Les fichiers de travail vont dans `_PLANS\_travail`.

## Règles non négociables
1. **Sources en lecture seule.** Ne modifie, ne déplace, ne renomme et ne supprime aucun fichier existant. Tu écris uniquement dans `_PLANS`. Si une source est dans un .zip, extrais-la dans `_PLANS\_travail\sources` et laisse l'original intact.
2. **Tout reste en local.** N'envoie aucun fichier client vers un service en ligne ; la transcription se fait sur la machine.
3. **Fidélité absolue.** Uniquement des propos réellement prononcés. Aucune citation inventée, reformulée ou « améliorée », aucun chiffre ni résultat ajouté.
   - Nettoyage autorisé : « euh », répétitions, faux départs.
   - Une coupe ne doit jamais changer le sens. Attention aux négations, aux « mais », aux conditionnels et à l'ironie.
4. **Traçabilité.** Chaque extrait = un fichier + des timecodes d'entrée et de sortie vérifiés sur la transcription mot à mot.
5. **Rien d'inventé pour combler un manque.** Écris `[À CONFIRMER]` et ajoute la question à ta liste.
6. **Rien de fabriqué.** Aucune voix, aucun visage ni aucun avis générés pour simuler un témoignage. Pas de faux visuels : fausses notes, faux chiffres, fausse interface.
7. **Langue et encodage.** Rédige en français, fichiers texte en UTF-8.

## Déroulé
Enchaîne les étapes sans me demander de valider chacune, et donne-moi une ligne d'avancement entre deux étapes.

Si le temps manque, priorité dans cet ordre : plans `.md`, puis sous-titres `.srt`, puis radio-edits `.mp3`, puis bonus.

### Étape 1 : inventaire (lecture seule)
- **Outils.** Vérifie `ffmpeg`/`ffprobe`, Python 3 et la présence d'un GPU NVIDIA (`nvidia-smi`). Installe ce qui manque (ffmpeg : `winget install Gyan.FFmpeg` ; transcription : `pip install faster-whisper`) et dis-moi ce que tu as installé.
- **Médias.** Parcours récursivement les deux dossiers et le dossier client. Pour chaque média, relève avec ffprobe : nom, durée, résolution, orientation (9:16, 16:9 ou 1:1), cadence, codec, présence d'audio, taille. Si un rush est en cadence variable (fréquent sur iPhone), signale-le.
- **Formes de témoignage.** Ils peuvent être des vidéos, des audios ou des captures écrites (avis, messages). Traite chaque type.
  - Une capture écrite peut servir d'insert ou de carton, en citant exactement son texte.
  - Masque les données personnelles si besoin, sans jamais retoucher le contenu.
- **Documents et ressources.** Lis tous les documents (briefs, scripts, notes en .txt, .docx ou .pdf). Repère les logos, polices, couleurs, musiques et SFX.
  - Projets Premiere (`.prproj`) : note-les, sans les ouvrir.
  - Transcriptions existantes (`.srt`, `.txt`) : réutilise-les.
- **Rôle du dossier Ads.** Déduis ce qu'il contient : 6 sous-dossiers de rushs (une pub chacun), des briefs, des B-rolls, ou un dossier de destination vide ? Note quel témoignage va dans quelle pub si c'est déjà prévu. Si c'est ambigu, pars sur l'hypothèse la plus probable, écris-la noir sur blanc et ajoute la question à l'étape 4.
- **Livrable** : `_PLANS\00_inventaire.md`.

### Étape 2 : transcription horodatée (locale)
- **Audio.** Pour chaque témoignage, et chaque rush parlé du dossier Ads, extrais l'audio en WAV mono 16 kHz dans `_travail`.
- **Transcription avec faster-whisper.**
  - Options : `language="fr"`, `word_timestamps=True`, `vad_filter=True`, `beam_size=5`, `condition_on_previous_text=False`.
  - Modèle : `large-v3` sur GPU (`float16`), sinon `large-v3-turbo` sur CPU en `int8` (ou `medium` si turbo est indisponible).
  - Si CUDA pose problème, passe en CPU sans y perdre de temps.
- **Livrables par fichier** dans `_PLANS\transcriptions` :
  - `<nom>.srt` : une entrée par phrase ;
  - `<nom>_mots.json` : chaque mot avec son début, sa fin et sa probabilité ;
  - `<nom>.md` : version lisible, une phrase par ligne, préfixée par `[mm:ss.cc → mm:ss.cc]`, avec `(?)` après chaque mot de confiance inférieure à 0,5.
- **Noms propres.** Whisper peut mal entendre les noms propres et le nom de la marque. Ne corrige jamais au hasard : signale le doute.
- **Niveaux et défauts audio.** Mesure le niveau de chaque témoignage (`ffmpeg -af ebur128` : LUFS intégré et crête). Note les défauts audio : bruit, écho, saturation, musique de fond.

### Étape 3 : analyse et banque de citations
- **Images.** Extrais 6 à 10 images par témoignage avec ffmpeg et **regarde-les** : cadrage, position du visage, lumière, fond, qualité.
  - Pour une source 16:9, définis le recadrage 9:16 (position horizontale du visage).
  - Repère les meilleures images d'ouverture : regard caméra, expression forte, yeux ouverts.
- **Fiche par témoignage.** Elle contient :
  - qui parle (prénom ou rôle **seulement** s'il est dit ou écrit dans les fichiers) ;
  - le contexte, la situation avant (le problème), le déclic, l'expérience ;
  - les résultats, en mots exacts avec leurs timecodes ;
  - les émotions, les objections levées, la recommandation ;
  - l'énergie et la qualité image et son.
- **Banque de citations** : `_PLANS\01_banque_citations.md`, plus une version `.csv`. Colonnes :
  - ID (`T1-Q03`), fichier, TC d'entrée, TC de sortie, durée ;
  - citation exacte ;
  - type : Résultat, Avant, Déclic, Expérience, Objection, Émotion ou Recommandation ;
  - potentiel d'accroche de 1 à 5 ;
  - remarques : mot coupé, bruit, regard, énergie.
- **Règle des timecodes.** Cale les bornes sur les timestamps des mots, avec une marge de 2 à 3 images (≈ 0,1 s) qui ne mord pas sur le mot voisin. Donne chaque timecode au format `hh:mm:ss:ii` (images, à la cadence du rush) et en secondes décimales.

### Étape 4 : questions (une seule fois, groupées)
Pose-moi en un seul message uniquement ce qui est indispensable et introuvable dans les fichiers, typiquement :
- l'offre et le texte exact de l'appel à l'action de fin ;
- logo, couleur et police, s'ils sont absents des dossiers ;
- plateforme et durée (par défaut : Meta Reels, Stories et fil, en 9:16, 20 à 35 s) ;
- le droit de mélanger plusieurs témoignages dans une pub, si le dossier Ads ne le dit pas ;
- l'accord écrit de chaque personne pour une utilisation publicitaire.

**N'attends pas mes réponses.** Continue avec les marqueurs `[OFFRE]`, `[CTA]` et `[COULEUR ACCENT]`, puis mets à jour quand je réponds.

### Étape 5 : les 6 plans
**Répartition des angles.** Si le dossier Ads impose déjà les 6 pubs, suis-le. Sinon, utilise cette répartition par défaut :

| Pub | Angle | Accroche | Structure |
|---|---|---|---|
| A1 | Résultat | la phrase de résultat la plus forte | résultat → avant → déclic → recommandation → CTA |
| A2 | Sceptique → convaincu | « J'étais sceptique… » (si quelqu'un le dit) | doute → essai → surprise → recommandation → CTA |
| A3 | Avant / après | la situation de départ | avant → bascule → après → CTA |
| A4 | Compilation | 3 à 5 voix, une phrase forte chacune | rafale de phrases fortes → CTA |
| A5 | Objection | la réponse vécue à l'objection n°1 (prix, temps, confiance…) | objection → réponse → résultat → CTA |
| A6 | Recommandation | « Si tu hésites… », un conseil direct | conseil → pourquoi → CTA |

- Chaque accroche doit être une phrase **réellement prononcée**. Si aucune citation ne porte un angle, remplace-le par un angle que la matière permet, et dis-le.
- Deux pubs ne partagent jamais la même accroche. Répartis les meilleurs témoignages pour que chaque pub ait une ouverture forte.

**Plan de chaque pub.** Un fichier par pub, de `_PLANS\A1_<angle>.md` à `A6_<angle>.md`, avec exactement les sections suivantes :

0. **Fiche** : angle, hypothèse testée en une phrase, durée totale calculée, témoignage(s) utilisé(s), points `[À CONFIRMER]`.
1. **Extraits à utiliser** : tableau `# | fichier | TC d'entrée | TC de sortie | durée | citation exacte`.
2. **Accroche d'ouverture (0 à 2 s)** :
   - l'image d'ouverture (laquelle, avec quel recadrage ou punch-in) ;
   - le texte du carton : citation exacte ou condensé fidèle, avec **la phrase source citée à côté** ;
   - le départ du son : la voix démarre-t-elle dès la première image, ou la musique avant ?
   - pourquoi ça arrête le scroll.
3. **Ordre des séquences** : tableau `TC timeline | partie | extrait # | cadrage | habillage | son`.
   - Parties : Accroche, Contexte, Déclic, Résultat, Recommandation, CTA.
   - Cadrage : 100 %, 118 % ou push-in.
4. **Textes à l'écran** : tableau `TC timeline | type | texte exact | mot en couleur d'accent | position | durée`.
   - Types : carton, mot-clé, bandeau nom, écran de fin.
   - 3 ou 4 cartons au maximum ; les sous-titres complets sont dans le `.srt`.
5. **Visuels, transitions et musique** :
   - inserts, seulement s'ils illustrent ce qui est dit, en précisant où les trouver dans les dossiers ou quoi capturer ;
   - transitions : où, laquelle, durée en images ;
   - musique : style, BPM, où elle monte, où elle s'efface ;
   - SFX.
6. **Notes de montage** : pièges (mot coupé, bruit, regard hors champ), accroche alternative à tester plus tard, temps de montage estimé.

**Fichiers associés à chaque pub** :
- **`A1_sous-titres.srt`** : sous-titres **en temps timeline**, importables dans Premiere.
  - Verbatim nettoyé, sans les « euh ».
  - Blocs de 3 à 5 mots, 2 lignes au maximum d'environ 22 caractères.
  - Un bloc n'est jamais à cheval sur deux extraits et dure au moins 0,4 s.
- **`A1_radio-edit.mp3`** : les extraits enchaînés dans l'ordre du plan, avec un micro-fondu de 10 ms à chaque coupe, pour que je valide le sens et le rythme à l'oreille.
- **Bonus, si le temps le permet** :
  - `A1.xml` : séquence au format FCP7 XML, importable via Premiere › Fichier › Importer. Elle est en 1080 × 1920, avec les extraits coupés et placés dans l'ordre, les médias liés par leur chemin local, et sans habillage. Vérifie que le fichier se relit correctement.
  - `A1_precut.mp4` : aperçu brut en 9:16 sans habillage, pour valider sur téléphone.

**Musique.** S'il existe une bibliothèque de musiques ou de SFX dans les dossiers Gateway, propose 2 ou 3 pistes adaptées (instrumentales, 110 à 128 BPM). Sinon, donne des mots-clés de recherche pour la Bibliothèque sonore de Meta, Artlist ou Epidemic Sound. **Même piste (2 au maximum) pour les 6 pubs.**

### Étape 6 : contrôle qualité (obligatoire avant de me rendre la main)
- Relis chaque citation mot à mot contre la transcription, et liste les mots à vérifier à l'oreille.
- Vérifie qu'aucune coupe ne change le sens.
- Vérifie que chaque chiffre ou résultat affiché est dit par la personne, à l'écran, au même moment.
- Vérifie que les durées sont dans la cible (20 à 35 s, écran de fin compris).
- Règles Meta : pas d'interpellation sur un attribut personnel, pas de faux éléments d'interface, textes dans la zone sûre.
- Cohérence du test : même habillage, même musique, même écran de fin. Seuls l'accroche et les extraits changent.
- Radio-edits : aucun mot coupé ni clic aux jonctions (contrôle avec les timestamps des mots).

### Étape 7 : récapitulatif
- **`_PLANS\RECAP.md`** :
  - un tableau des 6 pubs (angle, accroche, durée, témoignages, fichiers) ;
  - l'ordre de montage conseillé, les plus simples d'abord ;
  - les points à confirmer ;
  - comment lire le test : taux d'accroche à 3 s, rétention, CTR, CPA.
- **Dans le chat** : un résumé court et les questions encore ouvertes.

Si Premiere est connecté via un outil (par exemple le panneau Higgsfield et ses outils `pr_*`), propose de poser directement le dérush des 6 séquences dans un projet, sans le faire d'office.

## Charte commune (à appliquer aux 6 pubs)

**Specs**
- 9:16, 1080 × 1920, à la cadence des rushs.
- 20 à 35 s (45 s au maximum).
- Vidéo : H.264 en VBR, 15 Mbit/s cible et 20 au maximum.
- Audio : AAC 48 kHz, 320 kbit/s, **−14 LUFS intégré et crête vraie à −1 dBTP**.
- Nommage : `GW_TEMO_A1_<angle>_v1.mp4`.

**Test lisible.** Tout est identique sauf l'accroche et les extraits : même habillage, même musique (2 au maximum), même écran de fin, durées à ±5 s.

**Zone sûre**
- Les infos importantes restent entre y = 300 et y = 1240 px, à au moins 70 px des bords. L'interface des Reels masque 14 % de l'écran en haut et 35 % en bas, et le fil recadre en 4:5.
- Sous-titres : centrés vers y ≈ 1150 px.
- Cartons : vers y ≈ 420 px, sans masquer les yeux.

**Habillage**
- **Police et couleurs** : une seule police, Montserrat Bold/ExtraBold (ou celle de la marque). Blanc, noir et une seule couleur d'accent (celle de la marque, sinon `#FFD60A`).
- **Sous-titres, présents tout le long** :
  - blanc, 64 à 72 px, ombre douce (noir à 60 %, flou de 8 à 10 px), sans contour épais ;
  - 3 à 5 mots par bloc et 2 lignes au maximum ;
  - un seul mot-clé par phrase en couleur d'accent.
- **Cartons d'emphase** :
  - texte noir sur un cartouche blanc aux coins arrondis (rayon ≈ 16 px), 7 mots au maximum ;
  - 1,5 à 2,5 s à l'écran, 3 ou 4 au maximum par pub ;
  - quand le carton dit la même chose que le sous-titre, masque le sous-titre ;
  - un carton peut condenser une phrase en retirant des mots, mais jamais ajouter un mot ni changer le sens.
- **Animation** : apparition « pop » (échelle de 90 à 100 % et opacité, sur 4 images), sortie en coupe sèche. Rien d'autre.
- **Bandeau nom** (prénom et contexte) : 2 s, seulement avec des infos vérifiées.

**Rythme et image**
- **Coupes** : retire les blancs, les respirations et les hésitations, sans jamais couper au milieu d'un mot.
- **Cadrage** : alterne 100 % et 115 à 120 % à chaque coupe.
- **Changements** : jamais plus de 3 s sans changement (coupe, zoom, carton ou insert).
- **Phrase clé** : push-in de 100 à 106 % sur sa durée.
- **Étalonnage** : léger et homogène, sans LUT créative.
- **Inserts** : 2 ou 3 au maximum, seulement s'ils illustrent ce qui est dit.

**Transitions (une seule famille pour les 6 pubs)**
- Dans un même témoignage : coupe sèche et punch-in.
- Entre deux témoignages ou deux parties : zoom croisé de 6 à 8 images, ou fondu au blanc de 3 ou 4 images, calé sur un temps fort de la musique, avec un whoosh discret.
- Vers l'écran de fin : fondu de 6 images.

**Musique et mix**
- **Musique** : instrumentale (sans paroles), entraînante, 110 à 128 BPM, énergie montante.
- **Licence publicitaire obligatoire** : Bibliothèque sonore de Meta, Artlist, Epidemic Sound (licence commerciale) ou Commercial Music Library de TikTok.
- **Voix** : Améliorer la voix (Enhance Speech) entre 40 et 70 % s'il y a du bruit, passe-haut à 80 Hz, niveaux homogènes d'un témoignage à l'autre.
- **Ducking contre le dialogue** : sensibilité 6, réduction de −15 à −18 dB, fondus de 500 ms. La musique remonte sur les 0,5 premières secondes et sur l'écran de fin.
- **SFX** : whoosh vers −20 dB sur les transitions, « pop » vers −24 dB sur les cartons, rien sur les sous-titres.

**Écran de fin (identique sur les 6)** : 2 à 3 s, fond uni, logo Gateway, `[OFFRE]` et `[CTA]`, avec la musique qui remonte.

**Garde-fous**
- **Chiffres** : affichés tels qu'ils sont dits, au moment où ils sont dits.
- **Résultats hors norme** : ajoute « Résultats individuels, non garantis ».
- **Attributs personnels** : pas d'interpellation du type « Tu es endetté ? ». La citation à la première personne passe.
- **Visuels** : pas de fausse interface ni d'avant/après trompeur.
- **Droit à l'image** : accord écrit de chaque personne.

**Méthode Premiere**
- **Séquence master**, ensuite dupliquée 6 fois. Elle contient :
  - le calque d'effets ;
  - le style de piste `GW_Sous-titres` ;
  - le carton `GW_Carton` (Objets graphiques essentiels) ;
  - l'écran de fin ;
  - la musique, avec l'atténuation déjà réglée.
- **Montage** par le texte.
- **Sous-titres** importés depuis les `.srt`.
- **Export** en lot via Media Encoder.

**Check-list avant envoi**
- L'accroche est lisible dès la première seconde.
- Pub testée sur téléphone, sans le son puis avec le son.
- Zone sûre et orthographe vérifiées.
- Aucun propos ni chiffre ajouté.
- Voix intelligible, crête ≤ −1 dBTP.
- Licence musicale OK.
- Nommage conforme.

**Commence par l'étape 1 maintenant.**
