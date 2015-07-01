ID: 01
Title: Submit a completely novel simple allele

Description
Curator submits a completely novel simple allele to the Allele Registry.


####Actors
- Curation Admin - a user that has the authority to register new alleles in the Allele Registry
- Curation Application - a system that stores curation evidence related to allele identifiers from the Allele Registry.
- Allele Registry - a service that is the single authority for canonical allele identifiers and the canonicalization engine implementation for registering, mapping, aligning and canonicalizing various allele representations.

####Pre-conditions
- One of either of the following minimal data sets for an allele representation are provided for registring an allele
-- Reference seqeunce identifier and associated HGVS expression. (e.g. NM_007294.3:c.5297T>G or U14680.1:n.5416T>G)
-- Genome build assembly, chromosome, genomic coordinates, reference and alternate allele. (e.g. GRCh37, 17, 41203114, 41203115, A, C)

- The allele representation to be registered does not previously exist in the Allele Registry, nor does the canonical representation of the allele representation.

####Steps
1. Curation admin requests a formal allele identifier from the Curation Application in order to capture specific evidence from one or more publications.
2. The Curation application requests an allele identifier from the Allele Registry using one of the minimal required data sets (see pre-conditions) for representing an allele.
3. The Allele Registry determines that the allele representation specified does not already exist and registers it. 
4. The Allele Registry returns the URI of the canonical allele (or universal identifier) to the Curation Application.
5. The Curation Application captures the universal stable allele identifier and presents all relevant forms of the allele to the Curation admin.


####Post-conditions
- The Curation Application captures a universal stable identifier authorized by the Allele Registry for the original allele representation submitted by the Curation Admin.  
- The Curation Application would be responsible for keepi

####Exceptions
- HGVS is invalid
- Invalid reference sequence identifier or reference sequence not loaded in repository.

####Questions/Comments
- Is the Allele Registry responsible for capturing and retaining the originally submitted data that resolved to a specific allele URI?  (I think not, it should be the responsibility of systems external to the Allele Registry to maintain submission tracking kinds of behavior.  However, wouldn't the original request be needed for provenance sake?  And, if so, then would we not need to capture other requested representations that resolved to it?)
