# FreshTrack — générer l'APK via GitHub

Application anti-gaspillage : scan de codes-barres, suivi des dates de péremption
et gestion du congélateur. Ce dépôt compile **automatiquement un fichier `.apk`**
grâce à GitHub Actions — tu n'as **rien à installer** sur ton ordinateur.

## Étapes (10 minutes)

1. **Crée un compte GitHub** (gratuit) si tu n'en as pas : https://github.com
2. **Crée un nouveau dépôt** : bouton « + » en haut à droite → *New repository*.
   Donne-lui un nom (ex. `freshtrack`), laisse-le **Public**, puis *Create repository*.
3. **Envoie ces fichiers** dans le dépôt. Deux options :
   - **Simple (navigateur)** : sur la page du dépôt → *Add file* → *Upload files*,
     puis glisse **tout le contenu** de ce dossier (y compris les dossiers `www` et
     `.github`). Valide avec *Commit changes*.
   - **Avec git** (si tu connais) :
     ```bash
     git init && git add . && git commit -m "FreshTrack"
     git branch -M main
     git remote add origin https://github.com/TON-PSEUDO/freshtrack.git
     git push -u origin main
     ```
4. **La compilation démarre toute seule.** Va dans l'onglet **Actions** du dépôt :
   tu verras le job *Build APK* tourner (≈ 3 à 5 min). Attends le ✅ vert.
   - S'il ne démarre pas : clique *Build APK* → *Run workflow*.
5. **Récupère l'APK** :
   - dans l'onglet **Releases** (à droite de la page d'accueil du dépôt), ou
   - dans **Actions** → ton build → section **Artifacts** → `FreshTrack-APK`.
6. **Installe-le sur ton téléphone Android** :
   - transfère/ouvre le fichier `app-debug.apk` sur le téléphone,
   - Android demandera d'**autoriser l'installation depuis cette source** : accepte,
   - ouvre l'appli, et autorise la **caméra** au premier scan.

## Bon à savoir

- L'APK est signé en mode **debug** : parfait pour un usage perso, mais non publiable
  sur le Play Store tel quel (il faudrait une signature de release).
- Le **scan de code-barres fonctionne hors-ligne** (la librairie est embarquée).
  La **récupération du nom du produit** (Open Food Facts) et le **scan de date (OCR, beta)**
  nécessitent une connexion internet.
- Pour relancer une compilation après une modif : il suffit de re-pousser un fichier,
  ou *Run workflow* dans l'onglet Actions. Un nouveau numéro de build est créé.

## Structure du projet

```
freshtrack/
├─ www/
│  ├─ index.html            ← l'application
│  └─ html5-qrcode.min.js   ← scan de codes-barres (hors-ligne)
├─ capacitor.config.json    ← config de l'appli (nom, identifiant)
├─ package.json             ← dépendances de compilation
└─ .github/workflows/
   └─ build-apk.yml         ← recette qui fabrique l'APK
```
