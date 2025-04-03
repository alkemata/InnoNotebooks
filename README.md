# InnoNotebooks
A set of notebooks to investigate the SDG approach


# Updates
- extract_prompts now has all sdgs included.
-  patent_extract has now sql queries to load random texts, texts in each IPC class, texts in 10 groups of dates between the first and the last publication: still in test
- automatic transfer of the result to the ovh server for embedding and search
- patent number added, patent date added,
- extraction of limited number of characters directly in sql request to avoid high transfer load


# TODO

Patent data extraction analysis

-> load patent and keep x first characters (1000)
limit to A1
ok number of patent to requests
method to extract: ok random
ok ipc random on ipc ou cpc
random on lengths
ok random on publication date (maybe more ocr issues on older)
ok creation d'un fichier .conf avec ces parametres
requete des donnees et sauvegarde dans un fichier .dat.gz (forcer l'extension et la changer peut-etre)

-> extraction des données
ok creer ou charger un fichier de configuration .ext existant.
Input: conf filename
Dedans: nom du fichier source existant
Comment:
ok full length: modify - do it in previous step
Method d'extraction: keywords !!!!!!! important
ok Save data as .dat.gz (jsonl)
affichage de mini statistiques pour check rapide (sauvée dans .emet.conf)
 -> rajouter le nombre de dossiers par ipc en moyenne et l'écart type, le nombre d'ipc qui ne sont pas couverts

 modifier, tester les parametres

-> view of extraction results
Select and load config name
display config
display side by side extracted and original
option to display only difficult files (add flag in the file)
may be highlight text
checkbox to flag file : -> add flag
button to save th results

Output
master file with:
- patent nbr, extracts, flag "issue", initial length, length, date of publication, list of CPC.


SDG_prompts
-file with sdg_number, prompt.

Embedding, Indexing and search
load master file: only patent_nbr and extract.
indexing parameters to check (length of extracts)
Cleaning to check
indexing of patents extracts
save operation duration and size of database
embedding of sdg prompts
search paramers: knn
combined to check and compare
save SDG_nbr, file, with patent_nbr and score for each document

Results processing and human checking
display as it is
enter proper class: SGxx or nothing
for a given class: enter AI/reality: high score but wrong (HIGH), low score but right (LOW)
issue: wrong extract, general vocabulary, no context....
save these three parameters

Validation set:
take EP nbr, human classes and that's it

Score - Class relation
for each SDG class, display the score with colour blue the class is right, red is wrong. Ltpimize the parameters to get a separation on all classes

Relations between extraction failed and wrong classes.

