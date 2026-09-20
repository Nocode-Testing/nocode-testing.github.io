# 02 - Gestion des user stories et tickets

## Registre de travail

- Project GitHub `#2` est le Kanban des user stories, taches, dette et actions qualite.
- Les tickets restent des GitHub Issues afin de conserver description, discussion et liens Git.
- La chaine documentaire est `exigence -> US -> cas de test -> campagne -> execution`.

## Creation

1. Scarce PO redige une US avec objectif utilisateur, perimetre, criteres d'acceptation, exclusions et liens vers les exigences.
2. Camity, Rindel, Mikaya, Mina ou Soso ajoutent les contraintes de leur domaine lorsque necessaire.
3. L'auteur prepare un ticket pret a creer ou le cree seulement avec une integration GitHub explicitement autorisee.
4. Le ticket est lie au Project `#2`, aux cas de test et aux dependances pertinentes.
5. Le sponsor valide la priorite et les exceptions ; les agents peuvent uniquement proposer une priorite.

## Cycle Kanban

1. A cadrer : besoin incomplet ou non valide.
2. Pret : criteres, dependances et tests definis.
3. En cours : lot valide et responsable identifie.
4. En recette : commit deploye sur recette stable et preuves en cours.
5. Termine : recette et promotion, si applicable, validees par le sponsor.

## Point de controle

Une US ne passe pas en cours sans criteres testables. Elle ne passe pas a termine sans lien vers le commit ou la PR, resultat de recette et decision du sponsor.