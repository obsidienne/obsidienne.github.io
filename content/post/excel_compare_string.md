---
title: "Confirmer la présence de cellule en minuscule"
date: 2021-02-19T00:00:00+01:00
slug: "check-uppercase-excel"
tags: [Excel]
categories: [TIL]
--- 

Aujourd'hui j'ai appris que l'on pouvait utiliser la macro Excel [EXACT](https://support.microsoft.com/en-us/office/exact-function-d3087698-fc15-4a15-9631-12575cf29926) et [MAJUSCULE](https://support.microsoft.com/fr-fr/office/majuscule-majuscule-fonction-c11f29b3-d1a3-4537-8df6-04d0049963d6) pour savoir si une colonne contient des valeurs en miniscule

```
=EXACT(B7;MAJUSCULE(B7))
```

![](https://res.cloudinary.com/dswia5bj3/image/upload/s--QUr4EeEL--/f_auto,fl_force_strip.immutable_cache/v1613734415/CV_Hugo_GitHub/excel-uppercase.png)