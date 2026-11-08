# una-scanner — Pointage du Week-end Culturel AEEMCI S/C UNA

Scanner de QR Codes pour la 6ᵉ édition du Week-end Culturel
(20, 21 et 22 novembre 2026, Université Nangui ABROGOUA).

Adresse du scanner : https://hackerdialls.github.io/una-scanner/

## Fonctionnement

Le scanner fonctionne seul, directement sur le téléphone des agents d'accueil.
Il lit le QR Code du reçu et l'envoie à l'application Google Apps Script
(fonction `doPost`), qui enregistre la présence dans le Google Sheets.

```
Téléphone (GitHub Pages) ──POST JSON──▶ Apps Script /exec ──▶ Google Sheets
```

Plusieurs téléphones peuvent pointer en même temps.

## Configuration (une seule fois)

1. Dans Apps Script : **Déployer → Gérer les déploiements**.
   Le déploiement doit être réglé sur :
   - Exécuter en tant que : **Moi**
   - Qui a accès : **Tout le monde**
2. Copier l'URL du déploiement (elle se termine par `/exec`).
3. Sur GitHub, ouvrir `config.js` → crayon (Edit) → coller l'URL dans `API_URL`
   → **Commit changes**. GitHub Pages se met à jour en 1 à 2 minutes.

## Le jour de l'activité

1. Ouvrir https://hackerdialls.github.io/una-scanner/ dans Chrome (Android)
   ou Safari (iPhone).
2. Saisir le code PIN du comité et choisir la journée.
   La journée du jour est sélectionnée automatiquement.
3. Autoriser la caméra quand le navigateur le demande.
4. Présenter le QR Code du reçu :
   - **Vert** : présence enregistrée
   - **Orange** : déjà pointé ce jour
   - **Rouge** : refusé (QR inconnu, participant introuvable…)
   - **Bleu** : pas de réseau, le pointage est mis en attente
5. Sans QR Code : saisir la référence (ex. `UNA-WC26-00006`) puis **POINTER**.

L'écran reste allumé pendant le pointage (si le téléphone le permet).

## Hors ligne

Si le réseau coupe, les pointages sont gardés sur le téléphone (compteur
« En attente ») et envoyés automatiquement toutes les 15 secondes dès que la
connexion revient. L'heure enregistrée dans le Sheet est alors l'heure de
synchronisation. Ne pas vider les données du navigateur tant que le compteur
« En attente » n'est pas à 0.

## Dépannage

| Problème | Solution |
|---|---|
| « Scanner non configuré » | `API_URL` manquant ou incorrect dans `config.js` |
| « Impossible de joindre le serveur » | Vérifier Internet, l'URL `/exec`, l'accès « Tout le monde » |
| « Réponse inattendue du serveur » | Le déploiement n'est pas public ou la nouvelle version n'est pas déployée |
| Caméra refusée | Cadenas à côté de l'adresse → Autorisations → Caméra → Autoriser, puis recharger |
| « Code PIN incorrect » | Vérifier `ADMIN_PIN` dans les propriétés du script Apps Script |

## Fichiers

| Fichier | Rôle |
|---|---|
| `scanner.html` | Application de pointage |
| `config.js` | URL de l'application web Apps Script |
| `index.html` | Redirection vers `scanner.html` |
| `assets/` | Logos AEEMCI et 50 ans, bibliothèque html5-qrcode 2.3.8 (licence Apache 2.0) |

---

**S/C UNA, la science notre priorité !** — AEEMCI, pour une identité islamique !
