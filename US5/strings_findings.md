### 1. Clés d'API Google exposées
*   **Extrait :** `<string name="google_api_key">AIzaSyBTgztvImsUfMWDa41PCrDWAj7dmyIDhUg</string>`[cite: 3]. Note : cette même clé est répétée sous `google_crash_reporting_api_key`[cite: 3].
*   **Risque associé :** Quotas épuisés par un tiers, facturation abusive au nom de l'entreprise, ou accès non autorisé à d'autres services Google Cloud si la clé n'est pas strictement restreinte au nom de package de l'application.

### 2. URL de la base de données Firebase
*   **Extrait :** `<string name="firebase_database_url">https://application-client-nickel.firebaseio.com</string>`[cite: 3].
*   **Risque associé :** Risque critique d'exfiltration ou d'altération de données. Si les règles de sécurité Firebase (Realtime DB/Firestore) sont configurées sur "public" ou mal sécurisées, un attaquant peut lire/écrire directement dans la base.

### 3. Bucket de stockage Cloud
*   **Extrait :** `<string name="google_storage_bucket">application-client-nickel.appspot.com</string>`[cite: 3].
*   **Risque associé :** Similaire à Firebase, si les permissions du bucket Google Cloud Storage sont mal configurées, cela permet le vol de fichiers sensibles ou le dépôt de malwares.

### 4. Endpoints d'API internes (Reconnaissance)
*   **Extrait :** `<string name="CUSTOMER_AUTHENTICATION_ENDPOINT">https://api.nickel.eu/customer-authentication-api</string>`[cite: 3]. (Ainsi que les endpoints *Account* et *Personal Space*[cite: 3]).
*   **Risque associé :** Cartographie immédiate de la surface d'attaque. Un pirate connaît exactement l'URL de production[cite: 3] à cibler pour des attaques de type force brute, *credential stuffing* ou injection sur les processus d'authentification.

### 5. Identifiants de services tiers
*   **Extrait :** `<string name="PUSHWOOSH_APPID">DDF11-D1BF9</string>` et `<string name="default_web_client_id">717748501407...apps.googleusercontent.com</string>`[cite: 3].
*   **Risque associé :** Bien que souvent nécessaires côté client, ces identifiants facilitent l'usurpation d'identité de l'application pour interagir avec des services externes (campagnes de push frauduleuses, abus des flux OAuth).
