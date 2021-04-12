---
title: "Le 580000"
date: 2021-04-12T00:00:00+01:00
slug: "580000"
tags: [TIL]
--- 

Lors d'un projet de reprisse de données comptables, je me suis retrouvé
confronté à une génération automatique d'écriture comptable sur le compte
580000.

Quelques recherches et échanges avec des experts comptables m'ont permis de
comprendre l'anomalie.

- un journal de banque par compte bancaire
- utilisation du 580000 (virements internes) pour faire un virement compte bancaire à
    compte bancaire

Le fichier à importer ne respectant pas ces règles, l'outil métier corrige
les écritures comptables en incorporant un 580000.

Résultat quelques heures de recette de plus et une importation répondant au règle métier


