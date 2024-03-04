# Installation de Terraform sur Linux

## Prérequis
Avant d'installer Terraform sur Linux, assurez-vous d'avoir les prérequis suivants :
- Accès administratif à votre système Linux.
- Connexion internet fiable.
- Compréhension de base de l'utilisation de l'interface en ligne de commande.

## Étapes pour Installer Terraform

### Étape 1: Télécharger Terraform
1. Ouvrez une fenêtre de terminal sur votre système Linux.
2. Naviguez jusqu'au répertoire où vous souhaitez télécharger Terraform.
3. Utilisez `wget` ou `curl` pour télécharger le binaire Terraform. Par exemple :
    ```bash
    wget https://releases.hashicorp.com/terraform/<VERSION>/terraform_<VERSION>_linux_amd64.zip
    ```
    Remplacez `<VERSION>` par la version souhaitée de Terraform.
4. Alternativement, vous pouvez également télécharger manuellement le binaire Terraform à partir de la [page de téléchargements officielle de Terraform](https://www.terraform.io/downloads.html).

### Étape 2: Extraire le Binaire Terraform
1. Une fois le téléchargement terminé, naviguez jusqu'au répertoire où se trouve le fichier zip Terraform.
2. Utilisez la commande suivante pour extraire le binaire Terraform :
    ```bash
    unzip terraform_<VERSION>_linux_amd64.zip
    ```
    Remplacez `<VERSION>` par la version de Terraform que vous avez téléchargée.
3. Cela extraira le binaire Terraform (`terraform`) dans le répertoire actuel.

### Étape 3: Déplacer le Binaire Terraform dans un Répertoire de votre Variable PATH
1. Déterminez un répertoire où vous souhaitez stocker le binaire Terraform. Les choix courants incluent `/usr/local/bin` ou `~/bin`.
2. Déplacez le binaire Terraform dans le répertoire choisi :
    ```bash
    sudo mv terraform /usr/local/bin/
    ```
    Si vous avez choisi un répertoire différent, remplacez `/usr/local/bin/` par le chemin approprié.
3. Assurez-vous que le répertoire est inclus dans votre variable d'environnement PATH. Vous pouvez vérifier cela en tapant `echo $PATH` dans le terminal.

### Étape 4: Vérifier l'Installation
1. Ouvrez une nouvelle fenêtre de terminal ou tapez `source ~/.bashrc` (ou `source ~/.bash_profile` si vous utilisez Bash) pour rafraîchir votre shell.
2. Tapez `terraform -v` et appuyez sur Entrée.
3. Si l'installation a réussi, vous devriez voir la version de Terraform affichée dans la sortie.

## Conclusion
Félicitations ! Vous avez réussi à installer Terraform sur votre système Linux. Vous pouvez maintenant commencer à utiliser Terraform pour gérer votre infrastructure sous forme de code.

Pour plus d'informations sur la prise en main de Terraform, consultez la [documentation officielle de Terraform](https://learn.hashicorp.com/terraform).
