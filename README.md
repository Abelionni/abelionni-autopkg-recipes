# DO NOT USE

This repo isn't published for now on autopkg repo, this mean content isn't read for production.

# Abelionni AutoPKG Recipes
 
__The goal of this special recipes repository for AutoPkg is to build trust into the thousands of available AutoPkg recipes for our customers and the community.__
 
In order to accomplish this, we will have a team of vetted reviewers ensuring that the recipes in this repository follow strict rules. These rules limit recipes' capabilities, and defining and enforcing those rules will require a lot of work on the part of our community. But we hope that the benefits of establishing a core of trusted recipes will be well worth it.
 
 
## What kind of trust?
 
We intend to build trust in _recipes_ — not in _payload_. We will verify that the recipe plist content is correctly identified, comes from a trusted source, and behaves in a reasonable manner. However, we will not guarantee that the software packaged by the recipe is secure or trusted.
 
 
## Who reviews these recipes?
 
Our reviewers are volunteers with recognized interest in the security of AutoPkg. Their role is to ensure that recipes conform to the above rules.
 
They don't write the recipes, and they don't do security checkup on the payload of the downloaded material.
 
Reviewers' GitHub accounts are required to use two-factor authentication to prevent unauthorized access to this repository.
 
 
## Repository structure and content
 
All recipes available in this repo must be organized in folders by software developer, then in subfolders by product name.
 
All products MUST have:
 
* a download recipe
* a package (pkg) recipe
* an install recipe
 
And MAY have:
 
* shared recipes stored at the software developer level (for example, if a single download recipe can be used for multiple products)
* "importer" recipe(s) dedicated to a distribution service (for example, a Munki or JSS recipe)
 
All recipe identifiers follow following nomenclature: ```com.abelionni.autopkg.recipe.trusted.<action>.<developer>.<product>```
 
And for recipe filename: ```AbelionniTrusted<Developer><Product>.<action>.recipe```
 
Contributors' identity must not be used in recipe name or identifier.
 
Contributors are tracked via git history and if needed by a ```AbelionniTrusted<Developer><Product>.contributors.txt``` file. This file may also contain a reference to original source of inspiration (if an unmaintained recipe is ported by someone else to this repo).
 
Here's an example of the repository structure, including recipe identifiers:
 ```
- Microsoft
    - Office 2016
        - AbelionniTrustedMicrosoftOffice2016.download.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.download.Microsoft.Office2016`)
        - AbelionniTrustedMicrosoftOffice2016.pkg.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.pkg.Microsoft.Office2016`)
        - AbelionniTrustedMicrosoftOffice2016.install.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.install.Microsoft.Office2016`)
        - AbelionniTrustedMicrosoftOffice2016.munki.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.munki.Microsoft.Office2016`)
    - Office 2011
        - AbelionniTrustedMicrosoftOffice2011.download.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.download.Microsoft.Office2011`)
        - AbelionniTrustedMicrosoftOffice2011.pkg.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.pkg.Microsoft.Office2011`)
        - AbelionniTrustedMicrosoftOffice2011.install.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.install.Microsoft.Office2011`)
        - AbelionniTrustedMicrosoftOffice2011.munki.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.munki.Microsoft.Office2011`)
- Adobe
    - Acrobat Reader DC
        - AbelionniTrustedAdobeAcrobatDC.download.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.download.Adobe.AcrobatDC`)
        - AbelionniTrustedAdobeAcrobatDC.pkg.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.pkg.Adobe.AcrobatDC`)
        - AbelionniTrustedAdobeAcrobatDC.install.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.install.Adobe.AcrobatDC`)
        - AbelionniTrustedAdobeAcrobatDC.munki.recipe
            (identifier: `com.abelionni.autopkg.recipe.trusted.munki.Adobe.AcrobatDC`)
 ```
 
## Recipes requirement
 
All recipes available in this repo __must__ use a HTTPS source URL and may __not__ run scripts or use custom processors.
 
All URLs present in the recipes __must__ point to the product developer's website. No recipe will be allowed if it uses mirrors or personal web site URLs.
 
If a recipe requires a custom processor, we first recommend considering whether it would be valuable in the core AutoPkg lib. If not and under certain circumstances, a custom processor __may__ be allowed here after a deep code review. That requires more time from our reviewers, so avoid it if you expect your contribution to be made available quickly.
 
Payload (dmg, pkg, app) code signature verification __must__ be checked by the download recipe.
 
 
## Lifecycle
 
### Contribution
 
To contribute to this repository, please use the [git-flow](http://nvie.com/posts/a-successful-git-branching-model/) method.
 
Make a clone from this repo, when working on a recipe, always do a dedicated fork (called feature in git-flow parlance).
 
When your contribution is ready, update your `develop` branch from the original one, then merge your feature fork.
 
Then issue a pull request from your `develop` branch.
 
### Validation
 
In the future, automated validation may occur before the PR reaches reviewers. For now, we are relying on the reviewers' eagle eyes.
 
### Pre-production
 
When a pull request is submitted, a first analysis is done by the reviewer by simply reading the PR. When enough reviewers have checked the change, the PR is accepted and integrated in the `develop` branch.
 
Then the recipe will be tested for a while by reviewers and pre-production users.
 
### Production
 
When all current changes in the `develop` branch are considered stable, a merge with the `master` branch will be done.
 
### Hot fix
 
If a recipe is broken due to a change in the software reviewer side, an hot fix can be submitted.
 
This hot fix must be done from the `master` branch and then merge into the `develop` branch.
 
When you issue a PR for a hot fix, you must specify it in the PR title and the change must be linked only to the fix. Do not change something not related to the fix in a hot fix PR.
