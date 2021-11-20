
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

<pre>
<!-- START sponsor.md -->
<!-- END sponsor.md -->
</pre>

</details>

---

