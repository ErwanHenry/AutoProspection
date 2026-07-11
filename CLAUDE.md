# AutoProspection — Contexte pour Claude/Keel

## Ce que c'est

Repo **embryon** : deux fichiers seulement (un README d'une ligne « Web app that automate a prospection workflow » et une fiche DATA_ROOM.md générée automatiquement le 2026-04-13). Aucun code. Créé le 2025-08-05, jamais développé depuis. La fiche data room le classe « B2B Prospection / Python / AI-powered B2B prospection automation system / Prototype ».

## Intention déduite du créateur

**Hypothèse à valider par Erwan.** Erwan (recruteur/placement IT chez SpikeeLabs, fondateur d'alignd) voulait une web app qui enchaîne TOUT le workflow de prospection B2B de bout en bout : sourcing de comptes/contacts → enrichissement (email, contexte) → génération de messages personnalisés → envoi → suivi. Créé en août 2025, probablement pour outiller sa propre prospection (SpikeeLabs et/ou alignd) avant que les briques spécialisées du portefeuille n'existent ou ne soient reliées entre elles.

## Direction recommandée

**Ne pas construire une énième web app de prospection.** Le portefeuille couvre déjà chaque étage : email-reacher (trouver l'email pro), playwright-worker (scraping), routerMessages (génération IA + envoi multi-canal), jarvi (CRM prospection SpikeeLabs), alignd (CRM/ATS ESN, projet phare). Ce qui manque, c'est **la glu** : un pipeline d'orchestration headless (Python, CLI/cron — pas d'UI) qui chaîne ces briques et dépose le résultat dans alignd/jarvi. AutoProspection devient donc **le module d'orchestration de prospection au service d'alignd**, pas un produit autonome. Si Erwan invalide cette direction, l'alternative honnête est l'archivage (retrait de la whitelist).

## Roadmap proposée

1. **Spec du pipeline** : écrire `PIPELINE.md` — inventaire des briques existantes (endpoints email-reacher, API routerMessages, capacités scraping, points d'entrée alignd), schéma des 5 étages (source → enrich → compose → send → track), formats d'échange (un `prospect.json` commun). Réalisable en une session.
2. **Squelette Python** : `pipeline.py` + un connecteur par brique (stubs), config `.env.example`, exécution dry-run sur 5 prospects fictifs.
3. **Premier étage réel** : brancher email-reacher (enrichissement) sur une liste CSV réelle, sortie vérifiable.
4. **Bout-en-bout supervisé** : chaîner enrichissement → routerMessages en mode preview (aucun envoi auto), validation humaine via digest Keel/Telegram.
5. **Intégration alignd** : pousser les prospects traités dans alignd ; décider alors si le repo est absorbé comme module d'alignd.

## Première action pour Keel

Créer `PIPELINE.md` à la racine : lister les briques du portefeuille avec leurs interfaces réelles (lire les README/code d'email-reacher et de routerMessages), dessiner les 5 étages du pipeline et proposer le schéma `prospect.json`. Poser en fin de fichier 3 questions fermées à Erwan (checklist à cocher) pour valider la direction « module au service d'alignd » avant toute ligne de code.
