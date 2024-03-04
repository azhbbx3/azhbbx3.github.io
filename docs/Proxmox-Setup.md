### Ajout d'un nouvel utilisateur via l'interface graphique :

1. Connectez-vous à l'interface web de Proxmox.
2. Naviguez vers la vue "Datacenter".
3. Cliquez sur "Users" dans la barre latérale gauche.
4. Cliquez sur le bouton "Ajouter" en haut.
5. Remplissez les détails requis pour le nouvel utilisateur :
   - **Nom d'utilisateur:** [Entrez le nom d'utilisateur]
   - **Mot de passe:** [Entrez le mot de passe]
   - **Email:** [Entrez l'adresse e-mail]
   - **Permissions:** [Sélectionner les permissions]
6. Cliquez sur "OK" ou "Enregistrer" pour créer le nouvel utilisateur.

![Image 1](add%20user.png)
![Image 2](add%20user%202.png)

### Ajouter un Token ID dans l'interface graphique de Proxmox :
1. Connectez-vous à l'interface web de Proxmox.
2. Naviguer vers la vue "Datacenter".
3. Cliquez sur "Datacenter" dans la barre latérale gauche.
4. Cliquez sur l'onglet "Permissions".
5. Sélectionnez l'utilisateur pour lequel vous souhaitez ajouter un token ID dans la liste des utilisateurs.
6. Cliquez sur l'onglet "Permissions" pour l'utilisateur sélectionné.
7. Dans la section "API Tokens", cliquez sur le bouton "Create" (Créer).
8. Saisissez un nom descriptif pour le jeton dans le champ "Nom".
9. Cliquez sur le bouton "Créer" pour générer le jeton.
10. Copiez l'identifiant du jeton généré.
11. Cliquez sur le bouton "Fermer" pour terminer.
12. Vous avez maintenant ajouté avec succès un token ID pour l'utilisateur sélectionné dans l'interface graphique de Proxmox.

![Image 1](add%20token.png)
![Image 2](add%20token%202.png)

Veuillez noter que les étapes exactes peuvent varier légèrement en fonction de la version de Proxmox que vous utilisez, mais le processus général devrait être similaire.