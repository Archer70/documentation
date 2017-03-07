---
title: ParallelCI
weight: 97
tags:
- testing
- continuous integration
- parallelci
- parallelism
category: Getting Started
redirect_from:
  - /continuous-integration/parallelci/
---

**ParallelCI** allows you to split your test commands across multiple build VMs to speed up your build time. See the [ParallelCI feature page](http://codeship.com/features/parallelci) to check out how this helped users improve their build times tremendously.

<div class="info-block">
Do you want to try **ParallelCI** on your projects? [Sign up for the trial](https://codeship.com/projects#start-trial) and use up to 20 parallel test pipelines for two weeks on all your projects.

A few days before the end of the trial we'll send you a message to give you a heads up including a comparison of build times before and during the trial. Once the two weeks are up any additional pipelines not included in your current plan will be merged into the first one.

If you have any questions about the trial you can reach us directly at [support@codeship.com](mailto:support@codeship.com).
</div>

## Test Pipelines
Each project has multiple **test pipelines** that are run in parallel. Each of those pipelines is a build VM running independently of each other. Codeship will first run your setup commands and then any arbitrary _test commands_ you defined for this specific pipeline via the interface. To ease distinguishing different pipelines you can provide a name for each one.

![Configuration of test pipelines]({{ site.baseurl }}/images/continuous-integration/parallelization-test-pipelines-configuration.png)

### Disable ParallelCI
You can either delete additional test pipelines, or comment out any commands by prepending a `#` symbol to each line. A test pipeline is only active if it contains at least one command.

## Deployment Pipeline
If you have a deployment configured for a specific branch and each test pipeline reports a successful run, your deployment pipeline will be run. You do not need to change anything if you use one of our integrated deployments.

As we do not run your _setup commands_ for the deployment pipeline, please add a script based deployment before the actual deployment and install any required dependencies there.

![Configuration of build pipelines]({{ site.baseurl }}/images/continuous-integration/parallelization-deploy-pipelines.png)

## Artifacts Support
As your build and deployment commands are run on multiple virtual machines, **artifacts created during the test steps will not be available during the deployment**. If you need artifacts from the previous steps, make sure to regenerate them during the deployment using a [_script deployment_]({{ site.baseurl }}{% link _basic/continuous-deployment/deployment-with-custom-scripts.md %}) added before the actual deployment.

## Downgrade Behavior
If you downgrade to a subscription with fewer parallel pipelines any additional pipelines will merged into the first one. If this is not desirable for your project make sure to manually move the steps to the appropriate test pipelines before downgrading.

## Parallel Modules
In addition to parallelizing explicitly in your via parallel pipelines, most popular frameworks offer modules that you can install to parallelize within the codebase itself.

While we do not officially support or integrate with any of these modules, many Codeship users find success speeding their tests up by using them. Note that in many cases these modules create additional strain on your machine resource usage, so you will want to keep an eye on this as misconfiguration can result in a resource max out that ultimately slows your builds down or causes failures.

### Rails
https://github.com/grosser/parallel_tests
https://github.com/ArturT/knapsack

### Node
https://www.npmjs.com/package/mocha-parallel-tests

### PHPUnit
https://github.com/brianium/paratest
