# Expression Profiling of Differentially Expressed Genes Under Stress Conditions and FLC1 Modulation in *Cryptococcus neoformans*

## Executive summary

This report analyses RNA-seq data from an experiment designed to understand how *Cryptococcus neoformans* responds to cell wall stress under varying genetic and environmental conditions, with a focus on the FLC1 gene, a candidate antifungal drug target. Cells from wild-type and FLC1Δ strains were grown under combinations of temperature (30°C or 37°C) and growth media (YPD, with or without CFW and/or EGTA), simulating stress conditions.

The analysis confirmed strong biological replicate consistency of the experimental data and revealed that strain background shaped the response to stress: FLC1Δ cells displayed more pronounced expression changes, particularly in response to CFW and at higher temperatures. Key driver genes of this variation included FLC1 gene itself (CNAG_04283), as well as CNAG_01653, CNAG_04891, and CNAG_00588. 

Differential expression analysis identified over 3,400 genes (52.4%) with significant changes related to the interaction of the experimental factors, especially when contrasting the FLC1Δ strain under compound stress (CFW + EGTA at 37°C) with the wild-type strain under basal medium at 37°C, where most were downregulated. One gene, CNAG_06576, showed consistent high significance and condition-specific regulation. Clustering the top 500 most informative DE genes revealed four major expression patterns, primarily driven by strain and stress condition, with one cluster reflecting stress-induced repression in the mutant FLC1Δ strain.

The findings suggest FLC1 plays a key role in mediating the transcriptional stress response. A ranked list of the top 100 DE genes is provided for future functional characterisation. While robust, the results are based on a single DE method (`DESeq2`), and could be further validated using complementary statistical methods.

### Session info

```{bash}
─ Session info ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
 setting  value
 version  R version 4.4.1 (2024-06-14 ucrt)
 os       Windows 11 x64 (build 26100)
 system   x86_64, mingw32
 ui       RStudio
 language (EN)
 collate  English_United States.utf8
 ctype    English_United States.utf8
 tz       Europe/London
 date     2025-07-01
 rstudio  2025.05.1+513 Mariposa Orchid (desktop)
 pandoc   3.4 @ C:\\PROGRA~1\\Pandoc\\pandoc.exe
 quarto   ERROR: Unknown command "TMPDIR=C:/Users/Diego/AppData/Local/Temp/RtmpARcqtO/file407c417939bc". Did you mean command "create"? @ C:\\PROGRA~1\\RStudio\\RESOUR~1\\app\\bin\\quarto\\bin\\quarto.exe

─ Packages ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
 ! package              * version    date (UTC) lib source
   abind                  1.4-8      2024-09-12 [1] RSPM (R 4.4.0)
   apeglm                 1.28.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P backports              1.5.0      2024-05-23 [?] RSPM
   bbmle                  1.0.25.1   2023-12-09 [1] RSPM (R 4.4.0)
   bdsmatrix              1.3-7      2024-03-02 [1] RSPM (R 4.4.0)
 P beachmat               2.22.0     2024-10-29 [?] Bioconduc~
   Biobase              * 2.66.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
   BiocGenerics         * 0.52.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P BiocManager            1.30.26    2025-06-05 [?] RSPM
   BiocParallel           1.40.2     2025-06-22 [1] Bioconductor
 P BiocSingular           1.22.0     2024-10-29 [?] Bioconduc~
 P bit                    4.6.0      2025-03-06 [?] RSPM
 P bit64                  4.6.0-1    2025-01-16 [?] RSPM
 P broom                  1.0.8      2025-03-28 [?] RSPM
 P car                    3.1-3      2024-09-27 [?] CRAN (R 4.4.1)
 P carData                3.0-5      2022-01-06 [?] RSPM
 P circlize               0.4.16     2024-02-20 [?] RSPM
 P cli                    3.6.5      2025-04-23 [?] RSPM
 P clipr                  0.8.0      2022-02-22 [?] RSPM
 P clue                   0.3-66     2024-11-13 [?] RSPM
 P cluster                2.1.6      2023-12-01 [?] CRAN (R 4.4.1)
   coda                   0.19-4.1   2024-01-31 [1] RSPM (R 4.4.0)
 P codetools              0.2-20     2024-03-31 [?] CRAN (R 4.4.1)
 P colorspace             2.1-1      2024-07-26 [?] RSPM
 P commonmark             1.9.5      2025-03-17 [?] CRAN (R 4.4.3)
 P ComplexHeatmap       * 2.22.0     2024-10-29 [?] Bioconduc~
 P cowplot                1.1.3      2024-01-22 [?] RSPM
 P crayon                 1.5.3      2024-06-20 [?] RSPM
   DelayedArray           0.32.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P DelayedMatrixStats     1.28.1     2025-01-09 [?] Bioconduc~
   DESeq2               * 1.46.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P digest                 0.6.37     2024-08-19 [?] RSPM
 P doParallel             1.0.17     2022-02-07 [?] RSPM
 P dplyr                * 1.1.4      2023-11-17 [?] RSPM
 P dqrng                  0.4.1      2024-05-28 [?] RSPM
   edgeR                * 4.4.2      2025-01-27 [1] Bioconductor 3.20 (R 4.4.2)
   emdbook                1.3.13     2023-07-03 [1] RSPM (R 4.4.0)
 P evaluate               1.0.3      2025-01-10 [?] RSPM
 P factoextra             1.0.7      2020-04-01 [?] CRAN (R 4.4.1)
 P farver                 2.1.2      2024-05-13 [?] RSPM
 P fastmap                1.2.0      2024-05-15 [?] RSPM
 P forcats                1.0.0      2023-01-29 [?] RSPM
 P foreach                1.5.2      2022-02-02 [?] RSPM
 P Formula                1.2-5      2023-02-24 [?] RSPM
 P generics               0.1.4      2025-05-09 [?] RSPM
   GenomeInfoDb         * 1.42.3     2025-01-27 [1] Bioconductor 3.20 (R 4.4.2)
   GenomeInfoDbData       1.2.13     2025-06-22 [1] Bioconductor
   GenomicRanges        * 1.58.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P GetoptLong             1.0.5      2020-12-15 [?] RSPM
 P ggplot2              * 3.5.2      2025-04-09 [?] RSPM
 P ggpubr                 0.6.0      2023-02-10 [?] RSPM
 P ggrepel              * 0.9.6      2024-09-07 [?] CRAN (R 4.4.1)
 P ggsci                  3.2.0      2024-06-18 [?] RSPM
 P ggsignif               0.6.4      2022-10-13 [?] RSPM
 P GlobalOptions          0.1.2      2020-06-10 [?] RSPM
 P glue                   1.8.0      2024-09-30 [?] RSPM
 P gt                   * 1.0.0      2025-04-05 [?] RSPM
 P gtable                 0.3.6      2024-10-25 [?] CRAN (R 4.4.1)
 P hms                    1.1.3      2023-03-21 [?] RSPM
 P htmltools              0.5.8.1    2024-04-04 [?] RSPM
 P httr                   1.4.7      2023-08-15 [?] RSPM
   IRanges              * 2.40.1     2024-12-05 [1] Bioconductor 3.20 (R 4.4.2)
 P irlba                  2.3.5.1    2022-10-03 [?] RSPM
 P iterators              1.0.14     2022-02-05 [?] RSPM
 P jsonlite               2.0.0      2025-03-27 [?] RSPM
 P knitr                  1.50       2025-03-16 [?] RSPM
 P labeling               0.4.3      2023-08-29 [?] RSPM
 P lattice                0.22-6     2024-03-20 [?] CRAN (R 4.4.1)
 P lifecycle              1.0.4      2023-11-07 [?] RSPM
   limma                * 3.62.2     2025-01-09 [1] Bioconductor 3.20 (R 4.4.2)
 P litedown               0.7        2025-04-08 [?] RSPM
   locfit                 1.5-9.12   2025-03-05 [1] RSPM (R 4.4.0)
 P magrittr               2.0.3      2022-03-30 [?] RSPM
 P markdown               2.0        2025-03-23 [?] RSPM
 P MASS                   7.3-60.2   2024-04-26 [?] CRAN (R 4.4.1)
 P Matrix                 1.7-0      2024-04-26 [?] CRAN (R 4.4.1)
   MatrixGenerics       * 1.18.1     2025-01-09 [1] Bioconductor 3.20 (R 4.4.2)
   matrixStats          * 1.5.0      2025-01-07 [1] RSPM (R 4.4.0)
 P mgcv                   1.9-1      2023-12-21 [?] CRAN (R 4.4.1)
 P mvtnorm                1.3-3      2025-01-10 [?] RSPM
 P nlme                   3.1-164    2023-11-27 [?] CRAN (R 4.4.1)
 P numDeriv               2016.8-1.1 2019-06-06 [?] RSPM
 P patchwork            * 1.3.1      2025-06-21 [?] RSPM
 P PCAtools             * 2.18.0     2024-10-29 [?] Bioconduc~
 P pillar                 1.10.2     2025-04-05 [?] RSPM
 P pkgconfig              2.0.3      2019-09-22 [?] RSPM
 P plyr                   1.8.9      2023-10-02 [?] RSPM
 P png                    0.1-8      2022-11-29 [?] CRAN (R 4.4.0)
 P purrr                * 1.0.4      2025-02-05 [?] RSPM
 P R6                     2.6.1      2025-02-15 [?] RSPM
 P ragg                   1.4.0      2025-04-10 [?] RSPM
 P RColorBrewer           1.1-3      2022-04-03 [?] RSPM
 P Rcpp                   1.0.14     2025-01-12 [?] RSPM
 P readr                  2.1.5      2024-01-10 [?] RSPM
   renv                   1.1.4      2025-03-20 [1] RSPM (R 4.4.0)
 P reshape2               1.4.4      2020-04-09 [?] RSPM
 P rjson                  0.2.23     2024-09-16 [?] RSPM
 P rlang                  1.1.6      2025-04-11 [?] RSPM
 P rstatix                0.7.2      2023-02-01 [?] RSPM
 P rstudioapi             0.17.1     2024-10-22 [?] RSPM
 P rsvd                   1.0.5      2021-04-16 [?] RSPM
   S4Arrays               1.6.0      2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
   S4Vectors            * 0.44.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P sass                   0.4.10     2025-04-11 [?] RSPM
 P ScaledMatrix           1.14.0     2024-10-29 [?] Bioconduc~
 P scales                 1.4.0      2025-04-24 [?] RSPM
 P sessioninfo            1.2.3      2025-02-05 [?] RSPM
 P shape                  1.4.6.1    2024-02-23 [?] RSPM
   snow                   0.4-4      2021-10-27 [1] RSPM (R 4.4.0)
   SparseArray            1.6.2      2025-02-20 [1] Bioconductor 3.20 (R 4.4.2)
 P sparseMatrixStats      1.18.0     2024-10-29 [?] Bioconduc~
   statmod                1.5.0      2023-01-06 [1] RSPM (R 4.4.0)
 P stringi                1.8.7      2025-03-27 [?] RSPM
 P stringr                1.5.1      2023-11-14 [?] RSPM
   SummarizedExperiment * 1.36.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P systemfonts            1.2.3      2025-04-30 [?] RSPM
 P textshaping            1.0.1      2025-05-01 [?] RSPM
 P tibble                 3.3.0      2025-06-08 [?] RSPM
 P tidyr                * 1.3.1      2024-01-24 [?] RSPM
 P tidyselect             1.2.1      2024-03-11 [?] RSPM
 P tzdb                   0.5.0      2025-03-15 [?] RSPM
   UCSC.utils             1.2.0      2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P vctrs                  0.6.5      2023-12-01 [?] RSPM
 P vroom                  1.6.5      2023-12-05 [?] RSPM
 P withr                  3.0.2      2024-10-28 [?] CRAN (R 4.4.1)
 P xfun                   0.52       2025-04-02 [?] RSPM
 P xml2                   1.3.8      2025-03-14 [?] RSPM
   XVector                0.46.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)
 P yaml                   2.3.10     2024-07-26 [?] RSPM
   zlibbioc               1.52.0     2024-10-29 [1] Bioconductor 3.20 (R 4.4.1)

 [1] C:/Users/Diego/Documents/MSc/Dissertation/Project 1/gene-expression/renv/library/windows/R-4.4/x86_64-w64-mingw32
 [2] C:/Users/Diego/AppData/Local/R/cache/R/renv/sandbox/windows/R-4.4/x86_64-w64-mingw32/e0da0d43

 * ── Packages attached to the search path.
 P ── Loaded and on-disk path mismatch.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

```

