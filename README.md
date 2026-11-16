# État de caisse — 30 Minutes Multi-Services

Page de la caisse centrale (fichier unique `index.html`) : saisie de l'état de caisse du jour, répertoire de tous les états enregistrés et rapports de gestion en PDF et en Excel.

## Les quatre onglets

1. **État du jour** : on colle les rapports WhatsApp des vendeurs, puis on complète les recettes, les crédits, les dépenses et les dépôts. Le bouton « Enregistrer dans le répertoire » garde la journée. On peut aussi télécharger le PDF et l'Excel du jour.
2. **Répertoire** : tous les états enregistrés, mois par mois. Les jours sans état apparaissent comme manquants. On peut rouvrir une journée pour la corriger, ou télécharger son PDF.
3. **Rapports** : rapport PDF et fichier Excel sur une période au choix (hier, semaine dernière, ce mois, mois dernier, ou deux dates).
4. **Réglages** : nom de l'utilisateur et accès au dépôt privé.

## Ce que l'import des rapports récupère

- ventes par produit, crédits des clients, loyalty, dépenses payées par le vendeur, espèces remises ;
- vendeur et pompiste, compteur d'ouverture et de fermeture, jauges ;
- réceptions de gaz : fournisseur, numéro du bon de livraison, camion, chauffeur, gallons payants et en remise ;
- deux services le même jour (« Shift 2 ») : les deux rapports s'additionnent.

Le texte d'origine de chaque rapport est archivé dans le dépôt privé (dossier `rapports`).

## Contrôles automatiques

- total et encaisse du vendeur recalculés ;
- compteur d'ouverture comparé à la fermeture de la veille ;
- sortie du compteur comparée aux gallons vendus ;
- jauge au-dessus de 85 % après une réception ;
- écart de caisse par point (tolérance 150 HTG) ;
- espèces remises comparées aux dépôts en banque ;
- chèques non déposés, crédits sans nom de client, dépenses sans reçu, livraisons sous 375 HTG le gallon.

## Contenu du rapport de période

Synthèse, jour par jour, par point de vente (ventes, gallons, écarts), recettes par catégorie, crédits accordés et recouvrés par client, dépenses par catégorie et en détail, dépôts par compte, réceptions de gaz par fournisseur, points d'attention.

Le fichier Excel de la période contient les mêmes données ligne par ligne, pour la saisie dans OneBooks.

## Mise en ligne de la page (dépôt public)

1. Sur github.com, ouvrez le dépôt `etat-de-caisse` (ou créez-le : New repository → Public).
2. Add file → Upload files → glissez `index.html` et `README.md` → Commit changes.
3. Settings → Pages → Branch `main`, dossier `/ (root)` → Save.
4. Adresse : `https://<votre-compte>.github.io/etat-de-caisse/`

La page ne contient aucun rapport : elle peut rester publique.

## Dépôt privé des rapports

Les états de caisse sont rangés dans un second dépôt, **privé**. La page refuse d'envoyer quoi que ce soit si ce dépôt est public.

1. github.com → New repository → nom `etat-de-caisse-donnees` → **Private** → cochez « Add a README file » → Create repository.
2. Photo de profil → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token.
   - Repository access : « Only select repositories » → `etat-de-caisse-donnees`.
   - Permissions → Repository permissions → Contents : « Read and write ».
   - Generate token, puis copiez la clé (`github_pat_…`).
3. Dans la page, onglet Réglages : compte GitHub, dépôt `etat-de-caisse-donnees`, clé d'accès → « Tester la connexion ».
4. Refaites l'étape 3 sur chaque appareil (Johny, Sagine, caisse centrale).

La clé reste dans le navigateur de l'appareil. Si un téléphone est perdu, supprimez la clé dans GitHub (même écran qu'à l'étape 2) et créez-en une nouvelle.

Rangement dans le dépôt privé :

- `etats/2026-11/2026-11-16.json` : un fichier par journée ;
- `rapports/2026-11/2026-11-16.json` : le texte des rapports des vendeurs de la journée.

GitHub garde l'historique de chaque modification : on peut toujours voir qui a changé une journée et quand.

## Sans dépôt privé

La page fonctionne aussi sans clé : les états restent alors sur l'appareil. Les boutons « Télécharger une sauvegarde » et « Importer une sauvegarde » du Répertoire servent à les transférer.

## Modifier les prix, points ou comptes

En haut du premier script de `index.html` : `PTS` (points de vente), `CAT_REC` (catégories de recettes et prix par défaut), `CAT_DEP` (catégories de dépenses), `COMPTES` (comptes bancaires), `LIVRAISON_PRIX` et `PYRO_PRIX` (prix contrôlés). La tolérance d'écart (`TOL`) est en haut du second script.
