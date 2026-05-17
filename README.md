# Génomique des Populations — Chromosome 21 (1000 Genomes Project)

## Description
Ce projet constitue une analyse complète de la structure génétique et de la 
diversité des populations humaines à partir d'un sous-ensemble de variants du 
chromosome 21 issus du 1000 Genomes Project Phase 3. Il couvre l'ensemble du 
pipeline analytique, du contrôle qualité des variants jusqu'à l'inférence de 
la structure de population par ADMIXTURE et PCA.

---

## Données
- **Source** : 1000 Genomes Project Phase 3
- **Chromosome** : 21
- **Fichier original** : `ALL.chr21.phase3_shapeit2_mvncall_integrated_v5a.20130502.genotypes.vcf.gz` (209 Mo — non inclus)
- **Subset utilisé** : `chr21_subset.vcf.gz` (~2.6 Mo — 1% des variants originaux)
- **Individus** : 2504 individus issus de populations mondiales
- **Variants initiaux** : 13 427 SNPs
- **Variants après pruning LD** : 11 406 SNPs

---

## Pipeline d'analyse

### 1. Contrôle qualité avec VCFtools
Calcul des statistiques de base sur le fichier VCF brut :
- Qualité des variants (`--site-quality`)
- Profondeur moyenne par site (`--site-depth`)
- Profondeur par individu (`--depth`)
- Données manquantes par site (`--missing-site`) et par individu (`--missing-indv`)
- Fréquence des allèles mineurs (`--freq`)

### 2. Filtrage
Paramètres de filtrage appliqués avec VCFtools :
- `MAF = 0.05` — exclusion des variants rares
- `MISS = 0.99` — sites présents chez au moins 99% des individus
- `QUAL = 30` — score de qualité minimal
- `MIN_DEPTH = 3` / `MAX_DEPTH = 200` — profondeur acceptable

### 3. Conversion et pruning LD avec PLINK
- Conversion du VCF au format binaire PLINK (`.bed`, `.bim`, `.fam`)
- Pruning par déséquilibre de liaison : fenêtre 50 SNPs, pas 10, r² = 0.1
- 2021 variants éliminés, 11 406 variants retenus

### 4. Analyse en composantes principales (PCA)
- PCA calculée avec PLINK sur les variants pruned
- Visualisation des 5 premières composantes principales
- Trois groupes continentaux clairement identifiés : Africains, Européens, Asiatiques

### 5. Inférence de structure — ADMIXTURE
- Logiciel : ADMIXTURE 1.3.0 (32-bit)
- K testé : 1 à 3
- Sélection du K optimal par validation croisée (CV error)
- K=3 retenu comme optimal (CV error = 0.04804)
- Résultats cohérents avec la structure continentale observée en PCA
---

## Logiciels utilisés

| Outil | Version | Usage |
|-------|---------|-------|
| VCFtools | 0.1.16 | Contrôle qualité et filtrage |
| PLINK | 1.9 | Conversion, pruning LD, PCA |
| ADMIXTURE | 1.3.0 | Structure de population |
| R / ggplot2 | 4.x | Visualisation |
| Python / numpy | 3.x | Analyses complémentaires |

---

## Reproduire l'environnement

```bash
conda env create -f environment_minimal.yml
conda activate popgen2
```

---

## Résultats principaux
- Le fichier `chr21_subset.vcf.gz` présente une qualité exceptionnelle 
  (taux de génotypage > 99.98%) typique des données du 1000 Genomes Project
- La distribution du MAF révèle une majorité de variants rares 
  (médiane = 0.0003) avec une minorité de variants communs
- La PCA et ADMIXTURE convergent vers **3 groupes ancestraux** 
  correspondant aux grandes régions continentales : Afrique, Europe et Asie

---

## Auteur
**Omar Kadiri**  
Contact : omar-cssc@hotmail.com  
GitHub : [omar-cssc-sys](https://github.com/omar-cssc-sys)

---

## Référence
1000 Genomes Project Consortium (2015). A global reference for human genetic 
variation. *Nature*, 526, 68–74.

---

