# Installation de Terraform sur Windows

## Prérequis
Avant d'installer Terraform sur Windows, assurez-vous d'avoir les prérequis suivants :
- Accès administratif à votre PC.
- Connexion internet fiable.
- Compréhension de base de l'interface en ligne de commande de votre système d'exploitation.

## Étapes pour Installer Terraform

### Étape 1: Télécharger Terraform
1. Ouvrez votre navigateur web et accédez à la [page de téléchargements de Terraform](https://www.terraform.io/downloads.html).
2. Sélectionnez la version appropriée de Terraform pour votre système d'exploitation. Pour PC, vous pouvez choisir la version 32 bits ou 64 bits, en fonction de l'architecture de votre système.
3. Cliquez sur le lien de téléchargement pour démarrer le processus de téléchargement.

### Étape 2: Extraire le Binaire Terraform
1. Une fois le téléchargement terminé, localisez le fichier zip Terraform téléchargé dans votre dossier de téléchargements ou à l'emplacement que vous avez spécifié.
2. Cliquez avec le bouton droit sur le fichier zip et sélectionnez "Extraire tout...".
3. Choisissez le dossier de destination où vous souhaitez extraire les fichiers binaires Terraform.
4. Cliquez sur "Extraire" pour extraire les fichiers dans le dossier de destination choisi.

### Étape 3: Ajouter Terraform à votre Variable d'Environnement PATH
1. Ouvrez l'Explorateur de fichiers et accédez au dossier où vous avez extrait les fichiers binaires Terraform.
2. Copiez le chemin de ce dossier.

#### Sur Windows
1. Cliquez avec le bouton droit sur le bouton "Démarrer" et sélectionnez "Propriétés".
2. Cliquez sur "Paramètres système avancés" sur le côté gauche.
3. Dans la fenêtre Propriétés du système, cliquez sur le bouton "Variables d'environnement...".
4. Sous "Variables système", sélectionnez la variable "Path" et cliquez sur "Modifier...".
5. Cliquez sur "Nouveau" et collez le chemin du dossier contenant les fichiers binaires Terraform.
6. Cliquez sur "OK" pour enregistrer les modifications.

### Étape 4: Vérifier l'Installation
1. Ouvrez une nouvelle fenêtre d'invite de commandes ou terminal.
2. Tapez `terraform -v` et appuyez sur Entrée.
3. Si l'installation a réussi, vous devriez voir la version de Terraform affichée dans la sortie.

## Conclusion
Félicitations ! Vous avez réussi à installer Terraform sur votre PC. Vous pouvez maintenant commencer à utiliser Terraform pour gérer votre infrastructure sous forme de code.

Pour plus d'informations sur la prise en main de Terraform, consultez la [documentation officielle de Terraform](https://learn.hashicorp.com/terraform).
