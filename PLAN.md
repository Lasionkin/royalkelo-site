# PLAN DE CONSTRUCTION — royalkelo.com

Ce document est autonome. Il ne renvoie a aucune conversation anterieure, a aucune version
precedente, a aucun autre fichier que ceux qu'il nomme. Tout ce qu'il faut pour batir le site
est ici.

---

## 0. Ce que tu construis

Le site commercial de **Royal KEL'O**, une entreprise de Montreal fondee par Enock
Lasi'onkin Kasiam. Une page unique, longue, defilante, servie en local pendant la
construction sur `http://127.0.0.1:3000`.

**Pile technique imposee :** HTML, CSS et JavaScript ecrits a la main. Aucun cadriciel, aucun
npm, aucune etape de compilation. Le site doit s'ouvrir en double-cliquant `index.html`.
Raison : il est bati et modifie depuis un telephone Android.

**Arborescence exacte a produire :**

```
index.html
styles.css
main.js
assets/
  logo.svg            <- fourni par Enock, JAMAIS dessine par toi (voir section 2)
  demo/               <- images reelles que TU enregistres (voir section 5)
    01.png ... NN.png
```

---

## 1. Ce qu'est Royal KEL'O, et ce qu'il n'est pas

Royal KEL'O est **100 % commercial**. C'est la seule porte commerciale de l'ecosysteme
d'Enock. Rien d'evangelique, rien de ministeriel, rien de caritatif n'apparait sur ce site.

Services reels, dans cet ordre d'importance :

1. **Automatisation de navigateur vendue en service** aux entreprises.
2. **Implantation d'intelligence artificielle en entreprise**, et formation des employes
   comme des dirigeants qui veulent apprendre eux-memes.
3. **Applications mobiles** developpees rapidement.
4. **Conception de sites web.**
5. **Textile Royal KEL'O**, vetements a la marque.

Les deux premiers occupent le haut de la page. Les trois autres viennent plus bas, en cartes
plus petites.

**N'invente aucun service.** Si un service n'est pas dans la liste ci-dessus, il n'existe pas.
En particulier : ni evenementiel, ni traiteur, ni decoration, ni conciergerie.

---

## 2. Regle absolue sur le logo

Le logo officiel ROYAL KEL'O **ne se recree jamais, ne se redessine jamais, ne se simule
jamais**. Cette regle passe avant toute autre consideration esthetique.

Concretement :

- Tu places une balise `<img src="assets/logo.svg" alt="Royal KEL'O">` dans l'en-tete.
- Si `assets/logo.svg` n'existe pas encore, tu laisses **un cadre vide reserve**, aux bonnes
  dimensions, portant le texte `EMPLACEMENT DU LOGO OFFICIEL`. Tu ne dessines rien dedans.
- Tu ne fabriques **aucun** monogramme, embleme, blason, couronne, lettrine, filigrane, ni
  composition typographique doree presentee comme signature de marque.
- Tu ne generes aucune image de logo, par aucun moyen.

Ce cadre vide est volontaire, ce n'est pas un travail inacheve. Un logo faux serait pire
qu'un emplacement honnete. Signale-le a Enock a la fin de ton travail.

**Ce qui reste autorise :** ecrire le nom « Royal KEL'O » dans le texte courant et dans les
titres, avec la typographie du site. Un nom dans une phrase n'est pas un logo. La frontiere
est la suivante : le nom dans une phrase, oui ; le nom compose en signature de marque, avec
degrade dore, ornements ou cadre, non.

---

## 3. Le systeme visuel : noir et or, royal et sobre

Standard vise : celui d'un site prime. Le generique et le croquis sont des echecs. La sobriete
n'est pas la pauvrete : le luxe se lit dans le vide, le rythme et la precision, pas dans
l'accumulation d'effets.

### 3.1 Couleurs, a declarer en variables CSS sur `:root`

```css
--noir:        #0A0A0B;   /* fond general */
--noir-carte:  #121214;   /* surfaces surelevees */
--ligne:       #26262B;   /* filets et bordures */
--or:          #C9A227;   /* accent, un seul ton, jamais de degrade multicolore */
--or-clair:    #E8CC6A;   /* survol et etats actifs uniquement */
--texte:       #EDEDEF;   /* texte principal */
--texte-doux:  #9A9AA3;   /* texte secondaire */
```

L'or est un **accent**, pas une couleur de fond. Regle de dosage : sur n'importe quel ecran,
l'or ne couvre jamais plus d'environ 5 % de la surface visible. Pas de grands aplats dores,
pas de boutons entierement dores plus larges que necessaire.

Contraste : tout texte doit atteindre au moins 4,5 contre son fond. `--texte-doux` sur
`--noir` passe ; ne descends pas plus bas. L'or sur noir passe pour du texte de grande taille,
pas pour du corps de texte : n'ecris jamais un paragraphe entier en or.

### 3.2 Typographie

Deux familles, chargees depuis Google Fonts avec `font-display: swap` et une pile de secours
declaree, pour que la page reste lisible hors ligne :

- Titres : `Cormorant Garamond`, graisse 300 et 600. Secours : `Georgia, 'Times New Roman', serif`.
- Texte et interface : `Inter`, graisses 400 et 600. Secours : `system-ui, -apple-system, sans-serif`.

Echelle fluide, a construire avec `clamp()` :

| Role | Taille |
|---|---|
| Titre de page | `clamp(2.6rem, 8vw, 6rem)` |
| Titre de section | `clamp(1.9rem, 4.5vw, 3.4rem)` |
| Sous-titre | `clamp(1.05rem, 2vw, 1.35rem)` |
| Corps | `clamp(1rem, 1.4vw, 1.125rem)` |
| Mention, legende | `0.85rem` |

Longueur de ligne : maximum 68 caracteres pour le corps de texte (`max-width: 34em`).
Interlignage : 1.6 pour le corps, 1.1 pour les grands titres.
Les sur-titres en capitales portent `letter-spacing: 0.18em`.

### 3.3 Espace et rythme

Echelle d'espacement, en variables : 4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 192 px.
Hauteur de section : `padding-block: clamp(96px, 14vh, 192px)`.
Gouttiere laterale : 20 px sur telephone, jamais moins.
Largeur de contenu : `min(1200px, 100% - 40px)`, centree.

### 3.4 Mouvement

Le mouvement sert a reveler, jamais a decorer.

- Apparitions au defilement par `IntersectionObserver` : opacite 0 vers 1, translation
  verticale de 24 px vers 0, duree 700 ms, courbe `cubic-bezier(.16,1,.3,1)`, decalage de
  60 ms entre elements voisins.
- Un seul filet dore qui se trace horizontalement sous chaque titre de section, duree 900 ms.
- Aucun parallaxe lourd, aucune particule, aucun curseur personnalise, aucun defilement
  detourne. Le defilement natif reste intact.
- `@media (prefers-reduced-motion: reduce)` : tout est instantane, rien ne bouge, rien ne
  disparait.

---

## 4. Structure de la page, dans l'ordre

1. **Barre superieure** fine, fixee, fond translucide floute. A gauche l'emplacement du logo.
   A droite trois ancres : Demonstration, Services, Contact. Sur telephone, les ancres
   deviennent une seule : Contact.
2. **Ouverture** (plein ecran).
3. **La demonstration** (section maitresse, voir section 5).
4. **Automatisation de navigateur** (service principal 1).
5. **L'IA implantee et enseignee** (service principal 2).
6. **Les autres services** (trois cartes plus petites).
7. **Comment on travaille** (trois etapes).
8. **Contact.**
9. **Pied de page.**

---

## 5. La demonstration : le coeur du site

C'est la section qui doit convaincre. Elle montre l'automatisation de navigateur **en train de
travailler**.

### 5.1 Regle de verite

Les images de cette section sont de **vraies captures**, pas des dessins, pas des maquettes,
pas des animations inventees. Tu les produis toi-meme ainsi :

1. Avec les outils du serveur `hpp` dont tu disposes, execute une tache reelle et utile dans le
   navigateur : ouvrir un site public, y chercher quelque chose, lire un resultat.
   Une suggestion neutre et reproductible : ouvrir `https://fr.wikipedia.org`, taper une
   recherche, ouvrir le premier resultat, faire defiler jusqu'a un tableau, le lire.
2. Prends une capture d'ecran **a chaque etape**, de 8 a 14 images.
3. Enregistre-les dans `assets/demo/` sous les noms `01.png`, `02.png`, et ainsi de suite.
4. Redimensionne-les pour que chacune pese moins de 300 Ko. Si aucun outil de
   redimensionnement n'est disponible, reduis la fenetre du navigateur avant de capturer.

Si tu n'arrives pas a produire ces captures reelles, **tu ne remplaces pas par des images
inventees**. Tu laisses la section vide avec une note visible, et tu le dis a Enock.

### 5.2 Mise en scene

Presentation en deux colonnes sur grand ecran, empilees sur telephone :

- **A gauche, l'instruction.** Un bloc sombre, bord dore fin, qui affiche la phrase en francais
  qui a declenche la tache, en train de s'ecrire lettre par lettre, vitesse 35 ms par
  caractere. Precede d'un chevron dore.
- **A droite, le navigateur.** Un cadre de navigateur dessine en CSS (barre d'onglet, trois
  pastilles, barre d'adresse), dans lequel les captures s'enchainent. Chaque image reste
  1,6 seconde, transition en fondu de 260 ms.

La sequence se lance **quand la section entre dans l'ecran**, pas au chargement de la page.
Elle boucle. Un bouton discret « Rejouer » sous le cadre.

Une barre de progression doree, fine, sous le cadre, indique ou en est la sequence.

### 5.3 Textes exacts de la section

- Sur-titre : `LA DEMONSTRATION`
- Titre : `Regardez-la travailler.`
- Texte : `Ce que vous voyez n'est pas une animation. C'est une sequence reelle, enregistree image par image dans un vrai navigateur, pilote par une seule phrase en francais.`
- Legende sous le cadre : `Sequence reelle enregistree le [DATE DU JOUR OU TU L'ENREGISTRES], acceleree.` Tu remplaces le crochet par la date reelle du jour ou tu produis les captures.
- Bouton : `Demander une demonstration en direct`

---

## 6. Les textes exacts du reste de la page

Utilise ces textes tels quels. Tu peux corriger une coquille, tu n'inventes pas de contenu
nouveau, tu ne rajoutes pas de chiffres, ni de pourcentages, ni de noms de clients.

### 6.1 Ouverture

- Sur-titre : `MONTREAL`
- Titre : `Nous mettons l'intelligence artificielle au travail dans votre entreprise.`
- Sous-titre : `Automatisation de navigateur. Implantation d'IA. Formation de vos equipes.`
- Bouton principal : `Voir la demonstration` (ancre vers la section demonstration)
- Bouton secondaire : `Nous ecrire`

Fond : noir profond, une seule source de lumiere doree tres diffuse en haut a droite, obtenue
par un `radial-gradient` a tres faible opacite. Rien d'autre. Pas d'image de stock.

### 6.2 Automatisation de navigateur

- Sur-titre : `SERVICE`
- Titre : `Automatisation de navigateur`
- Accroche : `Tout ce qu'une personne fait dans un navigateur, une machine peut le refaire. Sans se tromper, la nuit, cent fois de suite.`
- Liste :
  - `Extraction de donnees depuis des sites qui n'offrent aucune interface`
  - `Remplissage et depot de formulaires en serie`
  - `Veille quotidienne et rapports envoyes automatiquement`
  - `Taches repetitives que personne n'aime faire`
  - `Verification reguliere de vos propres sites et formulaires`
- Ligne de preuve, mise en valeur : `L'outil que vous venez de voir travailler est le notre. Nous nous en servons tous les jours.`

### 6.3 L'IA implantee et enseignee

- Sur-titre : `SERVICE`
- Titre : `L'IA, implantee et enseignee`
- Accroche : `Nous ne vendons pas un abonnement de plus. Nous installons l'intelligence artificielle la ou votre travail se fait, puis nous formons ceux qui vont s'en servir.`
- Liste :
  - `Audit de vos taches : ce qui gagne a etre automatise, et ce qui doit rester humain`
  - `Choix et mise en place des outils, chez vous, avec vos donnees`
  - `Formation des equipes, en francais ou en anglais`
  - `Formation des dirigeants qui veulent piloter eux-memes`
  - `Accompagnement apres la mise en place`

### 6.4 Les autres services

Trois cartes, meme taille, disposition en grille.

1. Titre `Applications mobiles` — texte `Des applications concues et livrees vite, sans equipe de dix personnes.`
2. Titre `Sites web` — texte `Des sites qui ne ressemblent a aucun autre. Celui que vous lisez en est un.`
3. Titre `Textile Royal KEL'O` — texte `Des vetements a la marque. Details sur demande.`

### 6.5 Comment on travaille

Trois etapes numerotees, chiffres en or, grands.

1. `On regarde` — `Une rencontre, vos ecrans, vos vraies journees. On repere ce qui se repete.`
2. `On construit` — `On bati l'outil, on vous le montre en marche, on corrige devant vous.`
3. `On vous forme` — `Vos gens savent s'en servir et le modifier. Vous ne dependez de personne.`

### 6.6 Contact

- Sur-titre : `PARLONS-EN`
- Titre : `Ecrivez-nous.`
- Texte : `Dites-nous en deux lignes ce qui vous fait perdre du temps. Nous repondons avec une demonstration, pas avec une brochure.`
- Bouton courriel : libelle `contact@royalkelo.com`, lien `mailto:contact@royalkelo.com`
- Bouton WhatsApp : libelle `WhatsApp`, avec l'attribut `href=""` et `data-a-remplir="whatsapp"`.
  **Tu n'inventes aucun numero de telephone.** Enock remplira ce lien lui-meme avec la ligne
  qu'il veut rendre publique. Signale-le lui a la fin de ton travail.

### 6.7 Pied de page

Une seule ligne, discrete : `Royal KEL'O — Montreal, Canada` et l'annee en cours, calculee en
JavaScript, jamais ecrite en dur.

---

## 7. Interdits

- Aucun chiffre invente : pas de « 200 clients », pas de « 40 % de temps gagne », pas de note
  sur cinq etoiles.
- Aucun temoignage, aucun avis, aucun nom de client, aucun logo d'entreprise cliente.
- Aucune image de banque d'images, aucune photo de personnes.
- Aucun emoji.
- Aucun tiret cadratin dans les textes francais. Virgule, point, deux-points, parentheses.
- Aucun texte de remplissage latin.
- Aucun violet, aucun degrade bleu-rose, aucune esthetique de page generee a la chaine.
- Aucun formulaire qui demande un mot de passe ou un moyen de paiement.
- Aucune mention de Heavenly Places Productions pour l'instant : ce site n'est pas encore en
  ligne, et on ne renvoie pas vers une adresse morte. On l'ajoutera quand il existera.

---

## 8. Qualite technique exigee

- **Telephone d'abord.** Tu ecris le CSS pour petit ecran, puis tu elargis avec
  `@media (min-width: 768px)` et `@media (min-width: 1200px)`.
- **Aucun defilement horizontal**, a aucune largeur.
- **Accessibilite** : un seul `<h1>`, hierarchie de titres continue, `alt` reel sur chaque
  image, contour de focus visible et dore sur tout element cliquable, navigation complete au
  clavier, `aria-label` sur les boutons sans texte.
- **Poids** : la page complete, images comprises, reste sous 2 Mo.
- **Aucune dependance externe** sauf les deux polices Google. Aucun script de suivi, aucune
  analytique, aucun cookie.
- Le titre de l'onglet : `Royal KEL'O`. Une `meta name="description"` d'une phrase. Les balises
  Open Graph `og:title`, `og:description`, `og:type` et `og:url`.

---

## 9. Comment tu verifies ton travail

Tu ne livres rien que tu n'aies regarde. Boucle obligatoire :

1. Sers le dossier : `python3 -m http.server 3000` en arriere-plan.
2. Avec les outils du serveur `hpp`, ouvre `http://127.0.0.1:3000`.
3. Prends une capture et **regarde-la**.
4. Dis honnetement ce qui ne va pas. Corrige. Recharge. Recapture.
5. Recommence jusqu'a ce que tu sois satisfait.

Tu repetes ce controle a **quatre largeurs de fenetre** : 390, 768, 1280 et 1920 pixels.
A chacune, tu verifies : pas de defilement horizontal, aucun texte sous 14 px, aucun texte
colle a un bord, aucun mot coupe bizarrement, aucun separateur orphelin en debut de ligne.

Tu verifies aussi, avec `prefers-reduced-motion` actif, que la page reste complete et lisible
sans aucune animation.

---

## 10. Ce que tu dis a Enock quand tu as fini

En quelques lignes, pas un rapport :

1. La capture finale.
2. Ce que tu as corrige a chaque passe, en une ligne chacune.
3. Les deux choses qu'il doit fournir lui-meme : le fichier `assets/logo.svg` et le lien
   WhatsApp.
4. Ce que tu n'as pas reussi a faire, s'il y a lieu, sans le maquiller.
