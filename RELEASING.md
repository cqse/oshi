Releasing OSHI
=====================

### Prepare

* Make sure tests are green on [Travis CI](https://travis-ci.org/dblock/oshi).
	* Choose an appropriate [version number](http://semver.org/) for the release
	* Proactively change the download link in [README.md](README.md) to point to the new version
	* Copy [README.md](README.md) to [src/site/markdown/README.md](src/site/markdown/README.md)
	* Change "Next" or in-progress version in [CHANGELOG.md](CHANGELOG.md) to this new version.
	* Move "Your contribution here." to a new empty "Next" section
	* Commit changes as a "prep for x.x release"

### Release

* See [this page](http://central.sonatype.org/pages/apache-maven.html#performing-a-release-deployment-with-the-maven-release-plugin) for a summary of the below steps
* `mvn release:clean`
	* Takes a few seconds
* `mvn -DdryRun=true release:prepare`
	* Takes a few minutes
	* This will ask for the version being released, removing -SNAPSHOT
	* This will suggest the next version, increment appropriately
	* Allows opportunity to find/fix any build errors
* `mvn release:prepare`
* `mvn release:perform`
	* Takes a few minutes. You should have previously:
		* Put your [repository credentials in your Maven settings.xml file](http://central.sonatype.org/pages/apache-maven.html#distribution-management-and-authentication). Use the default sonatype-nexus-staging id.
		* Put your [gpg certificate credentials in the settings.xml file](http://central.sonatype.org/pages/apache-maven.html#gpg-signed-components)
	* This pushes the release to the [Nexus](https://oss.sonatype.org/) staging repository
	* This also pushes to [gh_pages](https://dblock.github.io/oshi)
* Log on to [Nexus](https://oss.sonatype.org/) and [release the deployment from OSSRH to the Central Repository](http://central.sonatype.org/pages/releasing-the-deployment.html).
	
* Add a title and release notes [to the tag](https://github.com/dblock/oshi/tags) on GitHub and publish the release to make it current.

* As development progresses, update version in [pom.xml](pom.xml) using -SNAPSHOT appended to the new version using [Semantic Versioning](http://semver.org/) standards:
	* Increment major version (x.0) for API-breaking changes or additions
	* Increment minor version (x.1) for substantive additions, bugfixes and changes that are backwards compatible
	* Increment patch version (x.x.1) for minor bugfixes or changes that are backwards compatible
