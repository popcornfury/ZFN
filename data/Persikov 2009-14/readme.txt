How to use the pre-trained model files to test any protein-DNA pair:


MODEL FILE DOWNLOAD

If you would like to test our pre-trained SVM models on your own data,
you can use our pre-trained model files for the linear and polynomial
SVMs: SVMl.mod or SVMp.mod, respectively.


SVM-LIGHT

The model files can be used with SVM-light.
You can download and install the SVM-light from http://svmlight.joachims.org/.
To make predictions on your test examples, you will need the svm_classify program, a model_file (either SVMl.mod or SVMp.mod) and an example_file (containing information on your testing sequences).  The SVM-light classification module can be called as:

svm_classify [options] example_file model_file output_file


FEATURE VECTOR REPRESENTATION

We use the canonical zinc finger binding model to map each zinc finger-DNA contact to a feature number. In each zinc finger, the four amino acid positions that contact DNA are called –1, 2, 3, and 6 (as numbered from the start of the alpha-helix). We use the this model to represent each protein-DNA complex by a feature vector x = {x_abc}, where x_abc=1 for every amino acid 'a' from {A,C,D,...,Y} interacting with base 'b' from {a,c,g,t} at contact position 'c'. This representation scheme leads to a feature space containing 320 dimensions representing all possible abc combinations (20 amino acids x 4 bases x 4 contacts). Therefore, each 'abc' combination can be represented as a number in (1,320) range according to the conversion table:

Conversion table from SVM features to amino acid - nucleotide contacts. 
Canonials contacts are listed as (see Fig 1 at Persikov et al., 2008):
01 - between amino acid a6 and nucleotide b1
02 - between amino acid a3 and nucleotide b2
03 - between amino acid a-1 and nucleotide b3
04 - between amino acid a2 and nucleotide b4'

  1 01Aa
  2 01Ac
  3 01Ag
  4 01At
  5 01Ca
...
316 04Wt
317 04Ya
318 04Yc
319 04Yg
320 04Yt

Finally, for the SVM-light input, each tested zinc finger-DNA pair should be represented as a feature vector recorded as a single line in the example_file. It is of the following format:

<line> .=. <target> <feature>:<value> <feature>:<value> ... <feature>:<value> # <info>

In classification mode, the target value denotes the class of the example. +1 as the target value marks a positive example, -1 a negative example respectively. Feature/value pairs MUST be ordered by increasing feature number. Features with value zero are normally skipped. The string <info> can be used to pass additional information to the kernel (e.g. non feature vector data). Check the SVM-light FAQ for more details. So, for example, the following line specifies a negative example for which features 3, 59, 94 and 318 have the value 1:

-1 3:1 59:1 94:1 318:1 # abcdef


EXPERIMENTAL DATABASE DOWNLOAD

We have also made available for download the database of experimental data collected from 25 individual manuscripts published in 1990 - 2005 and from the Protein Data Dank. This archive is password-protected. You can request the password by contacting us. Each line in the database represents one experiment including fields: source - data origin; dna - DNA sequence; zf - number of zinc fingers in protein; f1-fN - sequnces of corresponding zinc finger regions; ex - type of example: + for binding, - for non-binding, Kd - for experimentally measured dissociation constant, and > for comparative examples when binding of sequence A is compared to the subsequently listed sequence B. Please consult the list of sources for all individual references.


CONTACT US

To give feedback or to send your comments or suggestions please email us: persikov@princeton.edu
