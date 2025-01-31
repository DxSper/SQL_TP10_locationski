# Requêtes SQL pour le TP10 location ski

## Ex1 - Liste des fiches de location
```sql
SELECT * FROM fiches;
```

## Ex2 - Liste des clients ayant loué du matériel
```sql
SELECT DISTINCT clients.* 
FROM clients 
JOIN fiches ON clients.noCli = fiches.noCli;
```

## Ex3 - Nombre total de fiches de location
```sql
SELECT COUNT(*) AS total_fiches FROM fiches;
```

## Ex4 - Durée moyenne des locations
```sql
SELECT AVG(DATEDIFF(COALESCE(lignesFic.retour, NOW()), lignesFic.depart)) AS duree_moyenne 
FROM lignesFic;
```

## Ex5 - Articles les plus loués
```sql
SELECT articles.refArt, articles.designation, COUNT(*) AS nombre_locations 
FROM lignesFic
JOIN articles ON lignesFic.refArt = articles.refArt 
GROUP BY articles.refArt, articles.designation 
ORDER BY nombre_locations DESC 
LIMIT 10;
```

## Ex6 - Montant total des locations par fiche
```sql
SELECT fiches.noFic, SUM(tarifs.prix * DATEDIFF(COALESCE(lignesFic.retour, NOW()), lignesFic.depart)) AS montant_total 
FROM fiches
JOIN lignesFic ON fiches.noFic = lignesFic.noFic
JOIN articles ON lignesFic.refArt = articles.refArt
JOIN grilleTarifs ON articles.codeGam = grilleTarifs.codeGam AND articles.codeCate = grilleTarifs.codeCate
JOIN tarifs ON grilleTarifs.codeTarif = tarifs.codeTarif
GROUP BY fiches.noFic;
```

## Ex7 - Liste des fiches non réglées
```sql
SELECT * FROM fiches WHERE etat = 'en cours';
```

## Ex8 - Nombre d'articles loués par gamme
```sql
SELECT gammes.libelle, COUNT(*) AS nombre_locations 
FROM articles 
JOIN gammes ON articles.codeGam = gammes.codeGam 
JOIN lignesFic ON articles.refArt = lignesFic.refArt 
GROUP BY gammes.libelle;
```

## Ex9 - Clients ayant loué plus de 5 fois
```sql
SELECT clients.noCli, clients.nom, clients.prenom, COUNT(fiches.noFic) AS nombre_locations
FROM clients
JOIN fiches ON clients.noCli = fiches.noCli
GROUP BY clients.noCli, clients.nom, clients.prenom
HAVING nombre_locations > 5;
```

## Ex10 - Articles jamais loués
```sql
SELECT * FROM articles 
WHERE refArt NOT IN (SELECT DISTINCT refArt FROM lignesFic);
```

## Ex11 - Montant total des locations
```sql
SELECT SUM(montant_total) AS montant_global FROM (
    SELECT fiches.noFic, SUM(tarifs.prix * DATEDIFF(COALESCE(lignesFic.retour, NOW()), lignesFic.depart)) AS montant_total
    FROM fiches
    JOIN lignesFic ON fiches.noFic = lignesFic.noFic
    JOIN articles ON lignesFic.refArt = articles.refArt
    JOIN grilleTarifs ON articles.codeGam = grilleTarifs.codeGam AND articles.codeCate = grilleTarifs.codeCate
    JOIN tarifs ON grilleTarifs.codeTarif = tarifs.codeTarif
    GROUP BY fiches.noFic
) AS sous_requete;
```

---


