# tb-moldova-203

In this dataset, mutations in resistance genes was removed in the timetree analysis in order to avoid selection impacting on clock-i-ness.

Commands to replicate

`augur refine -a data/MoldovaUral203_010920_filtres.vcf.gz -t results/tree_203_filtres.nwk --output-tree results/tree_203_refine_timetree_BEST.nwk --vcf-reference auxiliary/M_tuberculosis_H37Rv.fasta --metadata data/metaUral203.tsv --timetree --output-node-data results/branch_lengths_203_filtres_time_BEST.json --clock-filter-iqd 3 --coalescent opt --root least-squares --clock-rate 0.0000003 --clock-std-dev 0.00000005`

`augur ancestral --tree results/tree_203_refine_filtres_timetree_BEST.nwk --alignment data/MoldovaUral203_062620.vcf.gz --vcf-reference auxiliary/M_tuberculosis_H37Rv.fasta --inference joint --output results/nt_muts_203_filtres_time.json --output-vcf results/nt_muts_203_filtres_time.vcf
augur translate --tree results/tree_203_refine_filtres_timetree_BEST.nwk --ancestral-sequences results/nt_muts_203_filtres_time.vcf --vcf-reference auxiliary/M_tuberculosis_H37Rv.fasta --genes config/genes.txt --reference-sequence config/Mtb_H37Rv_NCBI_Annot.gff --output results/aa_muts_203_filtres_time.json --alignment-output results/translations_203_filtres_time.vcf --vcf-reference-output results/translations_reference_203_filtres_time.fasta`

`augur traits -t results/tree_203_refine_filtres_timetree_BEST.nwk --metadata data/metaUral203.tsv --columns country --output-node-data results/traits_203_filtres_time.json`

`augur sequence-traits --ancestral-sequences results/nt_muts_203_filtres_time.vcf --translations results/translations_203_filtres_time.vcf --vcf-reference auxiliary/M_tuberculosis_H37Rv.fasta --vcf-translate-reference results/translations_reference_203_filtres_time.fasta --features config/DRMs_AAnuc.tsv --label "Drug resistance" --output-node-data results/drms_203_filtres_time.json`

`augur export v2 --tree results/tree_203_refine_filtres_timetree_BEST.nwk --metadata data/metaUral203.tsv --auspice-config config/config.json --colors config/colors.tsv --lat-longs config/lat_longs.txt --node-data results/branch_lengths_203_filtres_time_BEST.json results/traits_203_filtres_time.json results/drms_203_filtres_time.json results/aa_muts_203_filtres_time.json results/clades.json results/nt_muts_203_filtres_time.json --output auspice/tb-moldova-203-filtres.json`
