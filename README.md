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
    - [Fichiers d'exemple](#fichiers-dexemple)
  - [Configuration & lancement de Kafka](#configuration--lancement-de-kafka)
    - [Configuration](#configuration)
      - [ZooKeeper](#zookeeper)
      - [Kafka](#kafka)
      - [Fichiers](#fichiers)
    - [Lancement de ZooKeeper](#lancement-de-zookeeper)
    - [Lancement de Kafka](#lancement-de-kafka)
    - [Vérification](#v%c3%a9rification)
  - [Lancement & configuration d'elasticsearch & kibana](#lancement--configuration-delasticsearch--kibana)
    - [Configuration d'elasticsearch](#configuration-delasticsearch)
    - [Lancement d'elasticsearch](#lancement-delasticsearch)
    - [Configuration de kibana](#configuration-de-kibana)
    - [Lancement de kibana](#lancement-de-kibana)
    - [Configuration du sharding](#configuration-du-sharding)
    - [Configuration du template d'index](#configuration-du-template-dindex)
  - [Configuration & lancement de filebeat](#configuration--lancement-de-filebeat)
  - [Configuration & lancement de logstash](#configuration--lancement-de-logstash)
    - [Remarques](#remarques)
    - [Configuration](#configuration-1)
    - [Lancement du pipeline AIR](#lancement-du-pipeline-air)
    - [Lancement du pipeline CCN](#lancement-du-pipeline-ccn)





## Contexte & Enjeux

Ce repository contient divers éléments utilisés dans le cadre d'un PoC. Les jeux de données contenu dans ce repository ont été générés aléatoirement et peuvent être publiés sur GitHub.

D'un point de vue technique, le pipeline de traitement est le suivant:
* Dépose des fichiers dans un répertoire
* Lecture & forward dans kafka du contenu de ces fichiers avec filebeat
* Parsing & forward des données dans elasticsearch avec logstash
* Stockage des données dans un cluster elasticsearch
* Affichage de divers indicateurs & dashboards dans kibana

Par ailleurs, les données générées ne sont pas suffisament nombreuses et ne sont pas suffisament corrélées pour pouvoir élaborer des dashboards avancés. L'objet de ce PoC se limite donc à l'affichage de quelques valeurs et à suivre leur évolution dans le temps.





## Environnement technique

| Produit       | Version | Lien de Download                                   |
| :------------ | :-----: | :------------------------------------------------- |
| Windows       | 7/8/10  | N/A                                                |
| Java          | 12.0.2  | https://www.oracle.com/technetwork/java/index.html |
| Apache Kafka  |  2.3.0  | https://kafka.apache.org/downloads                 |
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
* Se placer dans le répertoire `C:\PoC-telco\elasticsearch`
* Lancer la commande `bin\elasticsearch` et vérifier qu'elasticsearch se lance bien
* Arrêter elasticsearch à l'aide des touches `Ctrl + C`

### Installation de kibana

* Télécharger kibana et déplacer l'archive dans `C:\PoC-telco\repository`
* Décompresser kibana et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de kibana en `kibana`, de sorte à avoir un répertoire `C:\PoC-telco\kibana`

### Installation de logstash

* Télécharger logstash et déplacer l'archive dans `C:\PoC-telco\repository`
* Décompresser logstash et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de logstash en `logstash`, de sorte à avoir un répertoire `C:\PoC-telco\logstash`

### Installation de filebeat

* Télécharger filebeat et déplacer l'archive dans `C:\PoC-telco\repository`
* Décompresser filebeat et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de filebeat en `filebeat`, de sorte à avoir un répertoire `C:\PoC-telco\filebeat`

### Installation de Kafka

* Télécharger kafka et déplacer l'archive dans `C:\PoC-telco\repository`
* Décompresser kafka et déplacer le répertoire vers `C:\PoC-telco`
* Renommer le répertoire de kafka en `kafka`, de sorte à avoir un répertoire `C:\PoC-telco\kafka`
* Télécharger & installer kafka-tools à l'aide de l'installateur fourni

### Fichiers d'exemple

* Télécharger le fichier `AIR_POC_random_31052019.txt` ([ici](https://github.com/pingoolefoo/telco-demo/blob/master/samples/AIR/AIR_POC_random_31052019.txt)) et le copier dans le répertoire `C:\PoC-telco\samples\AIR`
* Télécharger le fichier `VOICE_MA_CCN_M_98.dat` ([ici](https://github.com/pingoolefoo/telco-demo/blob/master/samples/CCN/VOICE_MA_CCN_M_98.dat)) et le copier dans le répertoire `C:\PoC-telco\samples\CCN`





## Configuration & lancement de Kafka

### Configuration

#### ZooKeeper

* Se placer dans le répertoire `C:\PoC-telco\kafka\config`
* Editer le fichier `zookeeper.properties` et modifier la propriété `dataDir` de sorte à avoir `dataDir=C:\\PoC-telco\\kafka\\data\\zookeeper`

#### Kafka

* Se placer dans le répertoire `C:\PoC-telco\kafka\config`
* Editer le fichier `server.properties` et modifier les propriétés suivantes:
  * `log.retention.hours` de sorte à avoir `log.retention.hours=744` (soit 1 mois)
  * `log.dirs` de sorte à avoir `log.dirs=C:\\PoC-telco\\kafka\\data\\kafka`

#### Fichiers

| Fichier                | Url de téléchargement                                                                          |
| :--------------------- | :--------------------------------------------------------------------------------------------- |
| `zookeeper.properties` | https://github.com/pingoolefoo/telco-demo/blob/master/configuration/kafka/zookeeper.properties |
| `server.properties`    | https://github.com/pingoolefoo/telco-demo/blob/master/configuration/kafka/server.properties    |

### Lancement de ZooKeeper

* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\kafka`
* Lancer la commande `bin\windows\zookeeper-server-start.bat config\zookeeper.properties`

### Lancement de Kafka

* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\kafka`
* Lancer la commande `bin\windows\kafka-server-start.bat config\server.properties`

### Vérification

* Lancer Kafka-Tool et configurer le nom du cluster puis tester la connexion





## Lancement & configuration d'elasticsearch & kibana

### Configuration d'elasticsearch

* Aucune configuration spécifique n'est utilisée dans le cadre de ce PoC
* Le sharding et les templates d'index seront configurés ultérieurement

### Lancement d'elasticsearch

* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\elasticsearch`
* Lancer la commande `bin\elasticsearch`
* Ouvrir un navigateur web et se rendre à l'adresse http://localhost:9200 et vérifier qu'un document json indiquant le nom du cluster, sa version et quelques autres informations est bien affiché

### Configuration de kibana

* Aucune configuration spécifique n'est utilisée dans le cadre de ce PoC

### Lancement de kibana

* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\kibana`
* Lancer la commande `bin\kibana.bat` (attendre que le lancement de kibana se termine)
* Ouvrir un navigateur web et se rendre à l'adresse http://localhost:5601

### Configuration du sharding

* Ouvrir la console de développement de kibana disponible à l'adresse http://localhost:5601/app/kibana#/dev_tools/console?_g=()
* Copier/Coller puis exécuter la commande suivante 
  ```
  PUT _template/default-sharding
  {
      "index_patterns": ["*"] ,
      "order": 0,
      "settings": {
          "number_of_shards": 1,
          "number_of_replicas": 0
      }
  }
  ```

### Configuration du template d'index

* Ouvrir la console de développement de kibana disponible à l'adresse http://localhost:5601/app/kibana#/dev_tools/console?_g=()
* Copier/Coller puis exécuter la commande suivante 
  ```
  pas utilisé pour le moment, mais constitue une bonne pratique dans l'absolu
  ```





## Configuration & lancement de filebeat

* Télécharger le fichier `filebeat.yml` ([ici](https://github.com/pingoolefoo/telco-demo/blob/master/configuration/filebeat/filebeat.yml))
* Ecraser le fichier `C:\PoC-telco\filebeat\filebeat.yml` par celui qui vient d'être téléchargé
* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\filebeat`
* Lancer la commande `filebeat.exe`
* Vérifier à l'aide de Kafka-Tools que les topics `air-data` et `ccn-data` ont bien été crées





## Configuration & lancement de logstash

### Remarques

* Il est possible de centraliser la configuration des pipelines logstash dans elastic à condition d'avoir une licence
* Sur ce PoC, nous avons choisi de nous limiter à des fonctionnalités ne nécessitant pas de licence
* Par ailleurs, dans le cadre de ce PoC 
  * les pipelines logstash sont stockés dans `C:\PoC-telco\logstash\config\pipelines` 
  * les pipelines air & ccn seront lancés séparéments
  * les capacités de lancement simultané de plusieurs pipelines par logstash ne seront pas exploitées

### Configuration

* Dans le répertoire `C:\PoC-telco\logstash\config` créer un nouveau répertoire `pipelines`
* Dans le répertoire `C:\PoC-telco\logstash\config\pipelines`  créer un nouveau répertoire `pipeline-air`
* Dans le répertoire `C:\PoC-telco\logstash\config\pipelines`  créer un nouveau répertoire `pipeline-ccn`
* Copier les fichier se trouvant [ici] (https://github.com/pingoolefoo/telco-demo/tree/master/configuration/logstash/pipeline-air) dans `C:\PoC-telco\logstash\config\pipelines\pipeline-air`
* Copier les fichier se trouvant [ici] (https://github.com/pingoolefoo/telco-demo/tree/master/configuration/logstash/pipeline-ccn) dans `C:\PoC-telco\logstash\config\pipelines\pipeline-ccn`

### Lancement du pipeline AIR

* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\logstash`
* Lancer la commande `bin\logstash -f config\pipelines\pipeline-air`
* Attendre quelques minutes que logstash se lance et traite l'ensemble des données puis arrêter logstash à l'aide des touches `Ctrl + C`

### Lancement du pipeline CCN

* Ouvrir une fenêtre "Invite de commandes"
* Se placer dans le répertoire `C:\PoC-telco\logstash`
* Lancer la commande `bin\logstash -f config\pipelines\pipeline-ccn`
* Attendre quelques minutes que logstash se lance et traite l'ensemble des données puis arrêter logstash à l'aide des touches `Ctrl + C`
