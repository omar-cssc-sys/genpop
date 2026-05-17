# Génomique des populations — Chr21

## Description
Analyse de la diversité génétique à partir d'un sous-ensemble de variants 
du chromosome 21 (1% des variants du fichier 1000 Genomes phase 3).

## Données
- Source : 1000 Genomes Project Phase 3
- Chromosome : 21
- Variants retenus : ~11 000 SNPs (subset chr21)
- Lien : https://hgdownload.soe.ucsc.edu/gbdb/hg19/1000Genomes/phase3/

## Structure du projet
├── plink/        # Fichiers binaires PLINK (bed, bim, fam)
├── admixture/    # Résultats ADMIXTURE (fichiers Q et P)
├── pca/          # Analyse en composantes principales
├── stats/        # Statistiques de diversité
└── filtrage/     # Fichiers issus des étapes de filtrage

## Logiciels utilisés
- PLINK
- ADMIXTURE
- R / ggplot2

## Auteur
- omar-cssc-sys
- email : omar-cssc@hotmail.com
