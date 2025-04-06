# InnoNotebooks
A set of notebooks to investigate the SDG approach on the TIP platform:
- exzract_sdg.ipynb: the list of SDGs wiht some cleanup. It is asave as a pickle dataframe
- patent_extract_analyis: this notebook has the purpose to analyse the xtraction of interesting data from the patents, especially the background and the technical field. Different algorithms are tested and the result can vizualised and checked.
- Search.ipnyb: this is juste an interface with the OVH server and the embedding and search code runnning on it.Basically, ssh commands.
- Process_results: the data are loaded from the OVH server and vizualized and compared. The purpose is both to create a test set for the classification algorithm and to test it.

# installation
These notebooks are conceived to run on the TIP platform and to interface with the OVH server with elasticsearch.
Several steps are required for the installation:
- cloning the repository in TIP:
  git clone https://github.com/alkemata/InnoNotebooks
- creating a SSH key for accessing the OVH server without password:
  Open a terminal: This is your command-line interface.
Use the ssh-keygen command:
The basic command is: ssh-keygen
For stronger security, consider using ED25519 keys: ssh-keygen -t ed25519
You can also specify the bit length for RSA keys (e.g., 4096 bits): ssh-keygen -t rsa -b 4096
Follow the prompts:
You'll be asked where to save the keys. The default location (~/.ssh/id_rsa or ~/.ssh/id_ed25519) is usually fine.
You'll be prompted to enter a passphrase. While optional, a passphrase adds an extra layer of security. If someone gains access to your private key, they'll still need the passphrase.
After completing the prompts, you'll have two files:
id_rsa or id_ed25519 (or whatever name you chose): This is your private key. Keep this file secure!
id_rsa.pub or id_ed25519.pub: This is your public key.
2. Copying the Public Key to the Remote Server:
      Using ssh-copy-id (recommended):
    This is the easiest way to copy your public key.
    The command is: ssh-copy-id user@remote_host
    Replace user with your username on the remote server.
    Replace remote_host with the IP address or hostname of the remote server.
    You'll be prompted for your password on the remote server once.
    This command will append the contents of your public key file to the remote servers ~/.ssh/authorized_keys file.
    Manual copying:
    If ssh-copy-id is not available, you can manually copy the public key.
    Use cat ~/.ssh/id_rsa.pub (or the appropriate public key file) to display the contents of your public key.
    Copy the output.
    SSH into the remote server: ssh user@remote_host
    Create the ~/.ssh directory if it doesn't exist: mkdir -p ~/.ssh
    Create or append to the ~/.ssh/authorized_keys file: echo "your_public_key" >> ~/.ssh/authorized_keys
    Replace your_public_key with the copied public key.
    It is very important that the ~/.ssh/authorized_keys file has the correct permissions. The permissions should be set to 600. So after the file has been created, run the command: chmod 600 ~/.ssh/authorized_keys
- creatng a ".env" file with the following parameters:
server= the IP of the OVH server
username= the username on the OVH server
key= the path to the private SSH key.


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

