> File includes only work if its starts & end with a html comment 
>
> to avoid rendering Usage Block we have used `\!`. make sure to use only `!` to render the file include.

Inline Includes & Reusable includes dose the same work. but this can come in handy when you are generating template & saving it in the same file
it preserves include comment and will be parsed again when Re-generating the template & contents of that include will be updated

```
<\!-- START file.md --> 
<\!-- END file.md --> 
```

---

## Local File With Relative Path
Include a file from the current file's location 

### Usage :

<pre>
<\!-- START ./parts/license.md -->

<\!-- END ./parts/license.md -->
</pre>

<details> 
<summary>Output :</summary>

<pre>
<!-- START ./parts/license.md -->
## 📜  License & Conduct
- [****]() © [Varun Sridharan](website)
- [Code of Conduct]()
<!-- END ./parts/license.md -->
</pre>

</details>

---
## Local File With Absolute Path
Include a file located inside this repository

### Usage :

<pre>
<\!-- START templates/file-includes/parts/feedback.md -->

<\!-- END templates/file-includes/parts/feedback.md -->
</pre>

<details> 
<summary>Output :</summary>

<pre>
<!-- START templates/file-includes/parts/feedback.md -->
## 📣 Feedback
- ⭐ This repository if this project helped you! :wink:
- Create An [🔧 Issue](https://github.com/PavanMudigonda/action-dynamic-readme/issues/) if you need help / found a bug
<!-- END templates/file-includes/parts/feedback.md -->
</pre>

</details>

---
## Include File Inside Codeblock
dynamic-template.yml github action yaml file which in in this repository will be included below. its not recomended to use reusable include inside codeblock. but if you do want to have it. then use the `[code:yml]` to avoid showing include comment inside codeblock

### Usage :

<pre>
<\!-- START [code:yml] .github/workflows/dynamic-template.yml -->
<\!-- END [code:yml] .github/workflows/dynamic-template.yml -->
</pre>

<details> 
<summary>Output :</summary>

<!-- START [code:yml] .github/workflows/dynamic-template.yml -->
```yml
name: Dynamic Template

on:
  push:
    paths:
      - templates/**
      - .github/markdown-templates/**
      - .github/scripts/**
      - README.md
    branches:
      - main
  workflow_dispatch:

jobs:
  update_templates:
    name: "Update Templates"
    runs-on: ubuntu-latest
    steps:
      - name: "📥  Fetching Repository Contents"
        uses: actions/checkout@main

      - name: "💾  Github Repository Metadata"
        uses: varunsridharan/action-repository-meta@main
        env:
          GITHUB_TOKEN: 

      - name: "Setup PHP with pecl extension"
        uses: shivammathur/setup-php@v2
        with:
          php-version: '7.4'

      - name: "Regenerate Templates Files"
        run: php .github/scripts/create-markdown.php

      - name: "Updated Generated Template"
        run: |
          git config --global user.email "githubactionbot@gmail.com"
          git config --global user.name "Github Action Bot"
          git add -f ./templates/**
          if [ "$(git status --porcelain)" != "" ]; then
            git commit -m "Template Files Regenerated"
            git push "https://x-access-token:$GITHUB_TOKEN@github.com/$GITHUB_REPOSITORY"
          fi
        env:
          GITHUB_TOKEN: 

      - name: "💫  Dynamic Template Render"
        uses: varunsridharan/action-dynamic-readme@main
        with:
          global_template_repository: varunsridharan/varunsridharan
          files: |
            README.md
            templates/variables/defaults.md=output/variables/defaults.md
            templates/file-includes/inline.md=output/file-includes/inline.md
            templates/file-includes/reusable-includes.md=output/file-includes/reusable-includes.md
        env:
          GITHUB_TOKEN: 

```<!-- END [code:yml] .github/workflows/dynamic-template.yml -->

</details>

---
## Including File From A Remote Repository
You can include any type of file from any repository. if you want to include from a **Private** Repository then you have to provide **Github Personal Access Token** Instead **Github Token** in action's workflow file

### Usage :

```
Include from remote repository
<\!-- START {owner}/{repo}/{filepath}/{file} -->
<\!-- END {owner}/{repo}/{filepath}/{file} -->


Include from remote repository with specific branch
<\!-- START {owner}/{name}@{branch}/{filepath}/{file} -->
<\!-- END {owner}/{name}@{branch}/{filepath}/{file} -->
```
> **Note** : use `@` when loading files from specific branch
>
> Example : [`octocat/Spoon-Knife@master/README.md`](https://github.com/octocat/Spoon-Knife) file will be loaded below.
>
> Using : 

```
<\!-- START octocat/Spoon-Knife@master/README.md -->
<\!-- END octocat/Spoon-Knife@master/README.md -->
```

<details> 
<summary>Output :</summary>

<pre>
<!-- START octocat/Spoon-Knife@master/README.md -->
<!-- END octocat/Spoon-Knife@master/README.md -->
</pre>

</details>

---
## Including File From Global Repository Template
You can also configure a global template repository in action's workflow like `GLOBAL_TEMPLATE_REPOSITORY` and actions takes care of loading files from it. when using global template option you dont need to provide configure repository details in the include comment instead just load file like `<\!-- include file.md -->`

### Usage :

```
<\!-- START sponsor.md -->
<\!-- END sponsor.md -->
```

> If `sponsor.md` not found it current repository then it will check for the same in Global Template Repository & if found it will be loaded.

<details> 
<summary>Output :</summary>

<pre>
<!-- START sponsor.md -->
## 💰 Sponsor
[I][twitter] fell in love with open-source in 2013 and there has been no looking back since! You can read more about me [here][website].
If you, or your company, use any of my projects or like what I’m doing, kindly consider backing me. I'm in this for the long run.

- ☕ How about we get to know each other over coffee? Buy me a cup for just [**$9.99**][buymeacoffee]
- ☕️☕️ How about buying me just 2 cups of coffee each month? You can do that for as little as [**$9.99**][buymeacoffee]
- 🔰         We love bettering open-source projects. Support 1-hour of open-source maintenance for [**$24.99 one-time?**][paypal]
- 🚀         Love open-source tools? Me too! How about supporting one hour of open-source development for just [**$49.99 one-time ?**][paypal]



## Connect & Say 👋
- **Follow** me on [👨‍💻 Github][github] and stay updated on free and open-source software
- **Follow** me on [🐦 Twitter][twitter] to get updates on my latest open source projects
- **Message** me on [📠 Telegram][telegram]
- **Follow** my pet on [Instagram][sofythelabrador] for some _dog-tastic_ updates!

---

<p align="center">
<i>Built With ♥ By <a href="https://sva.onl/twitter"  target="_blank" rel="noopener noreferrer">Varun Sridharan</a> 🇮🇳 </i>
</p>

---

<!-- Personl Links -->
[paypal]: https://sva.onl/paypal
[buymeacoffee]: https://sva.onl/buymeacoffee
[sofythelabrador]: https://www.instagram.com/sofythelabrador/
[github]: https://sva.onl/github/
[twitter]: https://sva.onl/twitter/
[telegram]: https://sva.onl/telegram/
[email]: https://sva.onl/email
[website]: https://sva.onl/website/
<!-- END sponsor.md -->
</pre>

</details>

---

