
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

