# telco-demo

Ce repository contient divers éléments utilisés pour réaliser un PoC sur le parsing de fichiers spécifiques pour le compte d'un client institutionnel. L'intégralité des jeux de données utilisés ici ont été générées aléatoirement par le client de ce PoC et peuvent être publiés sans risques sur GitHub. Les données présentes dans ce repository ont donc été postées avec l'accord préalable de ce client.

D'un point de vue technique, le pipeline de traitement est le suivant:
1. Dépose des fichiers dans un répertoire spécifique avec un pattern spécifique par un tiers
2. Lecture des fichiers avec un agent de collecte filebeat et forward des données lues dans un topic Kafka
3. Parsing des données contenues dans les divers topics Kafka à l'aide de Logstash et envoi des données parsées dans un cluster elasticsearch mono-noeud
4. Affichage d'indicateurs calculés dans kibana

Par ailleurs, il convient de noter les données fournies ne sont pas suffisamment nombreuses pour pouvoir élaborer des dashboards avancés. L'objet de ce PoC se limite donc à l'affichage de quelques valeurs et à suivre leur évolution dans le temps.

## Prérequis Techniques



