### Configuration Terraform : Gestion de l'environnement virtuel Proxmox

## Étape 1 : Configuration de Terraform
Tout d'abord, configurons notre fichier de configuration Terraform `(provider.tf)` pour définir la version de Terraform et les fournisseurs requis.

```hcl
terraform {
  required_version = ">=0.14"
  required_providers {
    proxmox = {
      source = "telmate/proxmox"
      version = "2.9.11"
    }
  }
}
```

Dans ce bloc :

- Nous spécifions la version minimale requise de Terraform (`0.14` ou plus).
- Nous déclarons les fournisseurs requis, y compris `proxmox`, en spécifiant sa source et sa version.

### Étape 2 : Configuration du fournisseur Proxmox

Ensuite, configurons le fournisseur Proxmox pour qu'il communique avec notre instance PVE.

```hcl
provider "proxmox" {
  pm_tls_insecure = true
  pm_api_url = var.proxmox_api_url
  pm_api_token_secret = var.proxmox_api_token_secret
  pm_api_token_id = var.proxmox_api_token_id
  pm_log_enable = true
  pm_log_file   = "terraform-plugin-proxmox.log"
  pm_debug      = true
  pm_log_levels = {
    _default    = "debug"
    _capturelog = ""
  }
}
```

Voici ce que fait chaque paramètre de configuration :

- `pm_tls_insecure` : Désactive la vérification des certificats TLS. A utiliser avec précaution, typiquement pour les environnements de test.
- `pm_api_url = var.proxmox_api_url` : Variable définie dans un autre fichier.  Spécifie l'URL du point de terminaison de l'API Proxmox.
- `pm_api_token_secret = var.proxmox_api_token_secret` : Variable définie dans un autre fichier.  Fournit la partie secrète du jeton API pour l'authentification.
- `pm_api_token_id = var.proxmox_api_token_id` : Variable définie dans un autre fichier.  Spécifie la partie ID du jeton API pour l'authentification.
- `pm_log_enable` : Active la journalisation pour le fournisseur Proxmox.
- `pm_log_file` : Spécifie le fichier où les logs seront écrits.
- `pm_debug` : Active le mode debug pour la journalisation verbeuse.
- `pm_log_levels` : Définit les niveaux de logs pour les différents composants.

Avec cette configuration Terraform, nous sommes maintenant prêts à gérer nos ressources de l'environnement virtuel Proxmox de manière programmatique. Restez à l'écoute pour d'autres tutoriels sur le provisionnement et la gestion des ressources PVE à l'aide de Terraform !

---

## Étape 3 : Définir la ressource de machine virtuelle Proxmox
Commençons par définir la ressource de machine virtuelle Proxmox dans notre configuration Terraform `(main.tf)`.

```hcl
resource "proxmox_vm_qemu" "cloundint-terraform" {
  target_node = "dve01"
  desc = "cloudint-terraform3"
  count = 1

  clone = "ubuntu-cloud"

  agent = 0
  os_type = "cloud-init"

  cores = 1
  sockets = 1
  cpu = "host"
  memory = 2048
  name = "cloudinit-terraform-0${count.index +1}"
  cloudinit_cdrom_storage = "local-lvm"
  scsihw = "virtio-scsi-single"
  bootdisk = "scsi0"
  
  disk {
    storage = "local-lvm"
    size = "20G"
    type = "scsi"
  }
  sshkeys = <<EOF
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDWWFtzhsRIpg3PRKGjYZl4ugZNpC2a2llyGPSNLEg3IQs93hCSxwF7Z4P9U28I8+eaBcY7Qgq0lEu9yJI7YNkyte9kyyER655de0uwa+STMSHkarx74/3Q+/q4sxk+qwDu19fT1fIoMNGbXZQkKbsAzcV7Vn6L+0MoQhFQJbXAdx5WP/v5dyY/biwLpxA58CyK6m39w6ZY56lZRBWAZzev+tTaKeJxVPZej3uQ2YS2+V6a9EYVYYiFlHZUk095WmnI717UZqimwaNLvyOBqDCAIUIdixaC4ugafTQl0C+qdR4iZsfGRwvmRvIXkNxg4XmsoMfSBcYyIXOMKFwW95iOy3shhqWLl9lGJjXVq8Iyc9yKi0Ux1DbN3HCUYvDsVL0NO7PxwUOxCrJkwEVs047uj/uVmabTkcVygQbOzbx4Ci/sV4y6wxZ3VbUkyBjy8izTSC4kfC/rH2gKLiD1gQwUIxhBtN8BZMH3rntcC9uLabBmJsjvNx6U0X/FPivwrck= root@dve01
    EOF
}
```


Voici le détail de la configuration :

- `target_node` : Spécifie le noeud où la VM sera créée.
- `desc` : Fournit une description pour la VM.
- `count` : Spécifie le nombre d'instances à créer (dans ce cas, 1).
- `clone` : Spécifie le modèle à utiliser pour cloner la VM.
- `agent` : Désactive l'agent invité Proxmox.
- `os_type` : Spécifie le type d'OS pour la VM.
- `cores`, `sockets`, `cpu`, `memory` : Définit les paramètres de CPU et de mémoire pour la VM.
- `name` : Spécifie le nom de la VM.
- `cloudinit_cdrom_storage` : Spécifie le stockage du CD-ROM de cloud-init.
- `scsihw` : Spécifie le type de contrôleur SCSI.
- `bootdisk` : Spécifie le disque de démarrage de la VM.
- `disk` : Définit la configuration du disque pour la VM.
- `sshkeys` : Spécifie la (les) clé(s) publique(s) SSH pour accéder à la VM.

## Étape 4 : Gestion des variables d'authentification avec Terraform

Dans ce fichier `credentials.tfvars`, nous stockons les informations sensibles telles que l'URL du point de terminaison de l'API Proxmox, l'ID du jeton API et la partie secrète du jeton API pour l'authentification. Il est important de garder ces informations confidentielles et de ne pas les partager publiquement.

```` hcl
proxmos_api_url = "https://192.168.100.50:8006/api2/json"
proxmos_api_token_id = "teraform_user@pam!terraform"
proxmox_api_token_secret = "80e183d4-9751-4d1c-96f3-9f6065299bdb"
````


- `proxmos_api_url` : Cette variable contient l'URL du point de terminaison de l'API Proxmox. Elle spécifie l'emplacement où Terraform doit envoyer les requêtes pour interagir avec l'API Proxmox.

- `proxmos_api_token_id` : Cette variable contient la partie ID du jeton API pour l'authentification. Le jeton API est utilisé par Terraform pour s'authentifier auprès de Proxmox et exécuter des opérations sur les ressources.

- `proxmox_api_token_secret` : Cette variable contient la partie secrète du jeton API pour l'authentification. Il s'agit d'une information sensible et confidentielle qui doit être protégée. Cette partie du jeton est utilisée en conjonction avec l'ID du jeton pour s'authentifier auprès de Proxmox.

Ces variables sont définies dans un fichier séparé (`credentials.tfvars`) pour faciliter la gestion des informations sensibles et leur séparation du code source principal. Il est recommandé de ne pas les inclure dans le code source partagé ou versionné publiquement, mais de les stocker de manière sécurisée et de les gérer avec précaution.



# Conclusion

Avec cette configuration Terraform, nous avons défini les ressources nécessaires pour créer une machine virtuelle dans l'environnement virtuel Proxmox. L'exécution de `terraform apply` provisionnera la VM selon ces paramètres.

Restez à l'écoute pour d'autres tutoriels sur la gestion des ressources PVE à l'aide de Terraform !

---

| Column 1       | Column 2       | Column 3       |
| -------------- | -------------- | -------------- |
| Lorem ipsum dolor sit amet, consectetur adipiscing elit. | Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. | Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. |
| Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore | eu fugiat nulla pariatur. | Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. |


```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```