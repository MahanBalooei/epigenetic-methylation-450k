# Differential DNA Methylation Analysis on Illumina 450K Arrays

Group assignment for the DNA/RNA Dynamics course, MSc Bioinformatics, University of Bologna.

`analysis.R` goes from raw Illumina HumanMethylation450K IDAT files to a list of CpG sites that differ between a control group and a disease group, with the usual quality checks and plots along the way. It is written in R with Bioconductor's `minfi`.

The dataset was provided by the course: eight samples, labelled `CTRL` or `DIS` in the sample sheet. The raw files are not ours to redistribute, so they are not in this repository, and the script will not run without a comparable dataset of your own.

## What the script does

1. **Load the data.** Reads the sample sheet and IDAT files into an `RGChannelSet` and extracts the red and green intensity matrices.
2. **Inspect a single probe.** Looks up one assigned probe address (40796508) and reports its Infinium design type and its intensities in each sample. This was part of the assignment.
3. **Quality control.** Builds the raw methylation set, draws the methylated-versus-unmethylated median intensity QC plot, and computes detection p-values, flagging positions above 0.05.
4. **Raw beta and M values.** Compares the density of mean beta and mean M values between the two groups.
5. **Normalisation.** Applies `preprocessQuantile` and compares raw and normalised data, separately for Infinium I and II probes, in a six-panel figure (density of means, density of standard deviations, boxplots).
6. **PCA.** Principal component analysis of the normalised beta values, coloured by group, by sex and by Sentrix ID to look for batch effects.
7. **Differential methylation.** A Welch t-test at each CpG site between the two groups, followed by Benjamini-Hochberg and Bonferroni correction. The script counts how many probes pass at 0.05 before and after each correction.
8. **Plots.** A volcano plot (difference in mean beta against nominal p-value, highlighting probes with an absolute difference above 0.1 and p below 0.01), a Manhattan plot, and a heatmap with hierarchical clustering on a subset of 100 probes.

## What to keep in mind

This is a teaching exercise, and the analysis is deliberately simple.

- With four samples per group, a per-probe t-test has very little power, and few or no probes can be expected to survive correction across roughly 450,000 tests. A moderated test such as `limma` would be the standard choice for a real study.
- Sex and array batch are inspected in the PCA but are not included as covariates. Cell-type composition is not estimated.
- File paths and group labels are written into the script and match the course dataset. They need editing for other data.

## Running it

```r
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c(
  "minfi",
  "IlluminaHumanMethylation450kmanifest",
  "IlluminaHumanMethylation450kanno.ilmn12.hg19"
))

install.packages(c("gplots", "qqman"))
```

Put the IDAT files and the sample sheet in a folder called `Input_Data`, next to `analysis.R`. The sample sheet needs at least the columns `Group`, `Sex`, `SampleID` and `Sentrix_ID`. The script also expects a cleaned copy of the Illumina 450K manifest (`Illumina450Manifest_clean.RData`), which was provided in the course. Then run the script section by section in RStudio; it was written to be stepped through, not run in one go.

## Contributors

Elif Güler ([@elif-guler](https://github.com/elif-guler)), Eyip Sinay Dalmaz ([@Dalmaz-ES](https://github.com/Dalmaz-ES)), Simay Erol ([@Simay9](https://github.com/Simay9)), Barkin Kemec ([@mbkemec](https://github.com/mbkemec)), Negin Nilforoosh ([@neginnilforosh](https://github.com/neginnilforosh)), Kimia Kanouni ([@kanounik](https://github.com/kanounik)) and Mahan Balooei ([@MahanBalooei](https://github.com/MahanBalooei)).

## License

MIT. See `LICENSE`.
