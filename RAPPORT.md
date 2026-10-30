# Rapport de projet : Le forum entreprises

Ce rapport a pour but de récapituler le besoin initial, les solutions retenues ainsi que celles écartées. 

## Les besoins de Léo

Léo, qui préside le forum entreprise, avait une demande initiale simple : 
> Hello, Léo, je préside le forum entreprises de l'école. Chaque année, une trentaine d'entreprises viennent rencontrer les élèves. Résultat : des queues devant les stands connus, et des recruteurs qui s'ennuient devant les autres. On peut faire mieux.


Après une petite série de questions pour cibler le besoin réel et éclairer les zones d'ombres où les points flous, nous avons pu conclure sur ceci : 
### Une solution qui permet à toutes les entreprises d'avoir de la visite lors du forum

Ce que nous avons donc mis en place : 
- Des comptes élèves, entreprise et admin avec des accès et des vues différents.
- Le catalogue des entreprise visible sans compte.
- Les rendez-vous, avec la priorité pour les étudiants en 2e et 3e années
- le CV visible seulement par les entreprises avec qui l'élève a un RDV
- le planning du recruteur pour savoir quel élève il doit rencontrer et à quel créneau
- le suivi des stands vides par l'équipe
- les comptes recruteurs créés par l'équipe


On peut résumer cela en l'implémentation de 3 fonctionnalités majeures : 
1. La consultation de la liste des entreprises
2. Les rendez-vous (incluant la fonctionnalité annexe des plannings)
3. Les CV

La partie véritablement notable et novatrice est celle sur les CV, qui fait appelle à de la lecture de fichiers. 

