# ASHEs
ASHEs is a program written in C# that models the forward evolution of haplotypes from an ancestral state under different scenarios. Groups of haplotypes, either in multi-locus or binary format, are allowed to sort along Markov chains following random probability distributions.

Parameter value estimations, performance of genetic distance measures and alternate demographic histories can be evaluated by comparing randomized replications of user-specified evolutionary models with experimental data.

### Markov chains and the Wright-Fisher Model
In finite populations of constant size, the distribution of haplotype frequencies across generations fluctuates (drift) following random sampling probabilities (Wright –Fisher model, Fisher 1930, Wright 1931). Any new formed generation entirely replace the pre-existing one with the offspring randomly selecting their parents. In this process, the transition probabilities to the new state (j) depend only on the current state (i) of each haplotype and on the population effective size (N) according to the binomial function: Tij = (N j) (i/N)^j (1-i/N)^N-j.
In mathematics a process where new discrete states are reached from current states following random transition probabilities independently from the past pathways is called [Markov chain](http://en.wikipedia.com/wiki/Markov_chain).
ASHEs simulate haplotype states transitions under a Wright-Fisher model formulated in terms of Markov chains. (Montecarlo algorithm?) At each generation (t), any new haplotype is sampled randomly from the parental pool, stored in a temporary vector and a copy subsequently reintroduced in the parental pool. After a given number of samplings (k) the temporary pool will become the new generation of haplotypes {"(t+1)"} and processed n times (generations) in the same way (Figure 1). 

![](User Guide_hashes_userguide_fig1.jpg)
Figure 1. Flow chart of the basic Markov chain/Wright-Fisher algorithm implemented in ASHEs.

### Variable options
The values of different estimators related to the source population of haplotypes (X0) can be followed over generations: effective size (N), haplotype diversity (H), any haplotype frequency (p).

### Parameter options
The standard formulation of the Wright-Fisher model assumes stationarity, random mating and absence of mutation, selection, migration. ASHEs allows to vary some evolutionary parameters that extend the application of the Wright-Fisher model to realistic cases: the growth rate (g), expressed as increment rate = 1 ± g;  the mutation rate (µ); the number of migrants (Nm) evolving independently from the source population since generation t0.

## Modules
Two different approaches are available for simulations: 

# one-ancestral-population module (OAP)
# two-ancestral-population module (TAP).

### One-ancestral-population module (OAP)
In the OAP approach one can model the evolution of a single group of haplotypes and follow the fluctuation of a chosen variable (N, p, H) under evolutionary conditions defined by setting parameter options for 1+g, µ.

#### Randomly Generated grid

#### Downloaded data file

### Two-ancestral-populations module (TAP)
In the TPA approach the variation of both, population estimators (N, p, H) and distance measures (FST, DHS), can be followed over time. Two formulations of FST are implemented: FST, the standard fixation index (Wright 1921) and FST2, the unbiased measure of Weir & Cockerman (1984) as described in Michalakis & Excoffier (1996). DHS is a measure based on the amount and type of haplotypes shared by two diverging populations (Tofanelli et al. in press).
	
#### Randomly Generated grid 
 TODO

#### Downloaded data files
 TODO

## Installation 
 TODO

## Data format
ASHEs accepts haploid non-recombinant data in .txt, .arp, (.fa), .csv formats. This implies that it  handles uni-parentally transmitted markers of different genetic systems: Y-STRs, partial or complete mitochondrial DNA sequences,  UEPs (indels, SNPs or both).

## Input Files

### Text files (.txt)
Each row must correspond to one haplotype. Alleles at different loci are separated by a single whitespace. Headers, tags, points, commas, tabs must be avoided. Example text files are provided for multistate (STR.txt) and binary (UEP.txt) data.

### DNA sequence files (.arp, .fa)
ASHES loads aligned DNA sequences converting ARLEQUIN (.arp) or FASTA (.fa) format files directly into a binary format by matching nucleotides with a reference sequence. Example DNA sequence files are provided (Ref.arp, DNA.arp, Ref.fa, DNA.fa).

### Database entries (.csv)
Data records can be imported from .csv files. Each row must correspond to one haplotype with comma-separated alleles. Excel or other spreadsheet programs can be used to create or modify the CSV input file. CSV files can be opened and edited in any text editor.

### Missing Data (not yet implemented)
ASHES allows missing data. To mark data as missing, use “?”.  Missing data will not be used in calculations.

## Project design
Starting a new ASHEs session the first step is to design a new simulation project.  From the File menu select New Project and set options (Title, Data format, Model). Then, the ancestral population(s) of haplotypes must be loaded (File menu or yellow GroupX/Y iconas) or generated (Functions menu or white GroupX/Y iconas). Parameters, variables and graphic options can be set varying default values in the windows on the left side of ASHES page. The project can be saved in a .xml format by clicking on the “save project” button in the File menu. The project will be stored in the main directory with the given title name and can be re-loaded for subsequent simulations.
Each project describes the model of population history to be simulated over the chosen time window. 

## Output files
Outputs are saved in the same directory as the input file, in the form {"[input file name](input-file-name).csv"}. Each simulation will be given as a single row and t columns.

## Post-processing (R?)

The outputs can be opened with Microsoft Excel or OpenOffice Calc. Summary statistics of the simulated data (i.e. mean, median, SD, 95% CI) can be calculated from the CSV output format to be compared with the observed values. A model is accepted if the observed value falls within the tolerance interval of the simulated distribution or provides summary statistic values closer than alternative models to those given by the experimental data.

## Graphic interface

## Example session

### Performance of distance measures
The efficiency of two genetic distance DHS (Tofanelli et al. In press) and FST (Weir & Cockerman 1984) under different evolutionary scenarios (Table 1) has been tested by  ASHEs. Each computer simulation (200 iterations) modelled the increase rate over 200 generations of averaged DHS and FST values between diverging populations each evolving under reproductive isolation and constant size (Wright-Fisher model) from a source pool of 9-locus YSTR haplotypes (N=5,000; SIM1.csv). The impact on the two statistics of the number of migrants from a source population with Hx=0.815 was evaluated by simulating different values of Nm. The extent of the sampling error (measured as percent Coefficient of Variation or CV), and the linear relationship with time (expressed as both α, the angular coefficient and R2, the Pearson’s coefficient of regression) have been used as performance criteria. 

**Project**
Title: SIM1
Module: TAP
Data type: Multistate
GroupX: 5,000 9-locus YSTR haplotypes
Parameters
Nm: 10 or 100 or 1000
Mutation rate: 0.00185
Increment rate: 1
Iterations: 200
Generations: 200
Distance function: DHS or FST2
Output file: SIM1.csv
Variables
Calculate distance: true
Calculate group X P: false
Calculate group X H: false
Calculate group X N: false
Calculate group Y P: false
Calculate group Y H: false
Calculate group Y N: false

 (INSERT TABLE)

DHS performed much better than FST, being more linear with time (from 2 to 12 times higher α values) and having much lower variance (from 3,6 to 5 times lower CV values). Both the distributions show deviation from linearity (low R2 values) in the case of a marked founder effect (migrant size around 10). 

### Haplotype frequency fluctuations
We used ASHEs to test whether the differences in frequency between "Berber" (12,77%) and "Arabic" (18,78%) J1-M267 Y chromosomes are primarily a product of the Islamic expansion from Arabia since the 7th AD century or may they be accounted for by random fluctuations.
We calculated confidence intervals of the probability distributions of J1 frequencies  over the last 1,350 years (54 generations assuming 25 years per generation) from two source populations (GroupX0B, GroupX0A) showing the current frequency levels either in Berbers (p0B) or  Arabs (p0A). Before starting simulations the haplotype of choice in the data box should be clicked. In both cases the simulation gave observed J1 frequencies largely comprised in the confidence intervals expected by random fluctuations (Figure 2).

**Project**
Title: SIM2
Module: OAP
Data type: Binary
GroupX: 477 30-locus binary haplotypes
Parameters
Mutation rate: 1x10-8
Increment rate: 1.014
Iterations: 100
Generations: 54
Output file: SIM2.csv
Variables
Calculate distance: false
Calculate group X P: true
Calculate group X H: false
Calculate group X N: false

Figure 2. Random fluctuactions of Arab (in green) and Berber (in red) J1 frequencies over the last 54 generations: Mean values (thick line) and 95% CI intervals (dotted lines).

## References
* [Tofanelli, Sergio & Taglioli, Luca & Merlitti, Davide & Paoli, Giorgio. (2011). Tools which simulate the evolution of uni-parentally transmitted elements of the human genome. Journal of anthropological sciences = Rivista di antropologia : JASS / Istituto italiano di antropologia. 89. 201-19. 10.4436/jass.89017](https://www.researchgate.net/publication/51632143_Tools_which_simulate_the_evolution_of_uni-parentally_transmitted_elements_of_the_human_genome)
* Fisher RA (1930). _The Genetical Theory of Natural Selection. Oxford. Clarendon Press pp. 145.
* Michalakis Y., Excoffier L. (1996). A generic estimation of population subdivision using distances between alleles with special reference to microsatellite loci. Genetics 142:1061-1064.
* Tofanelli S, Bertoncini S, Castrì L, Luiselli D, Calafell F, Donati G, Paoli G (2009). On the origins and admixture of Malagasy: new evidence from high resolution analyses of paternal and maternal lineages. (submitted)
* Weir BS, Cockerham CC (1984). Estimating _F_-Statistics for the analysis of population structure. _Evolution_, 38: 1358–1370.
* Wright S (1921). Systems of mating. I. The biometric relations between offspring and parent. Genetics 6: 111-123.
* Wright S (1931). Evolution in Mendelian populations. Genetics 16: 97-159.


