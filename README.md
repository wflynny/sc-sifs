# Single Cell SIFs

This repo contains the definition files for several singularity image files
that contain 10X Genomics CellRanger and other tools used for Single Cell
genomics analyses.

## Basics

The two image bases that are used are `alpine` and `debian:buster-slim`.
Alpine is super useful for its very small uncompressed filesize, but from
experience it doesn't play nicely with Python due to its lack of glibc, so for
tools that rely on Python we use `debian:buster-slim` (a trimmed version of
Debian 10).

## Note on CellRanger

Due to the way 10X Genomics makes their software available, the download links
to the `*ranger-?.?.?.tar.gz` tarballs are internal JAX cloud storage, not
accessible to the external internet.  These download links are just static
mirrors of the tarballs made available on the various 10X Genomics software
downloads pages. This is because:

1. 10X software has expiration datetimes and tracking keys in the URLs which
   make it difficult for a build file used today to work tomorrow, and
2. Now-defunct software versions, like 2.0.1, are not made available publicly
   once they are superceded by new versions.

If you are trying to use these build files as is, you will just need to modify
the following lines:

    # Modify link!
    wget -nv -O cellranger-1.3.1.tar.gz "https://singlecell-software.s3-far.jax.org/cellranger-1.3.1.tar.gz"
    # Just remove these two lines or hardcode the md5sum 10X provides on the web
    wget -nv -O cellranger-1.3.1.tar.gz.sha1 "https://singlecell-software.s3-far.jax.org/cellranger-1.3.1.tar.gz.sha1"
    sha1sum --status -c cellranger-1.3.1.tar.gz.sha1
