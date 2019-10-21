---
title: "Improving maintenance of your Jenkins(file) pipelines"
layout: post
date: 2020-10-20 18:00
headerImage: false
tag:
- Pipelines as code
- Jenkins
- Declarative pipelines
star: false
category: blog
author: robertnorthard
description: Improving maintenance of your Jenkins(file) pipelines
---

Do you have 100s repositories with Jenkinsfile that look very similar and spend hours updating after the slightest change Declarative Jenkins pipeline are great. It makes it easy to create multi-branch pipelines (e.g. run tests or even build environments on feature branches). However, with all these Jenkinsfile everywhere maintaining them and sharing assets can be a challenge.

Imagine an environment where there is 10 services and therefore 10 copies of the same Jenkinsfile. To change a method we have to update the Jenkinsfile in 10 different places. With this level of decoupling teams will struggle to standardise and benefit from efficiency as we scale.

To try and resolve this you can look at developing Jenkins shared libraries. Libraries enable you to encapsulate build steps in re-usable methods. A shared library is stored in Git and retrieved as part of Jenkins pipeline builds. Jenkins pipelines can then import methods from this library - see example code below. This is great, we can now build a pipeline with shared step implementation and these steps can maintained and controlled centrally. The library can also be versioned.

````

@Library('shared-library') // no version specified always pull the latest and greatest

pipeline {

    agent none

    stages {
        stage('Deploy') {
            steps {
                deployToEnv('DEV')  // shared steps
            }
        }
    }
}

````

Shared libraries are a good start as it enables standard methods that product teams can use for their CI / CD steps. Teams still have control over the order of stages in the pipeline. In my opinion, we should be opinionated on the stages on what a CI / CD pipeline for say Java should look like.

Now let's scale, imagine you have 100 services (same technology) spread across 100 repositories and we want to add a new "stage" to the pipeline for enhanced security testing. With this approach the product teams would have to update 100 repositories. How might you tackle this?

Linking into a previous blog post you could jump to buildpacks, but let's solve the problem with Jenkins pipelines first.

To resolve this, alongside adding specific Jenkins stage step implementations to the shared library you can add the whole pipeline as a class that is configurable. Product teams could then add Jenkinsfile to their repositories and instantiate the pipeline suitable for their application - see example below.

````

@Library('shared-library') // no version specified always pull the latest and greatest

import pipeline.JavaPipeline;

new JavaPipeline(
  name: "ServiceA"
);

````

With this approach it brings greater efficiency of scale (why reinvent the wheel for a typical Java CI / CD pipeline) and enables standardisation and control.

~Robert
