RFID.hack
=========

Hacking the NFC credit cards for fun and debit par Renaud Lifchitz
==================================================================

#Hackito Ergo Sum 2012 [13/04/2012] 10h-11h


Renaud commence par pr�senter ses activit�s au sein de BT et le principe du paiement sans contact (NFC). En France 100 000 terminaux sont d�j� compatibles et 10 millions de cartes sont compatibles aux USA. Il existe deux syst�mes un par Visa et un pour MasterCard. Le paiement est pour le moment limit� � 4 paiements de maximum 20�. Les cartes NFS compatibles ont un logo de signal radio comme le wifi. Dans l�assembl�e seule une personne a une carte NFC, sans doute que certains n�ont pas pr�f�r� le dire :) . Le but du paiement sans fil est cens� simplifi� l�utilisation du moyen de paiement et au Canada les statistiques montrent que les gens consomment plus facilement.

Le stockage et la s�curit� est assur� par le standard EMV et la norme ISO 7816-4. La carte a un vrai filesystem avec un root directory et des r�pertoires / fichiers. Les donn�es sont encod�es en BER TLV. Renaud analyse les donn�es pr�sentes dans une requ�te de paiement sans contact. On retrouve une class, une instruction, deux param�tres, la longueur des donn�es, les donn�es et la longueur de la r�ponse esp�r�e. A pr�sent un parall�le est fait avec le pass Navigo, le ticket sans contact des transports parisien. La s�curit� est bonne car aucune donn�e personnelle n�est pr�sente, aucun lien ne peut �tre fait entre une personne et sa carte sauf par les serveurs centraux. La carte poss�de un bon cryptage, une bonne authentification et une signature digitale.

Renaud Lifchitz at Hackito Ergo Sum 2012

Les cartes de paiement sans contact sont au contraire du pass navigo, aucun cryptage des donn�es, aucune authentification, tout est ouvert. Le NFC regroupe le RFID, le NFC et le Cityzi, les fr�quences sont en HF � 13,56Mhz et en LF entre 125 et 134 Khz. On trouve des lecteurs usb et des t�l�phones capables de lire les NFC. Pour les outils utiles scriptor pour le prototype, libnfc et pn53x-tamashell pour la partie NFC et quelques scripts persos sont n�cessaires.

Les donn�es que l�on peut extraire sont les donn�es du propri�taire : sexe, nom, pr�nom, votre num�ro de compte PAN, votre date d�expiration, les donn�es de la bande magn�tique, l�historique de vos transactions. Potentiellement d�autres donn�es restent � d�couvrir comme les clefs publiques. Par contre le num�ro de la carte CVV n�est pas inscrit dans les donn�es NFC, on ne peut donc pas le r�cup�rer.

Les attaques possibles, sont le fait de r�cup�rer les donn�es et de les utiliser pour des paiements en ligne. On peut aussi bloquer une carte bleue en envoyant trois requ�tes de code pin erron�s et ainsi bloquer tout paiement avec cette carte. On peut aussi tenter la duplication de la carte, les donn�es NFC sont presques compl�tes et les donn�es de la piste magn�tique peuvent �tre reproduites. Une telle carte clon�e pourra �tre utilis� dans les pays ne demandant pas le code pin comme les USA et certains pays europ�ens par exemple. Enfin on peut reconna�tre la pr�sence d�une personne et d�clencher des actions : surveillance des passages, terrorisme avec une voiture qui explose uniquement si la personne vis�e est pr�sente.

Renaud aborde la m�thode pour faire une attaque avec la libnfc. On envoie une s�quence d�initialisation, il faut apr�s retrouver le code AID de l�application de la banque, ce num�ro se trouve sur tous les tickets de re�u de carte bleue et n�est pas tronqu�. Enfin il faut lire la r�ponse EMV de la carte. Renaud nous pr�sente les code AID des diff�rents types de paiement visa, mastercard, american express, �

Renaud Lifchitz lecture des informations NFC carte bleue sans contact

Une d�monstration est faite avec sa carte bleue dans son porte feuille qu�il approche du lecteur. Instannn�ment toutes les donn�es se trouvant dans sa carte sont apparues. On y voit son num�ro de carte bleue, sa date d�expiration, son identit� et l�historique de ses achats. Une deuxi�me d�monstration est faite sur un syst�me Android, les m�mes donn�es apparaissent. On imagine ais�ment les cons�quences de scan avec un t�l�phone dans un m�tro bond�.

A pr�sent nous voyons les limites des attaques. La principale contrainte est la distance entre 3 et 5 cm est la distance id�ale. Mais en utilisant des amplificateurs on peut monter � 1,5m. Avec un r�cepteur type USRP avec une antenne directive on peut monter � 15m. Il rappel que des hackers avaient r�ussi en 2004 � monter la distance op�rationnelle du bluetooth de 10m � 1,7km. La seule protection possible est un porte feuille anti RFID capable de bloquer les ondes radios comme une cage de Faraday. Renaud fait � pr�sent les recommendations de ce que devrait �tre la s�curit� sur les cartes NFC. Authentification, cryptage des communications, les sessions doivent �tre s�curis�es. Aussi pour lui le syst�me doit �tre enti�rement revu et ne pas �tre utilis�. Le paiement NFC n�est pas compatible avec les recommandations PCI DSS alors que ces derniers sont � l�origine du paiement NFC. Aussi c�est un grand �chec de la politique de s�curit� et de lutte contre la fraude des paiements au niveau internationale. En France le fait de ne pas prot�ger des donn�es personnelles est un acte criminel, la CNIL est d�j� pr�te � demander des actions concr�tes, aussi l�utilisation de cartes NFC en France semble incompatible.

Renaud termine sur le fait qu�il n�a pas eu besoin de faire de reverse engineering puisque le protocole est public, qu�il n�est entr� dans aucun syst�me et n�a cass� aucune s�curit� puisqu�il n�y en a simplement aucune.