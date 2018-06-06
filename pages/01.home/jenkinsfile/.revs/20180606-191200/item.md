---
title: Jenkinsfile
taxonomy:
    category:
        - Applications
        - DevOps
        - Pipeline
        - CI
        - CD
    author:
        - Knecht
---

## Global vars
List of available global vars: https://JENKINS_URL/pipeline-syntax/globals

Define your own global vars in "Configure System" -> **Global Pipeline Libraries**. 

Repository structure:
* ressources directory can have non-groovy resources, e.g. json, that get loaded via the libraryResource step.
* src directory uses a structure similar to the standard Java src layout and is added to the classpath when a Pipeline that includes this shared library is executed.
* vars directory holds global variables that should be accessible from pipeline scripts. A corresponding .txt file can be included that defines documentation for objects here.

##