MCScanX
=========


Installation
-------------
	$wget -c https://github.com/wyp1125/MCScanX/archive/refs/heads/master.zip
	$unzip master.zip
	$cd MCScanx
	$make
  

Main programs
-------------
- Usage
MCscan2 reads in two data files: all.blast and all.gff. 
The all.gff file holds gene positions, following a tab-delimited format::
	chr#	gene	starting_position	ending_position	
	P57B    P57B.rpl10      358     853
	P57B    P57B.orf127a-2  1665    2049
	P57B    P57B.orf144a    3771    4206
	P57B    P57B.orf135a-2  4585    4993

The all.blast file is simply the direct BLASTP output of m8 format as following::
	$makeblastdb -in P57B.pep.fasta -dbtype prot -out P57B.pep
	$blastall -i P56A.pep.fasta -d P57B.pep -p blastp -e 0 -a 1 -F F -m 8 -o all.blast
	$makeblastdb -in P56A.pep.fasta -dbtype prot -out P56A.pep
	$blastall -i P57B.pep.fasta -d P56A.pep -p blastp -e 0 -a 1 -F F -m 8 -o all1.blast
	$cat all1.blast >>all.blast
	$MCScanX all -k 10 -g 0 -s 20 -e 10 -w 10 -b 0
	$cp ../MCScanX/v1.0.0/downstream_analyses/dual_synteny_plotter.* .
	$java dual_synteny_plotter -g all.gff -s all.collinearity -c control -o collinearity.png
	
.. image:: https://github.com/zxgsy520/bioanalysis/edit/main/compare/image/collinearity.png
        :alt: MCScanX flow char
