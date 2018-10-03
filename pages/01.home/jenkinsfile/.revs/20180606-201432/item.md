---
title: Jenkinsfile
taxonomy:
    category:
        - Applications
        - DevOps
        - Pipeline
        - CI
        - CD
---

## Global vars
List of available global vars: https://JENKINS_URL/pipeline-syntax/globals

Define your own global vars in "Configure System" -> **Global Pipeline Libraries**. 

### Repository structure
* ressources directory can have non-groovy resources, e.g. json, that get loaded via the libraryResource step.
* src directory uses a structure similar to the standard Java src layout and is added to the classpath when a Pipeline that includes this shared library is executed.
* vars directory holds global variables that should be accessible from pipeline scripts. A corresponding .txt file can be included that defines documentation for objects here.

Example for vars file named `deployment.groovy`:

```groovy
def call(args) {
    if( args == "deploy") {
        lastBuild = ( ${env.BUILD_ID} as int) - 1
        sh "docker-compose pull"
        sh "docker-compose -p ${env.JOB_NAME}-${lastBuild} up --force-recreate --no-color  -d"
    }
    if( args == "remove") {
        LastBuild = env.BUILD_ID - 1
        sh "docker-compose -p ${env.JOB_NAME}-${LastBuild} down --remove-orphans"
        sh "docker-compose rm -f"
    }
}
```

### Usage
In your Jenkinsfile 
```groovy
library ('LIBRARY_NAME') // At the beginning
...
stages {
   stage ('prepare') {
        steps {
            deployment('remove') // name of the file of the shared library
        }
    }
...
}
```

[Reference](https://jenkins.io/doc/book/pipeline/shared-libraries/)

## Jenkinsfile 

### Enable git tag / push with ssh on jenkins slaves

Install [SSHAgent Plugin](https://wiki.jenkins.io/display/JENKINS/SSH+Agent+Plugin).
```groovy
def gt(args) {
    sshagent(['13fa2-gg251as-135tasf1-sa2']) {
                    sh "git ${args}"
                }
}
```
The cryptic number represents the ID of the credentials saved in the credential store of Jenkins

### Use credentials in your pipeline

```groovy
environment {
	NEXUS_CREDS = credentials('developer')
}
````
The name is the ID of the credential. Then the following three variables are automatically available:
* NEXUS_CREDS_USR (the username)
* NEXUS_CREDS_PSW (the password)
* NEXUS_CREDS (username:password)