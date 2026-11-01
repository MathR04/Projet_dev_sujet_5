# Rapport de projet : Le forum entreprises

Ce rapport a pour but de récapituler le besoin initial, les solutions retenues ainsi que celles écartées. 

## Les besoins de Léo

Léo, qui préside le forum entreprise, avait une demande initiale simple : 
> Hello, Léo, je préside le forum entreprises de l'école. Chaque année, une trentaine d'entreprises viennent rencontrer les élèves. Résultat : des queues devant les stands connus, et des recruteurs qui s'ennuient devant les autres. On peut faire mieux.

Léo ici nous fait part du résultat qui ne lui convient pas, mais il nous fallait encore comprendre son réel besoin.
Après une petite série de questions (https://github.com/gaetanmaisse/ismin-web-2026-tps/discussions/16) pour cibler le besoin réel et éclairer les zones d'ombres où les points flous, nous avons pu conclure sur ceci : 
### Une solution qui permet à toutes les entreprises d'avoir de la visite lors du forum

Ce que nous avons donc mis en place : 
- Des comptes élèves, recruteur et équipe du forum avec des accès et des vues différents. (api/src/auth/roles.ts:10)
- Le catalogue des entreprises visible sans compte. (api/src/companies/companies.controller.ts:28)
- Les rendez-vous, avec la priorité pour les étudiants en 2e et 3e années (api/src/bookings/bookings.service.ts:35)
- le CV visible seulement par les entreprises avec qui l'élève a un RDV (api/src/bookings/cv.service.ts:72)
- le planning du recruteur pour savoir quel élève il doit rencontrer et à quel créneau (api/src/bookings/schedule.service.ts:16)
- le suivi des stands vides par l'équipe (api/src/dashboard/dashboard.service.ts:70)
- les comptes recruteurs créés par l'équipe (api/src/companies/companies.service.ts:133)

Notons que cette mise en place découle aussi des questions posées à Léo qui nous ont permis de changer certaines idées, notamment l'idée d'une file d'attente. Pour citer la discussion:
> Qu'attendez-vous concrètement de la solution pour améliorer la situation ? Faut-il par exemple gérer des rendez-vous, des créneaux ou des files d'attente virtuelles ?

>[...]Une file d'attente virtuelle, j'y crois moins : elle raccourcit la queue devant le grand groupe, mais elle n'envoie personne vers les PME.

On peut résumer cela en l'implémentation de 3 fonctionnalités majeures : 
1. La consultation du catalogue des entreprises (api/src/companies/companies.controller.ts)
2. Les rendez-vous avec le CV (api/src/bookings/bookings.service.ts, api/src/bookings/cv.service.ts)
3. Le jour J: le planning du recruteur et le tableau de bord (api/src/bookings/schedule.service.ts, api/src/dashboard/dashboard.service.ts)

La partie véritablement notable qui sort des TPs est celle sur les CV, qui fait appelle à l'upload de fichiers. 

## Journal de décisions

1.  On a implémenté un "interrupteur" que l'équipe actionne pour ouvrir les réservations aux 1A car Léo veut les 2A/3A d'abord, donc bloquer temporairement les 1A semble être la solution la plus simple et flexible car l'équipe peut leur ouvrir les réservations quand elle veut.
On a considéré à dédier un quota de réservations aux 2A/3A mais c'était sûrement se compliquer la vie pour rien.

**Preuve** : api/src/bookings/bookings.service.ts:35  

**Commit** : 663abd2

2. Les créneaux font 20 minutes plutôt qu'une autre durée. C'est un point non discuté avec Léo, mais on s'est dit que 20 min correspondrait à peu près à une visio préliminaire pour un entretien, et que la situation y ressemble.

**Preuve**: api/src/forum.config.ts:28  

**Commit** : df57d34

3. Le catalogue est trié par places libres plutôt que par les plus naturels tris par nom au domaine. Comme le but est de faire remonter les PME, ce tri semblait primordial.  

**Preuve**: web/src/pages/CatalogPage.tsx:36  

**Commit** 32f46e0

4. On a fixé 5 RDV au plus par élève au lieu mettre aucune limite (autre que un RDV par entreprise) pour éviter de recréer la queue.  

**Preuve**: api/src/forum.config.ts:32  

**Commit** df57d34

5. La contrainte de l'unique couple (élève, entreprise) est gérée par la base, plutôt que par une vérification seulement dans le code pour nous éviter d'éventuels problèmes si deux clics arrivent simultanément: ce sera la base qui tranchera.  

**Preuve** : api/prisma/schema.prisma:129  

**Commit**: 62f58cc

## L'IA écartée

L'agent IA nous a suggéré que les élèvent pourraient "donner l'URL de leur CV (champ texte validé par @isUrl, comme website), mais un lien reste lisible par n'importe qui qui l'obtient." Comme Léo souhaite que les CV soient visibles que par les recruteurs concernés, on a préféré l'envoi des CV par pdf.