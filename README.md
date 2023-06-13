Ce repository contient des [Workflow Github Actions](https://docs.github.com/en/actions/using-workflows/about-workflows)
réutilisables pour les projets. 

[Reusing Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

Les fichiers dans le repertoire `.github/workflows` sont divisé en deux sortes:
- Ceux qui commencent par `callable-`
- Ceux qui ne commencent pas par `callable-`

Pour appeler une action dans un workflow, il suffit de définir un job de la 
manière suivante :

```yaml
jobs:
    myjob:
        uses: agence-adeliom/github-actions/.github/workflows/deployer-symfony.yml@main
        with:
            php: 8.1
            node: 18
```

Les workflow qui ne commencent pas par `callable-` peuvent être directement copiés dans votre projet pour aller plus vite.  
Il faut juste bien penser à mettre à jour les valeurs renseignées dans les paramètres des propriétés
`with` ou `env`.

## Liste des Workflows disponibles

### Dependabot
- `dependabot-approve-merge` - Approve et fusionne les Pulls Requests de Dependabot automatiquement

### Deployer
- `deployer-deploy-only` - Deploy un site vers un serveur distant en passant par une connexion SSH

### Symfony
- `symfony-dependabot-update` - Approuve et merge les PR de dependabot après
  que le build du site Symfony a fonctionné
- `symfony-deployer` - Ajoute un workflow de déployment lors du push sur une
branch définie
- `symfony-deployer-manual` - Ajoute un workflow de déployment qui peut être
  déclenché à la mani depuis l'interface de github.com

### Lumberjack
- `lumberjack-dependabot-update` - Approuve et merge les PR de dependabot après
  que le build du site WP a fonctionné
- `lumberjack-deployer` - Ajoute un workflow de déployment lors du push sur une
  branch définie
- `lumberjack-deployer-manual` - Ajoute un workflow de déployment qui peut être
  déclenché à la mani depuis l'interface de github.com

## Utilisation avec WordPress

### Liste des paramètres

#### `theme`
type: `string`
required: `false`
default: `"adeliom"`  
Nom du dossier de thème WordPress utilisé ex: "twentytwelve"  
#### `php`
type: `string`
required: `false`
default: `"8.1"`  
Version de PHP utilisé sur le thème
#### `node`
type: `string`
required: `false`
default: `"18"`  
Version de Node utilisée pour compiler les assets dans le thème
#### `themes_path`
type: `string`
required: `false`
default: `"web/app/themes"`  
Chemin vers le thème si différent d'une architecture lumberjack.
#### `working-directory`
type: `string`
required: `false`
default: `"."`  
Chemin vers le dossier ou sera configuré les plugins payant
#### `use-node`
type: `boolean`
required: `false`
default: `true`  
Sur les anciens projets qui n'utilisent pas nodeJS, permet de contourner certains steps de compilation obligatoire en temps normal

## Utilisation des actions dependabot

### Liste des paramètres

#### `merge_type`
type: `string`
required: `false`
default: `"merge"`  
Permet de savoir quelle stratégie de fusion utiliser. 
`merge` va créer un commit de merge en plus du/des commit(s) de la PR.
`rebase` va rebaser le(s) commit(s) sur la branche, comme si la PR était venu s'appliquer directement à la suite du denier commit de la branch par défaut
`squash` va regrouper le(s) commit(s) de la PR en un seul et rebaser ce commit à la suite du denier commit de la branch par défaut.
