# Maven Example: Sign only if CI

This example show how to sign an exe from maven with the following requirements:

* the signing configuration must happen in a parent pom so many project can share the same configuration
* the signing should only be performed from the CI server and not from the usual developer workstation.

The biggest problem to make it works is that the jsign-maven-plugin does not have any `skip` parameter.

The trick to make it work is to associate the plugin execussion to a nonexisting phase 'none'.
But to allow this phase definition to be overiden somewhere else.
The rest is standard maven plugin management.

Thanks to the following post for the idea:
https://www.igorkromin.net/index.php/2017/03/17/skipping-execution-of-maven-plugins-that-do-not-have-a-native-skip-option/

## How to run the example

to run the maven build as a developer:
`mvn -f child/pom.xml package`

to run the maven build as a CI server:
`mvn -f child/pom.xml -s settings.xml package`
_note that the execussion will fail as the exe and the java keystore don't exist in this example_