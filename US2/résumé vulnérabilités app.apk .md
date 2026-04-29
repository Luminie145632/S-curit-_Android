# Résumé de l'Audit MobSF

*   **Application :** Nickel (com.fpe.comptenickel)
*   **Score de sécurité :** 49/100 (Note B - Risque Moyen)

---

### 🔴 Vulnérabilités Critiques (High)

*   **Trafic réseau en clair autorisé :** L'attribut `android:usesCleartextTraffic=true` est activé, ce qui permet à l'application de communiquer via des protocoles non chiffrés (comme HTTP). Cela expose les données des utilisateurs aux interceptions (attaques Man-in-the-Middle).
*   **Cryptographie obsolète :** Le code utilise le mode de chiffrement CBC avec un padding PKCS5/PKCS7, une configuration connue pour être vulnérable aux attaques de type *Padding Oracle*.
*   **Support d'OS obsolètes :** L'application cible un `minSdk=19` (Android 4.4), permettant son installation sur des appareils dont les failles de sécurité ne sont plus patchées par Google.

### 🟠 Vulnérabilités Moyennes et Avertissements (Warnings)

*   **Exposition des composants (IPC) :** Plusieurs composants internes sont exportés publiquement (`android:exported=true`), dont des *Broadcast Receivers*, des *Services* (ex: `FcmRegistrationService`) et un *Content Provider* (`PushwooshSharedDataProvider`). Cela permet à d'autres applications malveillantes présentes sur le téléphone d'interagir avec eux.
*   **Risque d'injection SQL :** L'application utilise des bases de données SQLite avec des requêtes SQL brutes (Raw SQL), ce qui peut introduire des failles d'injection si les entrées utilisateurs ne sont pas correctement filtrées.
*   **Stockage et Permissions :** L'application possède les droits de lecture et d'écriture sur le stockage externe (`WRITE_EXTERNAL_STORAGE`). Les données qui y sont écrites peuvent être lues par d'autres applications. De plus, 8 permissions demandées sont répertoriées comme fréquemment abusées par les malwares (notamment la lecture des contacts).
*   **Pratiques cryptographiques faibles :** Utilisation de l'algorithme de hachage MD5 (sujet aux collisions) et de générateurs de nombres aléatoires non sécurisés.

### 🟡 Fuites d'informations (Info / Hardcoded Secrets)

*   **Secrets codés en dur :** Des informations très sensibles sont présentes en clair dans le code source, notamment des clés d'API Google (`google_api_key`, `google_crash_reporting_api_key`), des URL d'API privées (`CUSTOMER_AUTHENTICATION_ENDPOINT`), et l'URL de la base de données Firebase.
*   **Certificat d'application :** L'application n'est signée qu'avec le schéma v1, ce qui la rend vulnérable à la faille Janus sur les anciennes versions d'Android. De plus, le certificat utilise l'algorithme de hachage SHA1, aujourd'hui considéré comme cryptographiquement faible.
