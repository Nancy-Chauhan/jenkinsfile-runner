Jenkinsfile Runner Packaging POM (Experimental)
==============================================

This is an experimental parent POM for packaging custom Jenkinsfile Runner images.
It can be used for packaging of custom Jenkinsfile Runner bundles,
but at the moment it has a lot of limitations.

The framework is not ready for public use,
but you can try it out in your projects.
See the [Vanilla Package](/vanilla-package) definition to get an example.

## Known limitations

* Package produced by appassembler is **NOT** enough.
  Although it packages JARs and sets up classpath correctly,
  the resulting JFR bundle cannot execute Pipelines which rely on
  `Jenkins.instance.getPluginManager().getPlugin(String)`,
  because the plugin manager cannot discover plugins from classpath.
  * Solution: provide plugins using `--plugins`.
    It leads to higher image sizes, and needs to be fixed somehow.
* Uber Jar Packaging does not work reliably.
  See https://github.com/jenkinsci/jenkinsfile-runner/issues/350

## Other TODOs

* Cleanup profile management (there are warnings during the build)
* Add support for Docker packaging
* Add a light testing framework for Jenkinsfile Runner bundles
* Simplify management of Groovy Hooks, JCasC configs and System Properties.
  It would reduce need in Custom WAR Packager for simple use-cases.