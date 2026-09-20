# 03 - Gestion des anomalies et priorites

## Registre

Project GitHub `#1` est le tableau de bord des anomalies ; chaque anomalie est une GitHub Issue liee au Project.

## Declaration

1. Decrire le contexte, environnement, etapes de reproduction, resultat attendu, resultat observe et preuve non sensible.
2. Indiquer l'impact, la frequence et une severite proposee : bloquante, majeure, mineure ou cosmetique.
3. Ajouter les liens vers l'US, le cas de test, l'execution ou le deploiement concernes.
4. Ne jamais placer de secret, message de contact, adresse e-mail complete ou donnee reelle dans le ticket.

## Qualification et priorite

1. Mikaya ou l'agent competent verifie la reproductibilite et propose severite, priorite et contournement.
2. Le sponsor seul valide la priorite, toute exception et la decision d'accepter un risque.
3. Une correction est testee sur recette avant cloture ; le ticket conserve les preuves et le commit associe.

## Regle de blocage

Une anomalie bloquante ou majeure ouverte interdit la production. Il en est de meme pour une violation axe critique ou serieuse non justifiee, un E2E critique en echec ou une CI en echec.

## Retour arriere

Si une correction cree une regression, rouvrir ou creer l'anomalie liee, arreter la promotion et appliquer la procedure [08](08-incident-retour-arriere-et-post-mortem.md).