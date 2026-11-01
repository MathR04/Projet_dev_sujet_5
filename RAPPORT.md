# Rapport de projet : Le forum entreprises

Ce rapport a pour but de récapituler le besoin initial, les solutions retenues ainsi que celles écartées. 

## Les besoins de Léo

Léo, qui préside le forum entreprise, avait une demande initiale simple : 
> Hello, Léo, je préside le forum entreprises de l'école. Chaque année, une trentaine d'entreprises viennent rencontrer les élèves. Résultat : des queues devant les stands connus, et des recruteurs qui s'ennuient devant les autres. On peut faire mieux.

Léo ici nous fait part du résultat qui ne lui convient pas, mais il nous fallait encore comprendre son réel besoin.
Après une petite série de questions (https://github.com/gaetanmaisse/ismin-web-2026-tps/discussions/16) pour cibler le besoin réel et éclairer les zones d'ombres où les points flous, nous avons pu conclure sur ceci : 
### Une solution qui permet à toutes les entreprises d'avoir de la visite lors du forum

Ce que nous avons donc mis en place : 
- Des comptes élèves, recruteur et équipe du forum avec des accès et des vues différents.
- Le catalogue des entreprises visible sans compte.
- Les rendez-vous, avec la priorité pour les étudiants en 2e et 3e années
- le CV visible seulement par les entreprises avec qui l'élève a un RDV
- le planning du recruteur pour savoir quel élève il doit rencontrer et à quel créneau
- le suivi des stands vides par l'équipe
- les comptes recruteurs créés par l'équipe

Notons que cette mise en place découle aussi des questions posées à Léo qui nous ont permis de changer certaines idées, notamment l'idée d'une file d'attente. Pour citer la discussion:
> Qu'attendez-vous concrètement de la solution pour améliorer la situation ? Faut-il par exemple gérer des rendez-vous, des créneaux ou des files d'attente virtuelles ?

>[...]Une file d'attente virtuelle, j'y crois moins : elle raccourcit la queue devant le grand groupe, mais elle n'envoie personne vers les PME.

On peut résumer cela en l'implémentation de 3 fonctionnalités majeures : 
1. La consultation du catalogue des entreprises
2. Les rendez-vous avec le CV
3. Le jour J: le planning du recruteur et le tableau de bord

La partie véritablement notable qui sort des TPs est celle sur les CV, qui fait appelle à l'upload de fichiers. 

