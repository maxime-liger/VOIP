# VOIP
:feelsgood:Veille Technologique sur la VOIP
<hr>
1. Coûts opérationnels et de maintenance de la VoIP <br>
Réponse : Les coûts opérationnels et de maintenance de la VoIP sont généralement inférieurs à ceux des systèmes téléphoniques traditionnels grâce à une infrastructure partagée, une maintenance centralisée, et des mises à jour logicielles faciles.
<hr>
2. Différence entre la configuration VoIP d'un call center et d'un standard téléphonique d'entreprise<br>
Réponse : Un call center utilise des fonctionnalités avancées comme l'ACD (répartition des appels) et l'IVR (menu vocal), tandis qu'un standard téléphonique d'entreprise se concentre sur des fonctions basiques comme le transfert d'appels et la conférence.
<hr>
3. Exemples de sites marchands utilisant la VoIP et architecture possible<br>
Réponse : Des entreprises comme Amazon, Uber, et Airbnb utilisent la VoIP pour leur service client. Une architecture typique inclut un serveur VoIP, des intégrations CRM, et des fonctionnalités comme l'ACD et l'IVR.
<hr>
4. Scalabilité des serveurs VoIP<br>
Réponse : Les serveurs VoIP sont facilement scalables : on peut ajouter ou supprimer des utilisateurs, augmenter les capacités d'appels, et déployer la même configuration sur plusieurs sites sans interruption de service.
<hr>
5. Sécurité et chiffrement adapté à la VoIP<br>
Réponse : Pour sécuriser la VoIP, on utilise des protocoles comme SRTP (chiffrement des médias), TLS (chiffrement de la signalisation), et AES (algorithme de chiffrement). Ces outils, combinés à des bonnes pratiques (authentification forte, mise à jour régulière), rendent la VoIP plus sécurisée que les systèmes traditionnels.
En résumé, la VoIP est économique, flexible, scalable, et sécurisée lorsqu'elle est bien configurée.


<hr><hr><hr>
📞 Projet VoIP : Présentation, Installation d'Asterisk et Plan de Test 🌐<br>
Ce projet explore la technologie VoIP (Voice Over Internet Protocol), une solution de communication moderne qui permet de passer des appels via Internet plutôt que via le réseau téléphonique traditionnel. La VoIP offre des avantages significatifs en termes de coût, de flexibilité et de fonctionnalités avancées, mais elle présente également des défis, notamment en matière de sécurité et de qualité audio.

📚 Contenu du projet
1. 📖 Introduction à la VoIP
Explication du concept et de son fonctionnement.

2. ⚖️ Avantages et Inconvénients
Comparaison entre la VoIP et la téléphonie traditionnelle.

3. 🛠️ Solutions existantes
Présentation des solutions open-source (Asterisk, FreeSWITCH) et payantes (RingCentral, Zoom Phone).

4. 🏢 Exemples d'implémentation
Cas d'utilisation dans différents contextes (entreprises, centres d'appel, hôtellerie).

5. 🖥️ Installation d'Asterisk
Guide étape par étape pour installer et configurer Asterisk, un serveur VoIP open-source.

6. 🔧 Configuration des utilisateurs et extensions
Exemple de configuration pour gérer les utilisateurs et les appels.

7. 🧪 Plan de Test - Serveur VoIP
Validation du bon fonctionnement du serveur VoIP avant mise en production.

🚀 Installation d'Asterisk
Étapes d'installation :
+Mise à jour du système et installation des dépendances :

```
sudo apt update && sudo apt upgrade -y  
sudo apt install -y build-essential git libxml2-dev libncurses5-dev uuid-dev libjansson-dev libssl-dev libsqlite3-dev sqlite3 pkg-config automake libcurl4-openssl-dev libnewt-dev libsqlite3-dev
```
+Téléchargement et installation d'Asterisk :

```
wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-22.2.0.tar.gz  
tar -xvzf asterisk-22.2.0.tar.gz  
cd asterisk-22.2.0  
./configure  
make  
sudo make install  
sudo make samples  
sudo make config
```
+Lancement et vérification :

```
sudo systemctl start asterisk  
sudo systemctl status asterisk  
sudo systemctl enable asterisk
```
🔧 Configuration des utilisateurs et extensions
Exemple de configuration :
Utilisateurs :
Ouvrez le fichier de configuration :


+ nano /etc/asterisk/pjsip.conf  
Ajoutez des utilisateurs comme suit :
```
ini
Copy
[2001]  
type = endpoint  
context = default  
disallow = all  
allow = ulaw,alaw  
auth = auth2001  
aors = 2001  

[auth2001]  
type = auth  
auth_type = userpass  
password = 2001  
username = 2001  

[2001]  
type = aor  
```
Extensions :
Ouvrez le fichier de configuration :

+ nano /etc/asterisk/extensions.conf  
Ajoutez des extensions comme suit :

```
[default]  
exten => 2001,1,Dial(PJSIP/2001,20)  
exten => 2001,2,Hangup()
```
🧪 Plan de Test - Serveur VoIP
Objectifs des tests :
🧑‍💻 Administration des utilisateurs

📞 Établissement et réception d'appels

🌐 Connectivité entre le serveur et les clients

🔄 Démarrage et redémarrage du serveur

🔒 Sécurisation des appels<hr>

Cas de tests :
Cas de test 1 : Création d’un utilisateur
État initial : Serveur VoIP fonctionnel, aucun utilisateur configuré.

Fonctionnalité testée : Création d'un utilisateur.

Comportement attendu : L'utilisateur doit être enregistré et pouvoir se connecter.

Étapes :

Accéder à l'interface d'administration.

Ajouter un nouvel utilisateur.

Vérifier la connexion avec un client VoIP.

Résultat : ✅ OK<hr>

Cas de test 2 : Établissement d’un appel
État initial : Deux utilisateurs configurés et enregistrés.

Fonctionnalité testée : Établissement d'un appel.

Comportement attendu : L'appel doit être fluide et sans latence.

Étapes :

Lancer les clients VoIP.

Composer le numéro d'un utilisateur.

Vérifier la qualité audio.

Résultat : ✅ OK<hr>

Cas de test 3 : Redémarrage du serveur
État initial : Serveur fonctionnel avec des utilisateurs enregistrés.

Fonctionnalité testée : Redémarrage du serveur.

Comportement attendu : Les utilisateurs doivent pouvoir se reconnecter après le redémarrage.

Étapes :

Redémarrer le serveur.

Vérifier la reconnexion des utilisateurs.

Résultat : ✅ OK<hr>

Cas de test 4 : Sécurisation des appels
État initial : Appel fonctionnel entre deux utilisateurs.

Fonctionnalité testée : Chiffrement des appels (SRTP, TLS).

Comportement attendu : Les appels doivent être chiffrés et non interceptables.

Étapes :

Configurer le chiffrement.

Vérifier via les logs ou un outil de capture réseau.

Résultat : ❌ NOK (À corriger)<hr>

📝 Conclusion
La VoIP est une technologie puissante et économique, en pleine expansion, qui transforme les communications modernes. Asterisk, en tant que solution open-source, offre une grande flexibilité pour les déploiements personnalisés. Les tests réalisés permettent de valider le bon fonctionnement du serveur VoIP avant sa mise en production.

Pour plus de détails, consultez les fichiers de configuration et les exemples fournis dans ce dépôt.

🌟 N'hésitez pas à contribuer ou à poser des questions !
🚀 Bonne exploration de la VoIP !

