# Host on GitHub Pages

- [Demo site on GitHub Pages] (build & deploy with GitHub Actions)



## Build and deploy with GitHub Actions

- [peaceiris/actions-gh-pages: GitHub Actions for deploying to GitHub Pages with Static Site Generators](https://github.com/peaceiris/actions-gh-pages)

Go to the repository and read the latest `README.md` for more details.



## Build and deploy with `mkdocs gh-deploy`

### pipenv

```
pipenv run deploy

# OR
pipenv shell
mkdocs gh-deploy

# OR
pipenv run mkdocs gh-deploy
```



## Build and deploy with CircleCI

- Set these **Environment Variables**.
    - `USER_NAME`: GitHub ID
    - `USER_EMAIL`: Email
    - `GITHUB_TOKEN`: [Personal access token]



<!-- Internal References -->
<!-- External References -->
[Demo site on GitHub Pages]: https://github.com/gregruthenbeck/cavapa_docs.git
[Personal access token]: https://github.com/settings/tokens
