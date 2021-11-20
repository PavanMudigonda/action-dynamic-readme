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


      - name: "💫  Dynamic Template Render"
        uses: varunsridharan/action-dynamic-readme@main
        with:
          GLOBAL_TEMPLATE_REPOSITORY: PavanMudigonda/coverage-reporter
          files: |
            templates/file-includes/reusable-includes.md=README.md
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
<\!-- START PavanMudigonda/coverage-reporter@main/badge-template.md -->
<\!-- END PavanMudigonda/coverage-reporter@main/badge-template.md -->
```

<details> 
<summary>Output :</summary>

<pre>
<!-- START PavanMudigonda/coverage-reporter@main/badge-template.md -->
<svg fill="none" viewBox="0 0 120 120" width="120" height="120" xmlns="http://www.w3.org/2000/svg">
  <foreignObject width="100%" height="100%">
    <div xmlns="http://www.w3.org/1999/xhtml">
      <a href="">
<img alt="CI Build" src="https://github.com/$GITHUB_REPOSITORY/actions/workflows/$GITHUB_WORKFLOW/badge.svg?branch=$”GITHUB_REF_NAME>
      </a>
<br/>
<img alt="Stale Pull Requests" src=".github/badges/stale-pr-count.svg">
<br/>
<img alt="Dated Dependencies" src=".github/badges/dated-dependency-count.svg">
<br/>
<img alt="Veracode Vulnerabilities" src=".github/badges/veracode-vulnerability-counts.svg">
<br/>
<img alt="Code Coverage" src=".github/badges/code-coverage.svg">
<br/>
<img alt="Latest Release" src=".github/badges/latest-release.svg">
    </div>
  </foreignObject>
  </svg>
<!-- END PavanMudigonda/coverage-reporter@main/badge-template.md -->
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
<!-- END sponsor.md -->
</pre>

</details>

---

