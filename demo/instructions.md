# Visualization for graph alignments

Here we use a simple deletion to demonstrate how to visualize read alignments on the sequence graph

CAUTION: **This pipeline only works for a single event.**

We are currently improving it to incorporate more events.

## Demo for visualization

[chr20_17081294.input.png](chr20_17081294.input.png) demonstrates how the graph is like for this simple deletion. Its VCF representation can be found in [chr20_17081294.vcf](chr20_17081294.vcf).

[chr20_17081294.alignment.json](chr20_17081294.alignment.json) is the output of graph alignments for this deletion from one Illumina sample.

Go to the visualization website:

- https://traxexx.github.io/paragraph-tubemap/

Click "Choose File" to upload `chr20_17081294.alignment.json`.

Click Parse. You will get a visualization same as [chr20_17081294.alignment.png](chr20_17081294.alignment.png)

## Generate graph alignments for visualization

Assume:
- the graph genotyper, [Paragraph](https://github.com/Illumina/paragraph), is installed in a directory named `paragraph-build`
- `$HG38` represents the path to the reference genome GRCh38
- `NA12878.bam` is the short-read BAM file you'd like to use as input

### Convert the VCF to JSON graph
```
python3 paragraph-tools-build/bin/vcf2paragraph.py \
    -r $HG38 \
    chr20_17081294.vcf \ # the input VCF
    chr20_17081294.input.json # the output converted JSON
```

### Perform graph alignment agains the JSON graph
```
~/Documents/paragraph-tools-build/bin/paragraph \
    -b ~/Documents/data/NA12878_1_S1.bam \
    -r $HG38 \
    -g chr20_17081294.input.json \ # the output from the above command
    -o chr20_17081294.alignment.json \ # alignment output
    -E 1 # Required to output alignments of all reads in the target region
```

`chr20_17081294.alignment.json` can be visualized on the visualization website.