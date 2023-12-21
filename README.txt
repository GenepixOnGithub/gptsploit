# GPTsploit: Connexion d'un GPT personnalisé à Kali Linux

## Aperçu
GPTsploit est un outil de pentesting qui se connecte à Kali Linux via un serveur Flask. Il permet l'envoi de lignes de commande et l'interprétation des réponses, offrant une interface de type chat GPT entre l'utilisateur et Linux.

## Fonctionnalités
- Interactions : Dialoguez avec GPTsploit pour élaborer un scénario d'attaque et lui demander de l'exécuter.
- Interprétation des résultats : Les résultats sont récupérés et analysés par GPT.
- Utilisation pratique : Idéal pour des démonstrations techniques et l'apprentissage du pentesting.

## Public Cible
Cet outil est destiné aux utilisateurs possédant des connaissances en pentesting et en Kali Linux, et disposant d'un compte Chat GPT Plus. GPTsploit est particulièrement adapté aux professionnels et aux éducateurs en cybersécurité.

## Installation

### Installation de ngrok
1. ngrok permet d'exposer votre serveur gptsploit.py sur Internet.
2. Suivez la ligne de commande fournie par le site.
3. Téléchargez et installez ngrok : Guide d'installation pour Linux
4. Authentifiez ngrok : Page d'authentification
5. Créez un compte gratuit sur www.ngrok.com.
6. Création du endpoint sur le site de ngrok :
   - Accédez à l'onglet Cloud Edge > Domains > Create domain.
   - Exécutez la commande : \`ngrok http --domain=votre_domaine.ngrok-free.app 5000\` (ajustez le port si nécessaire).

### Installation des dépendances
```
pip install Flask==3.0.0 pyfiglet==1.0.2 termcolor==2.4.0
```

### Configuration du serveur gptsploit.py
Modifiez la clé d'API : \`API_KEY = os.environ.get("API_KEY", "VOTRE_MOT_DE_PASSE")\`

### Lancement de GPTsploit
```
sudo python gptsploit.py
```

### Test du serveur avec curl
Dans une nouvelle console, lancez :
```
curl -X POST https://[votre_domaine].app/execute \
     -H "Content-Type: application/json" \
     -H "X-API-KEY: votre_api_key" \
     -d '{"command": "ifconfig > [log_path]"}'
```
Si l'exécution est réussie, gptsploit.py doit afficher des informations similaires à :
```
127.0.0.1 - - [19/Dec/2023 20:19:41] "POST /execute HTTP/1.1" 202 -
Exécution de la commande : ifconfig > logs/log_20231219_202109.txt
```
et le résultat de ifconfig doit apparaître dans la console de curl.

## Configuration de votre GPT sur l'interface web de Chat GPT Plus
1. Accédez à https://chat.openai.com.
2. Créez un GPT et nommez-le selon votre préférence.

## Instructions
Copiez et collez les informations suivantes dans la section "instructions". Vous pouvez les modifier selon vos besoins ou le style souhaité pour votre GPT :
```
"Ce GPT fournit des réponses courtes, sauf indication contraire.

GPTsploit est conçu pour interagir avec une console Kali Linux via un serveur Flask. Il envoie des commandes, reçoit et interprète les réponses. Cette documentation explique comment GPTsploit doit formuler et envoyer des commandes pour une exécution efficace.

Communication avec le Serveur Flask :

Format des Commandes :
Utilisez la syntaxe exacte nécessaire pour une console Kali Linux.

Envoi des Commandes :
Les commandes sont envoyées via une requête POST à l'endpoint /execute du serveur Flask.
Format de la requête : JSON avec un champ command contenant la commande à exécuter.

À FAIRE DE MANIÈRE SYSTÉMATIQUE :
Incluez [log_path] à l'endroit où le fichier de log doit être créé.
[log_path] sera remplacé par le
