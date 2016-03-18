# secmake

Tool to create `.sec` files from `.pdb`, `.dssp` or `.wolf` files.

## About

A `.sec` file describes the secondary structure (SS) elements of protein structures. These files are currently required by some of the tools in the [cath-tools](http://www.github.com/UCLOrengoGroup/cath-tools) project.

We are currently working on clearing the licensing for this code to be included as open source. In the meantime, this project contains some [pre-compiled binaries](binaries/) for people to use.

## Usage 

```
$ secmake 
** secmake ** (branch: trunk, r18211, compile time: 12:19:20 Mar 18 2016)

Generates the sec and/or grath file for a given structure from the appropriate PDB and DSSP/WOLF files

Usage:
secmake [options]

Mandatory arguments to long options are mandatory for short options too.

 -l, --list=LISTFILE       Read a list of parameters for processing structures from the file LISTFILE.
                           Each line of this file should contain the four parameters for one structure:
                             PDBFILE WOLFFILE STEM STRUCID
 -p, --pdb=PDBFILE         Read the input PDB file from PDBFILE.
 -d, --dssp=DSSPFILE       Read the input dssp file from DSSPFILE.
 -w, --wolf=WOLFFILE       Read the input wolf file from WOLFFILE.
 -s, --sec=SECFILE         Output a sec file (as used by SSAP) to SECFILE.
 -g, --grath=GRATHFILE     Output a grath file (as used by CATHEDRAL) to GRATHFILE.
 -o, --outstem=STEM        Output a sec file to STEM.sec and a grath file to STEM.gth.
 -n, --nochop              Don't chop bent helices.
                           The default behaviour is to chop bent helices.
 -i, --id=STRUCID          The ID of the structure to place in the grath file (eg 1cukA01).


sec format is:

[FOREACH (SEC STRUCT) {]
  sec_strut_ctr sec_strut_type * start_residue stop_residue midpoint_x midpoint_y midpoint_z direction_x direction_y direction_z
  [FOREACH (LATER STRUCTURE) {] planar_angle_between_dirns_x planar_angle_between_dirns_y planar_angle_between_dirns_z [}]
[}]

Example usages :
secmake -l /cath/people/gandhi/listfile.txt
secmake -p /cath/data/current/pdb/1cukA01 -w /cath/data/current/wolf/1cukA01.wolf -g ~/1cukA01.gth -i 1cukA01

Example listfile entries:
/cath/data/latest_release/pdb/1cs8A /cath/data/latest_release/wolf/1cs8A.wolf /cath/people/beethoven/myfile 1cs1fseF00 1fseF00.wolf 1fseF00 1fseF00
```
