# DeNanoPolish

DeNanoPolish is a comprehensive DNA count analysis pipeline designed to simplify the process of mapping reads to a reference genome and counting genes. This Python-based pipeline leverages the power of several renowned bioinformatics tools, including Minimap2, Samtools, and HTSeq, to deliver accurate and reliable results.

## Table of Contents

- **[Prerequisites](https://github.com/tedblry/DeNanoPolish/#prerequisites)**
- **[Installation](https://github.com/tedblry/DeNanoPolish/#installation)**
- **[Usage](https://github.com/tedblry/DeNanoPolish/#usage)**
- **[Polishing Rounds](https://github.com/tedblry/DeNanoPolish/#polishing-rounds)**
- **[Output](https://github.com/tedblry/DeNanoPolish/#output)**
- **[Contact](https://github.com/tedblry/DeNanoPolish/#contact)**

## Prerequisites

Before you begin, ensure you have met the following requirements:

- You have installed the following:
    - **[Python 3.8 or later](https://www.python.org/downloads/)**
    - **[Minimap2](https://github.com/lh3/minimap2)**
    - **[Samtools](http://www.htslib.org/)**
    - **[HTSeq](https://htseq.readthedocs.io/en/release_0.11.1/)**
    - **[Flye](https://github.com/fenderglass/Flye)**
    - **[Racon](https://github.com/lbcb-sci/racon)**
    - **[Medaka](https://nanoporetech.github.io/medaka/)**
    - **[QUAST](http://quast.sourceforge.net/quast)**

## Installation

For users with Macs equipped with the M1/M2 chip running on the arm64 architecture, a specific conda environment with a Python version compiled for arm64 is required. HTSeq should be installed in this environment. Here are the steps to set it up:

```
# Create a new conda environment with a Python version compiled for arm64
conda create -n htseq_arm64 python=3.8
# Activate the new environment
conda activate htseq_arm64
# Install HTSeq in the new environment
pip install HTSeq
```

## Installation

To install DeNanoPolish, follow these steps:

1. Clone the repository:
    
    ```
    git clone https://github.com/tedblry/DeNanoPolish.git
    ```
    
2. Navigate to the cloned repository:
    
    ```
    cd NanoDenovo
    ```
    

## Usage

To use DeNanoPolish, follow these steps:

1. Run the script with the path to your reads file, the path to the reference genome file, and the path to the output directory. You can also specify a prefix for the output files.
    
    ```
    python3 DeNanoPolish.py --sample [sample_file_path] --ref_fna [ref_fna_file_path] --ref_gtf [ref_gtf_file_path] --output [output_directory] --prefix [prefix_for_output_files]
    
    ```
    
    Replace `[sample_file_path]`, `[ref_fna_file_path]`, `[ref_gtf_file_path]`, and `[output_directory]` with the paths to your actual files and directories.
    

## Polishing Rounds

DeNanoPolish uses an iterative polishing process to improve the accuracy of the assembled genome. The process involves multiple rounds of error correction using Racon and Medaka.

In each Racon round, the pipeline aligns the reads to the current assembly using Minimap2, and then uses Racon to correct the assembly based on the alignments. This process is repeated for a specified number of iterations or until the assembly quality stops improving.

After the Racon rounds, the pipeline performs a final polishing round using Medaka. This round uses a different error model that is specifically designed for Oxford Nanopore reads, and can correct different types of errors compared to Racon.

The pipeline also includes a rollback mechanism. After each polishing round, it evaluates the quality of the new assembly using QUAST. If the quality of the assembly decreases, the pipeline reverts to the previous assembly.

## Output

Upon completion, DeNanoPolish generates the following output files in the specified output directory:

- A SAM file with the mapping results.
- A BAM file converted from the SAM file.
- A sorted BAM file.
- A BAM index file.
- A statistics file generated from the sorted BAM file.
- A counts file with read counts for each gene.
- A sorted counts file.

All output files are named using the prefix specified when running the pipeline. This ensures a consistent and organized output, facilitating subsequent data analysis.

## Contact

If you want to contact me, you can reach me at `byeongyeon_cho@hms.harvard.edu`.
