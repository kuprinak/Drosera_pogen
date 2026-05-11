## Install bcftools, plink and admixture

```{bash}
bcftools view -m2 -M2 -v snps md6ct95ms200.vcf -Oz -o md6ct95ms200.biallelic.vcf.gz
bcftools index md6ct95ms200.biallelic.vcf.gz
```
## Create a numeric mapping

```{bash}
plink --vcf md6ct95ms200.biallelic.vcf.gz --make-bed --out md6ct95ms200_biallelic --allow-extra-chr 

awk '{$1=1; print $0}' md6ct95ms200_biallelic.bim > md6ct95ms200_biallelic_numeric.bim

plink --bfile md6ct95ms200_biallelic \
      --make-bed \
      --bim md6ct95ms200_biallelic_numeric.bim \
      --fam md6ct95ms200_biallelic.fam \
      --out md6ct95ms200_numeric

plink --bfile md6ct95ms200_numeric \
      --geno 0.9999 \
      --make-bed \
      --out md6ct95ms200_numeric
```

## Run ADMIXTURE

```{bash}
for K in {1..20}; do
    admixture --cv=10 md6ct95ms200_numeric.bed $K | tee log${K}.out
done

grep "CV error" log*.out | sed -E 's/.*\(K=([0-9]+)\): ([0-9.]+)/\1 \2/' > cv_errors.txt
```
