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
        uses: agence-adeliom/github-actions/.github/workflows/callable-wordpress-dependabot-update.yml@main
        with:
            theme: "theme-name"
            php: 8.0
            node: 16
```

Les workflow qui ne commencent pas par `callable-` peuvent être directement copiés dans votre projet pour aller plus vite.  
Il faut juste bien penser à mettre à jour les valeurs renseignées dans la propriété
`with`.