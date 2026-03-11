-----------------------------------------------------------------------------------------------------
🎯Comprendre les bases du réseau (OSI, DHCP, NAT)
------------------------------------------------------------------------------------------------------
Cet atelier propose une exploration pratique des fondamentaux des réseaux informatiques à travers trois mécanismes essentiels : le modèle OSI, le protocole DHCP et la traduction d’adresses NAT.  
  
L’objectif est de visualiser concrètement le fonctionnement du réseau, depuis la structure des communications jusqu’à l’attribution des adresses IP et la communication avec Internet. Dans un premier temps, nous allons découvrir le modèle OSI (Open Systems Interconnection) et son rôle comme cadre conceptuel pour organiser les communications réseau en 7 couches. Ensuite, notre atelier reviendra sur le protocole DHCP, qui permet d’attribuer automatiquement une configuration réseau (adresse IP, passerelle, DNS). Et enfin, l’atelier abordera le NAT (Network Address Translation), un mécanisme clé permettant à plusieurs machines d’un réseau privé de partager une même adresse IP publique pour accéder à Internet.  
  
**Notre atelier**  

![Screenshot Actions](Architecture_cible_Reseau.png)  

-------------------------------------------------------------------------------------------------------
🧩 Séquence 1 : GitHUB
-------------------------------------------------------------------------------------------------------
Objectif : Création d'un Repository GitHUB pour travailler avec son projet  
Difficulté : Très facile (~10 minutes)
-------------------------------------------------------------------------------------------------------
**Faites un Fork de ce projet**. Si besoin, voici une vidéo d'accompagnement pour vous aider à "Forker" un Repository Github : [Forker ce projet](https://youtu.be/p33-7XQ29zQ)  

---------------------------------------------------
🧩 Séquence 2 : Création d'un site chez Pythonanywhere
---------------------------------------------------
Objectif : Créer un hébergement sur Pythonanywhere  
Difficulté : Faible (~10 minutes)
---------------------------------------------------

Rendez-vous sur **https://www.pythonanywhere.com/** et créez vous un compte. Puis créez un serveur Web **Flask 3.15**.  
  
---------------------------------------------------------------------------------------------
🧩 Séquence 3 : Les Actions GitHUB (Industrialisation Continue)
---------------------------------------------------------------------------------------------
Objectif : Automatiser la mise à jour de votre hébergement Pythonanywhere  
Difficulté : Moyenne (~15 minutes)
---------------------------------------------------------------------------------------------
Dans le Repository GitHUB que vous venez de créer précédemment lors de la séquence 1, vous avez un fichier intitulé deploy-pythonanywhere.yml et qui est déposé dans le répertoire .github/workflows. Ce fichier a pour objectif d'automatiser le déploiement de votre code sur votre site Pythonanywhere. Pour information, c'est ce que l'on appel des Actions GitHUB. Ce sont des scripts qui s'exécutent automatiquement lors de chaque Commit dans votre projet (C'est à dire à chaque modification de votre code). Ces scripts (appelés actions) sont au format yml qui est un format structuré proche de celui d'XML.  

Pour utiliser cette Action (deploy-pythonanywhere.yml), **vous avez besoin de créer des secrets dans GitHUB** afin de ne pas divulguer des informations sensibles aux internautes de passage dans votre Repository comme vos login et password par exemple.  

Pour cet atelier, **vous avez 4 secrets à créer** dans votre Repository GitHUB : **Settings → Secrets and variables → Actions → New repository secret**  
  
**PA_USERNAME** = votre username PythonAnywhere.  
**PA_TOKEN** = votre API token. Token à créer dans pythonanywhere (Acount → API Token).  
**PA_TARGET_DIR** = Web → Source code (ex: /home/monuser/myapp).  
**PA_WEBAPP_DOMAIN** = votre site (ex: monuser.pythonanywhere.com).  
  
**Dernière étape :** Pour engager l'automatisation de votre première Action, vous devez cliquer sur le gros boutton vert dans l'onglet supérieur [Actions] dans votre Repository Github. Le boutton s'intitule "I understand my workflows, go ahead and enable them"   

Notions acquises de cette séquence :  
Vous avez vu dans cette séquence comment créer des secrets GiHUB afin de mettre en place de l'industrialisation continue.   

---------------------------------------------------
🗺️ Séquence 4 : OSI (Open Systems Interconnection)
---------------------------------------------------
Vous pouvez observez les différentes couches OSI sur votre site **{site}.pythonanywhere.com/osi**  
  
**Exercice 1 : Définissez les termes suivants (Répondre directement dans GitHub)**  

* Un protocole : C’est le "règlement" d'une couche. Il définit comment deux machines se parlent pour que le service fonctionne. Un protocole de niveau N précise le format des messages et l'ordre des échanges (qui parle en premier, que faire en cas d'erreur).
  
  Exemple : Le protocole HTTP définit qu'un client doit envoyer "GET" pour recevoir une page web.
  
* Une entité protocolaire : C’est le programme ou le composant qui exécute les règles du protocole. On l'appelle souvent "automate" car elle réagit selon des états précis.

  Exemple : Ton navigateur (Chrome) est une entité de couche 7. Il communique avec l'entité homologue (le serveur Web de PythonAnywhere)
  
* Un service : C’est la fonctionnalité qu'une couche offre à celle juste au-dessus d'elle. Le service dit ce que fait la couche, mais pas comment elle le fait techniquement.

  Exemple : La couche Liaison (Couche 2) offre un service de "transfert de trames" à la couche Réseau, peu importe que la connexion soit en Wi-Fi ou en Ethernet.

* Une primitive de service :C’est l'interaction standardisée pour demander ou recevoir un service entre deux couches sur la même machine. Il en existe 4 types principaux :

  4 types :
  - REQ (Request) : La couche supérieure demande un service.
  - IND (Indication) : La couche inférieure signale un événement ou une demande d'en face.
  - RESP (Response) : La couche supérieure répond à l'indication.
  - CONF (Confirmation) : La couche inférieure confirme que la requête initiale est terminée.
  
* Une Service Data Unit (SDU) par rapport à une PDU / Ces termes décrivent l'évolution de la donnée lors de l'encapsulation :

  - SDU : C'est la donnée "pure" transmise par la couche supérieure. Pour la couche actuelle, c'est la "marchandise" à transporter.

  - PDU : C'est l'unité complète produite par la couche. Elle contient la SDU à laquelle on a ajouté un en-tête (PCI) contenant les adresses ou numéros de ports.

  Exemple : Ton adresse IP client 10.0.5.156 est ajoutée dans l'en-tête de la PDU de couche 3 (le Paquet IP) pour encapsuler la SDU venant de la couche Transport.
  
* Un point d'accès à un service SAP (Service Access Point) : C'est l'interface logique (ou l'adresse) qui permet à une couche d'accéder aux services de la couche située juste en dessous.

  Exemple :Le Port TCP ou l'adresse IP (10.0.5.156) servent de SAP pour diriger les données vers la bonne application.

---------------------------------------------------
🗺️ Séquence 5 : Retour sur le protocole DHCP
---------------------------------------------------
Vous pouvez observez le protocole DHCP sur votre site **{site}.pythonanywhere.com/dhcp**  
  
**Exercice 2 : Créer une image montrant l’encapsulation des couches suivantes**  

Encapsulation du protocole DHCP dans le modèle OSI

<img width="547" height="345" alt="image" src="https://github.com/user-attachments/assets/9276516c-7282-424e-ba1a-20b0d8f0bf4e" />


Ce schéma illustre comment le protocole DHCP utilise les couches du modèle OSI pour fonctionner. Le message DHCP est généré en couche Application (7), encapsulé dans un segment UDP en couche Transport (4), puis dans un paquet IP en couche Réseau (3). Chaque couche ajoute ses propres informations pour permettre l'acheminement du message sur le réseau.  

--------------------------------------------------------------------
🧠 Troubleshooting :
---------------------------------------------------
Objectif : Visualiser ses logs et découvrir ses erreurs
---------------------------------------------------
Lors de vos développements, vous serez peut-être confronté à des erreurs systèmes car vous avez faits des erreurs de syntaxes dans votre code, faits de mauvaises déclarations de fonctions, appelez des modules inexistants, mal renseigner vos secrets, etc…  
Les causes d'erreurs sont quasi illimitées. **Vous devez donc vous tourner vers les logs de votre système pour comprendre d'où vient le problème** :  

Vos log sont accéssible via les URL suivantes :  
* Access log : {site}.pythonanywhere.com.access.log
* Error log : {site}.pythonanywhere.com.error.log
* Server log: {site}.pythonanywhere.com.server.log
