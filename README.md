<img width="20%" height="20%" src="master_BLASTer.png">

# masterBLASTer
A SLURM tool for performing parallel BLAST searches.

Requirements:
* HPC cluster running SLURM job scheduler
* BLAST
* Python 3.5+ (with pandas and numpy packages)
* Preindexed BLAST protein database

## DESCRIPTION:
This tool provides a way of submitting parallel BLASTp searches from a large protein FASTA file. It consists of a set of SLURM .srun files that each perform a different step. 

The three basic steps are:
1) Split the FASTA file into several smaller blocks
2) Perform seperate BLAST searches with each block
3) Combine the results and outputing a result file

## INSTRUCTIONS:
1) Copy all tool files into the project's working directory.
2) Edit the config.sh file to match the project parameters. These will be your SLURM account, SLURM partition, the project FASTA file, the blast database to use, the output file, and the number of blocks to split the file into.
3) Start the project3_master.srun file supplying the account and partition to run the master task from.
Example: 'sbatch -A youraccount -p yourpartition project3_master.srun'
4) The master SLURM script will direct the rest of the program. In your SLURM queue you should see the master job as well as the helper jobs (they will be held until the previous step completes). Simply, wait until all jobs are finished and the results will be in your project directory with the specified output file name.

## RESULTS:
The tool currently returns a tab-delimited file that includes each unique gene hit from the database and the number of hits for each gene sorted in descending order.

## Sample File
For testing, a sample FASTA file is provided (some.pep) as well as an example output (results.tsv)


