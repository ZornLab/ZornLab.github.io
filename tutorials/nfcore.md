---
title: Using nf-core on the cluster
---

Important notes before you begin:

- Do not edit/move/delete any of the other directories besides the one you are working in. 
- If you already have your raw data elsewhere on the cluster, it does not need to be copied to this directory. This will help free space for other users.

1. Navigate to /data/CuSTOM-DB-NGS/ 
2. Go to your lab directory under "labs", or create a new one if not already there.
3. Go to the [nf-core website](https://nf-co.re/pipelines) and find the specifics for the pipeline you plan to use. 
4. Set up your csv samplesheet according to the instructions on the website.
5. Set up a bash script containing bsub parameters, module loading, and your "nextflow run" command. See the provided examples for more information.
6. Monitor progress of the pipeline using "bsub" and "bpeek" commands, and check the logs if the job appears to fail.
