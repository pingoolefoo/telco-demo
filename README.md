# telco-demo

- [telco-demo](#telco-demo)
  - [Contexte & Enjeux](#contexte--enjeux)
  - [Environnement technique](#environnement-technique)
  - [Structure des répertoires](#structure-des-r%c3%a9pertoires)
  - [Installation](#installation)
    - [Installation de Java](#installation-de-java)
    - [Installation d'elasticsearch](#installation-delasticsearch)
    - [Installation de kibana](#installation-de-kibana)
    - [Installation de logstash](#installation-de-logstash)
    - [Installation de filebeat](#installation-de-filebeat)
    - [Installation de Kafka](#installation-de-kafka)
    - [Installation de NiFi](#installation-de-nifi)
  - [Lancement](#lancement)
    - [Configuration & lancement de Kafka](#configuration--lancement-de-kafka)
    - [Lancement d'elasticsearch](#lancement-delasticsearch)
    - [Lancement de kibana](#lancement-de-kibana)
    - [Configuration & lancement de filebeat](#configuration--lancement-de-filebeat)
    - [Configuration & lancement de logstash](#configuration--lancement-de-logstash)
    - [Lancement de NiFi](#lancement-de-nifi)





## Contexte & Enjeux

Ce repository contient divers éléments utilisés dans le cadre d'un PoC. Les jeux de données contenu dans ce repository ont été générés aléatoirement et peuvent être publiés sur GitHub.

D'un point de vue technique, le pipeline de traitement est le suivant:
* Dépose des fichiers dans un répertoire
* Lecture & forward dans kafka du contenu de ces fichiers avec filebeat
* Parsing & forward des données dans elasticsearch avec logstash et/ou NiFi
* Stockage des données dans un cluster elasticsearch
* Affichage de divers indicateurs & dashboards dans kibana

Par ailleurs, les données générées ne sont pas suffisament nombreuses et ne sont pas suffisament corrélées pour pouvoir élaborer des dashboards avancés. L'objet de ce PoC se limite donc à l'affichage de quelques valeurs et à suivre leur évolution dans le temps.





## Environnement technique

| Produit       | Version | Lien de Download                                   |
| :------------ | :-----: | :------------------------------------------------- |
| Windows       | 7/8/10  | N/A                                                |
| Java          | 12.0.2  | https://www.oracle.com/technetwork/java/index.html |
| Apache Kafka  |  2.3.0  | https://kafka.apache.org/downloads                 |
| Apache Nifi   |  1.9.2  | https://nifi.apache.org/download.html              |
| filebeat      |  7.2.0  | https://www.elastic.co/fr/downloads/beats/filebeat |
| logstash      |  7.2.0  | https://www.elastic.co/fr/downloads/logstash       |
| elasticsearch |  7.2.0  | https://www.elastic.co/fr/downloads/elasticsearch  |
| kibana        |  7.2.0  | https://www.elastic.co/fr/downloads/kibana         |

Pour faciliter l'utilisation de Kafka, il est possible de recourir à [Kafka Tools](http://www.kafkatool.com/).





## Structure des répertoires

| Répertoire                 | Utilité                                                           |
| :------------------------- | :---------------------------------------------------------------- |
| C:\PoC-telco               | Répertoire de base                                                |
| C:\PoC-telco\repository    | Répertoire contenant l'ensemble des archives téléchargés ci-avant |
| C:\PoC-telco\samples       | Répertoire de base pour l'ensemble des exemples de données        |
| C:\PoC-telco\samples\air   | Exemples de données AIR                                           |
| C:\PoC-telco\samples\ccn   | Exemples de données CCN                                           |
| C:\PoC-telco\elasticsearch | Répertoire d'installation d'elasticsearch                         |
| C:\PoC-telco\kibana        | Répertoire d'installation de kibana                               |
| C:\PoC-telco\logstash      | Répertoire d'installation de logstash                             |
| C:\PoC-telco\filebeat      | Répertoire d'installation de filebeat                             |
| C:\PoC-telco\kafka         | Répertoire d'installation de kafka                                |
| C:\PoC-telco\nifi          | Répertoire d'installation de NiFi                                 |





## Installation

### Installation de Java

* Télécharger & Installer le JDK 12.0.2 (ou supérieur) à l'aide de l'installateur fourni par Oracle
* Définir la variable d'environnement globale JAVA_HOME afin qu'elle pointe sur l'installation du JDK (typiquement: C:\Program Files\Java\jdk-12.0.2 )
* Modifier le Path afin de rajouter %JAVA_HOME%\bin
* Lancer une fenêtre "Invite de commandes" et vérifier que `java -version` indique bien `java version "12.0.2" 2019-07-16`

### Installation d'elasticsearch

* Télécharger elasticsearch et déplacer l'archive dans `C:\PoC-telco\repository `
* Décompresser elasticsearch et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire d'elasticsearch en `elasticsearch`, de sorte à avoir un répertoire `C:\PoC-telco\elasticsearch`
* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\elasticsearch `
* Lancer la commande `bin\elasticsearch` et vérifier qu'elasticsearch se lance bien
* Arrêter elasticsearch à l'aide des touches `Ctrl + C`

### Installation de kibana

* Télécharger kibana et déplacer l'archive dans `C:\PoC-telco\repository `
* Décompresser kibana et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de kibana en `kibana`, de sorte à avoir un répertoire `C:\PoC-telco\kibana`

### Installation de logstash

* Télécharger logstash et déplacer l'archive dans `C:\PoC-telco\repository `
* Décompresser logstash et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de logstash en `logstash`, de sorte à avoir un répertoire `C:\PoC-telco\logstash`

### Installation de filebeat

* Télécharger filebeat et déplacer l'archive dans `C:\PoC-telco\repository `
* Décompresser filebeat et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de filebeat en `filebeat`, de sorte à avoir un répertoire `C:\PoC-telco\filebeat`

### Installation de Kafka

* Télécharger kafka et déplacer l'archive dans `C:\PoC-telco\repository `
* Décompresser kafka et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de kafka en `kafka`, de sorte à avoir un répertoire `C:\PoC-telco\kafka`

### Installation de NiFi

* Télécharger NiFi et déplacer l'archive dans `C:\PoC-telco\repository `
* Décompresser NiFi et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de NiFi en `nifi`, de sorte à avoir un répertoire `C:\PoC-telco\nifi`





## Lancement

### Configuration & lancement de Kafka

TODO

### Lancement d'elasticsearch

Dans le cadre de ce PoC elasticsearch utilise une configuration par défaut. 

### Lancement de kibana

TODO

### Configuration & lancement de filebeat

TODO

### Configuration & lancement de logstash

TODO

### Lancement de NiFi

TODO

