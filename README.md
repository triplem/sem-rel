# sem-rel

This project shows how to use sem-rel in a "gitflow"-like workflow environment using [semantic-release](https://github.com/semantic-release/).

## Installed packages

semantic-release needs to get installed based on the existing nodejs version. For a nodejs-version 12.x the following packages should get installed:

```
npm install semantic-release@17.4.7
npm install @semantic-release/git@9.0.1
npm install @semantic-release/exec@5.0.0
npm install @semantic-release/changelog@5.0.1
```

If the installed nodejs-version is 14.x the latest semantic-release-Version can be installed, including all required plugins.

The semantic-release tool can then be called using the following command-line:

```
npx --no-install semantic-release
```

Please note, that the flag `--no-ci` is required, if this tool is called outside of an CI-Tool (eg. on your local development environment).

If github/ github Enterprise is used, the git-plugin does not need to be installed, instead the corresponding github-plugin can be used, which is installed by default with semantic-release.

## Steps in build process

### Steps not related to the generated version

* build
* run tests
* run integration tests
* run acceptance tests
* run quality assurance checks (eg. sonarqube)
* run security checks (eg. owasp)
* build docker image
* run security checks on build image

### Steps related to the semnatic-release version

* tag git repository
* tag docker image
* tag generated artifacts
* publish docker image
* publish generated artifacts
* generated Changelog

## Risks

If using any build mechanism like eg. gradle, this release process is not "fully integrated" and is therefor most probably not fully atomic. All steps related to the semantic-release version do need to know the generated version and this version can only exist exactly once. This means, that if one of those steps fail, all previous steps do need to be run with an incremented version number. To mitigate this, we should determine and tag the repository first. With this if any of the following steps fails, the version can be bumped easily with an appropriate commit message.

All steps not related to the generated version should run beforehand and should fail fast or fail on the end of the "unrelated" step-chain.

 
