# Mon Trajet en Allemand — projet d'app

App d'apprentissage de l'allemand mains-libres **et sans les yeux** (voiture,
course à pied) pour francophones. Chaque leçon se déroule intégralement à la
voix, sans aucun tap nécessaire pour avancer : introduction → aperçu des
phrases en français → apprentissage (français, puis allemand répété deux
fois avec un temps de silence pour répéter à voix haute) → deux phases de
test parlées → clôture → point de grammaire lu à voix haute si la leçon en
a un → enchaînement automatique sur la leçon suivante.
**Aucune reconnaissance vocale** : l'app n'écoute jamais l'utilisateur, les
temps de silence sont uniquement chronométrés.

> Quatrième maillon de la famille d'apps « Mon Trajet en... » (anglais,
> espagnol, italien, maintenant allemand) — dupliqué à partir du dépôt le
> plus abouti de la famille (`mon-trajet-en-italien` : icône intégrée,
> correctif safe-area, signature manuelle Codemagic).

## Niveaux

L'app propose trois **niveaux** (onglets en haut de l'accueil, au-dessus des
onglets de module) : même structure de 3 modules × 20 leçons × 10 phrases
par niveau, mais des situations différentes et un vocabulaire plus riche à
chaque niveau supérieur (jamais un remake des mêmes scènes). Un seul achat
premium débloque tous les modules payants, sur tous les niveaux.

- **Niveau 1** (A1) — terminé : 600 phrases, 3 modules, 15 points de
  grammaire (articles der/die/das, accusatif, verbes à particule séparable,
  modaux können/müssen, pluriel irrégulier, heure officielle, etc.).
- **Niveau 2** (A2) — terminé : 600 phrases, 3 modules, 15 points de
  grammaire (datif, Perfekt avec haben/sein, prépositions mixtes,
  comparatif, subordonnées weil/dass, génitif simple, etc.).
- **Niveau 3** (B1-B2) — terminé : 600 phrases, 3 modules, 15 points de
  grammaire (Konjunktiv II de politesse et d'irréel, passif présent et
  passé, discours indirect/Konjunktiv I, subordonnées enchâssées,
  particules modales, etc.).

**Total : 1 800 phrases, 45 points de grammaire, 180 leçons.**

## Ancrage culturel

Les trois modules de chaque niveau suivent un fil culturel cohérent :
- **Module 1 « Le quotidien »** : arrivée et installation en Allemagne —
  Berlin (porte de Brandebourg, Reichstag, cathédrale), la Forêt-Noire,
  l'Autobahn, la Bavière (Biergarten, Spätzle, bière), vie quotidienne
  (bureaucratie, assurance maladie, associations/Vereine, Feierabend).
- **Module 2 « En voyage »** : Francfort, la Deutsche Bahn, la vallée du
  Rhin et ses châteaux, Cologne et sa cathédrale, Hambourg et son port,
  les marchés de Noël (Dresde, Nuremberg), l'Oktoberfest à Munich, le lac
  de Constance, la mer Baltique et l'île de Rügen, les vendanges sur la
  Moselle, le mur de Berlin.
- **Module 3 « Conversation sociale »** : échanges progressivement plus
  profonds, ancrés dans la vie sociale allemande (différences régionales,
  élections locales, intégration, identité, amitié).

Aucune référence résiduelle à l'Espagne, l'Italie, les USA ou
l'Angleterre ne subsiste dans le contenu (vérifié par grep sur l'ensemble
du fichier `data.js`, y compris les phrases méta de fin de niveau/module).

## Ce qui est déjà fait

- Web app complète (`www/`), dupliquée depuis le dépôt italien (le plus
  abouti de la famille) : écran d'accueil avec sélecteur de niveau,
  lecteur de leçon 100% audio-automatique, points de grammaire parlés,
  paywall, **icône d'app intégrée**, **correctif safe-area** (encoche/Dynamic
  Island) sur les écrans d'accueil et de session.
- Chapitre d'orientation « Bien commencer ensemble » avant la leçon 1 du
  module 1, détection automatique iOS/Android pour le bon chemin de
  réglages système.
- Navigation ±10 secondes et barre de progression dans une leçon.
- Points de contrôle « Évaluation » toutes les 5 leçons + évaluation finale
  de module (60 phrases), numérotation continue sur tout le parcours.
- Déroulé de leçon entièrement scripté et automatique (voir
  `www/js/app.js`, fonction `playLessonFlow`), identique au moteur des
  autres apps de la famille — seul `www/js/data.js` change de langue
  (champ `de` au lieu de `it`/`es`/`en`), ainsi que la locale TTS `de-DE`.
- **Les 9 modules sont entièrement rédigés — 180 leçons, 1 800 phrases,
  45 points de grammaire**, vérifiés par script Node : nombre exact de
  phrases et de tips, aucun champ `de` manquant, aucune phrase FR
  dupliquée, syntaxe JS valide (`node -c data.js`).
- Paywall avec 10 leçons gratuites au niveau 1 (module 1 uniquement), 3
  leçons gratuites par niveau ensuite, le reste payant.
- Design system identique à toute la famille (dark, glanceable, une
  couleur par phase) — seul l'**accent de la marque change** : un bleu vif
  « Autobahn » (`#2E7DFF`), dans la même logique que les autres apps
  (anglais `#FF7A29`, espagnol `#FFB23D`, italien `#3DDC97`).
- `codemagic.yaml` configuré en **signature manuelle** (provisioning
  profile `mon_trajet_allemand_app_store` + certificat « iOS
  Distribution » référencés par nom, pas de signature automatique),
  génération d'icône via `@capacitor/assets`, et déclaration
  `ITSAppUsesNonExemptEncryption`.

## Ce qu'il reste à faire

Le contenu est terminé. Ce qui reste concerne la mise en production :
- Tester réellement l'app sur un iPhone.
- Créer le compte RevenueCat et les produits App Store Connect / Google
  Play (voir section dédiée plus bas) — **`REVENUECAT_API_KEY_IOS` est un
  placeholder `TODO_REVENUECAT_KEY_ALLEMAND`** tant que ce compte n'existe
  pas.
- Créer le profil de provisionnement `mon_trajet_allemand_app_store` dans
  App Store Connect / Apple Developer, référencé par `codemagic.yaml`.
- Relire/ajuster le contenu si certaines phrases ou tournures ne
  conviennent pas — tout est dans `www/js/data.js`.
- Pousser ce dossier vers le dépôt GitHub `mon-trajet-en-allemand` (créé
  mais vide à ce jour) dès qu'il est prêt à recevoir du code.

## Important : ce que ce projet EST et N'EST PAS

Ce dossier est un vrai projet **Capacitor** (web app encapsulée en app
native). Il n'est pas possible, depuis cet environnement, d'exécuter
`npm install`, de générer le projet Xcode, ni de compiler/signer/soumettre
l'app sur l'App Store (il faut un Mac + Xcode + un compte Apple
Developer). Tout ça se fait côté utilisateur, avec les commandes
ci-dessous.

## Étapes pour arriver sur l'App Store (et Google Play)

### 1. Préparer l'environnement (chez toi)
```bash
cd mon-trajet-en-allemand
npm install
```

### 2. Ajouter les plateformes natives
```bash
npx cap add ios       # nécessite Xcode (Mac uniquement)
npx cap add android    # nécessite Android Studio
npx cap sync
```

### 3. Ouvrir et lancer
```bash
npx cap open ios       # ouvre le projet dans Xcode
npx cap open android   # ouvre le projet dans Android Studio
```

### 4. Achat intégré (paiement) — code déjà en place, comptes à créer
Le code d'intégration **RevenueCat** est déjà écrit dans `www/js/app.js`
(`initPurchases`, `buyPremium`, `restorePremium`, `applyCustomerInfo`) :
- Tant que l'app tourne dans un navigateur classique (tests via
  `npx serve`), `window.Capacitor` n'existe pas → l'app reste
  automatiquement sur le mode test (déblocage immédiat, sans paiement).
- Dans l'app compilée (iOS/Android), le vrai flux RevenueCat
  (StoreKit / Play Billing) prend le relais automatiquement.

Ce qu'il reste à faire, uniquement côté comptes/configuration :
1. Créer un compte sur [revenuecat.com](https://www.revenuecat.com) (gratuit
   jusqu'à 2 500 $/mois de revenus suivis).
2. Créer le produit « version complète » dans **App Store Connect** et dans
   la **Google Play Console**, avec le même identifiant produit des deux
   côtés : `version_complete_de`.
3. Dans RevenueCat, connecter les deux stores, créer un entitlement
   `mon_trajet_en_allemand_pro` rattaché à ce produit, et récupérer les
   deux clés API publiques (une iOS, une Android).
4. Coller ces valeurs dans `app.js`, tout en haut du bloc PAYWALL :
   `REVENUECAT_API_KEY_IOS` (actuellement `TODO_REVENUECAT_KEY_ALLEMAND`),
   `REVENUECAT_API_KEY_ANDROID` (`TODO_REVENUECAT_ANDROID_KEY`).
   `ENTITLEMENT_ID` et `PRODUCT_ID` sont déjà renseignés.
5. `npm install` (ajoute `@revenuecat/purchases-capacitor`), puis
   `npx cap sync` pour que le plugin natif soit inclus dans le projet.

### 5. Signature iOS (Codemagic)
`codemagic.yaml` est configuré en **signature manuelle** :
- Profil de provisionnement à créer dans Apple Developer / App Store
  Connect : `mon_trajet_allemand_app_store`.
- Certificat : « iOS Distribution » (partagé avec le reste de la famille
  d'apps si déjà créé).
- Bundle ID : `com.tonstudio.montrajet.allemand`.

### 6. Comptes nécessaires
- **Apple Developer Program** : 99 $/an, obligatoire pour publier sur
  l'App Store.
- **Google Play Console** : 25 $, paiement unique.

### 7. Soumission
- iOS : build via Codemagic (ou Xcode) → App Store Connect → renseigner
  fiche, captures d'écran, prix, puis soumettre à la revue Apple.
- Android : build dans Android Studio (.aab) → Google Play Console →
  fiche + revue.

## Structure du projet

```
mon-trajet-en-allemand/
  package.json
  capacitor.config.json
  codemagic.yaml
  assets/
    icon.png      <- 1024x1024, accent bleu "Autobahn" #2E7DFF
    splash.png    <- 2732x2732
  www/
    index.html
    css/style.css   <- correctif safe-area conservé tel quel
    js/data.js      <- tout le contenu pédagogique (1 800 phrases, 45 tips)
    js/app.js       <- toute la logique de l'app (moteur partagé avec la famille)
```

## Vision corpus multi-langues

Ce projet fait partie d'une famille d'apps « Mon Trajet en... » dont le
moteur (`app.js`, `style.css`, `index.html`) est entièrement indépendant du
contenu — seul `data.js` contient les phrases et le français en dur.

Pour créer une nouvelle app de la famille à partir de celle-ci :
1. Copier tout le dossier, lui donner un nouveau nom.
2. Réécrire `www/js/data.js` avec des phrases FR nouvelles et variées (ne
   jamais recopier celles d'une autre langue de la famille) et leur
   traduction dans la nouvelle langue cible (le champ `de` devient par
   exemple `nl` pour le néerlandais), et adapter les appels `speak(...)`
   dans `app.js` en conséquence (locale TTS, libellés UI).
3. Changer `appId` et `appName` dans `capacitor.config.json`, `name` /
   `description` dans `package.json`, bundle ID et nom de profil dans
   `codemagic.yaml`.
4. Générer une nouvelle icône/splash avec le même motif (route + ondes
   sonores) mais une nouvelle couleur d'accent de la famille.
5. Le design (couleurs de base, typographie, écrans, paywall, points de
   grammaire) reste identique — c'est l'identité de marque commune à toute
   la famille d'apps.
