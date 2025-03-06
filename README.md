
### Bem vindo ao perfil de Miguel Victor 🉑

## Skills

![Skills](https://img.shields.io/badge/HTML5-E34826?style=for-the-badge&logo=html5&logoColor=black)
![Skills](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=pink)
![Skills](https://img.shields.io/badge/JavaScript-fcdf1e?style=for-the-badge&logo=javascript&logoColor=black)
![Skills](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=black)
![Skills](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=black)

💻 Desenvolvedor, apaixonado por aprender e compartilhar conhecimento no mundo da programação.

miguelldev@proton.me           

 ![Mail](https://img.shields.io/badge/ProtonMail-8B89CC?style=for-the-badge&logo=protonmail&logoColor=black) 

Estou atualmente desenvolvendo https://nevax.xyz

# GitHub Action for generating a contribution graph with a snake eating your contributions.
name: Generate Snake

# Controls when the action will run.
on:
  schedule:
      # every 12 hours
    - cron: "0 */12 * * *"

  # This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:
  
  # Also run on every push on the master branch
  push:
    branches:
    - main

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - name: Clone repo
        uses: actions/checkout@v3
    
      - name: Generate the snake files in './dist/'
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
            dist/github-contribution-grid-snake.gif?color_snake=aqua&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
           GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Show build status
        run: git status

      - name: Push new files to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
          commit_message: Update snake animations
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
