# UNIX

## UNIX commands and tips

__Basename.__

```bash
for file in *.shp; do echo $(basename $file .shp)_poly.shp; done
```

__Listing.__ Long list and human readable.

```bash
ls -lh
```

__Print between two delimiters.__ Useful for extracting one to several sequences from a fasta file.

```bash
awk '/>gene1|>gene2|>gene3/{flag=1;print;next}/>/{flag=0}flag' in.fasta > out.fasta
```

