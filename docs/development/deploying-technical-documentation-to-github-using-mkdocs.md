# Deploying technical documentation to github using mkdocs

## Resources

* [Deploying your docs](https://www.mkdocs.org/user-guide/deploying-your-docs/#deploying-your-docs)

## Contextual Description

mkdocs inlcudes support for hosting project documentation on [GitHub](https://github.com/) using [GitHub Project Pages](https://help.github.com/articles/user-organization-and-project-pages/#project-pages-sites) sites. **GitHub Project Pages** are similar to [GitHub User and Organization Pages](https://help.github.com/articles/user-organization-and-project-pages/#user-and-organization-pages-sites) sites **but have some important differences, which require a different work flow when deploying.**

### GitHub Project Pages

Project Pages site files are automatically deployed to a branch within the project repository (`gh-pages` by default). The process goes like this:

`checkout` the primary working branch (usually `master`):

```shell
git checkout master
```

Run `mkdocs gh-deploy`:

```shell
mkdocs gh-deploy
```

MkDocs will automatically build your docs and use the [ghp-import](https://github.com/davisp/ghp-import) tool to commit them to the `gh-pages` branch and push the `gh-pages` branch to GitHub.

Use `mkdocs gh-deploy --help` to get a full list of options available for the `gh-deploy` command.

Be aware that you will not be able to review the built site before it is pushed to GitHub. Therefore, you may want to verify any changes you make to the docs beforehand by using the `build` or `serve` commands and reviewing the built files locally.

Warning

You should never edit files in your pages repository by hand if you're using the `gh-deploy` command because you will lose your work the next time you run the command.

### Organization and User Pages

User and Organization Pages sites are not tied to a specific project, and the site files are deployed to the `master` branch in a dedicated repository named with the GitHub account name. Therefore, you need working copies of two repositories on our local system. For example, consider the following file structure:

```
my-project/
    mkdocs.yml
    docs/
orgname.github.io/
```

of choice for more information.

------