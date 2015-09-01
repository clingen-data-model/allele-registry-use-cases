##Implementer Topics

###Generating & Storing "All v. Submission Only" Allele Instance(s)

When an allele instance is submitted to the allele registry, it may generate a new canonical allele.  Furthermore, there are usually other allele instances that can be generated automatically from that canonical allele.  For example, if a nucleotide allele is submitted on a particular version of a chromosome, it would be possible to generate nucleotide alleles representing that allele on other versions of the chromsome, and also to generate alleles on any transcripts that span the genomic allele.

An allele registry can operate in one of two modes at the discretion of the implementor:

1) The allele registry will generate all possible allele instances at the time an allele instance is registered. (early instance creation)

2) The allele registry will not generate any allele instances at the time of registration other than the one that was submitted. (lazy instance creation)

Other possiblities exist, but for these two are sufficient to discuss the implementation issues.

Issue 1: Efficiency

For any given nucleotide allele, several allele instances are likely to be created.  In some cases, as many as fifteen instances may be created.  If responsiveness of the submission service is the priority, the time taken to create instances at submission may be unacceptable.   However, if instances are not created at submission, they will need to be lazily generated when a service requesting all available instances for a canonical allele is invoked.    The correct place to absorb this time will depend on the use case for the specific allele registry. For instance, a common idiom may involve submitting an instance (producing a canonical allele) and then immediately querying for the full set of instances for that canonical allele (for instance to annotate a list of alleles).  In such a case, efficiency does not provide an incentive one direction or the other.

Issue 2: Searchability

If allele instances are generated lazily, then searchability of the allele registry is reduced.   Specifically, if queries are allowed by transcript or region-type, these queries will not find alleles that have been entered as genomic instances, but for which transcript alleles have not been generated, because none have yet been asked for.  One possiblity would be to generate transcript alleles at the time of the transcript based query, but this would recall locating all the genomic alleles that intersect the transcript, likely requiring significant performance tuning.

Issue 3: Reference Updates

If early instance creation is employed, the registry enforces that all known instances of a canonical allele are created and entered into the registry.  If a new reference sequence is loaded into the registry, canonical alleles in that sequence must be updated to include any instances on that new reference sequence.

###Generating Amino Acid Alleles from Nucleotide Alleles

When a nucleotide allele is submitted to the allele registry, and a new canonical allele is generated, it is possible for any associated amino acid alleles to be generated as well.   The issues involved are similar to the early/lazy instance creation for allele instances, but also include the difficulty of associating amino acid and nucleotide alleles.

If amino acids alleles are generated at the time of a genomic allele submission, then the correct association links can be generated automatically by the allele registry.  If the allele registry does not create such links, then it will need to define the correct procedure for users to either create amino acid alleles from a nucleotide allele, or separately enter amino acid alleles and link them to a nucelotide allele.    In either case, the searchability of the registry is not high;  it is impossible to distinguish between nucleotide alleles that are not assocaited with an amino acid allele, with those that are, but for which the amino acid allele has not yet been created, or for which the amino acid allele has been created, but has not been explicitly associated with the nucleotide allele.

###Approach(es) to Handling Left-Right Issue at Submission

TODO L. Babb
Note that this is a special case of Generating & Storing?

###Canonicalization



