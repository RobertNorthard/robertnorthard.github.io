---
title: "Terraform + InSpec for automated Infra as Code testing"
layout: post
date: 2019-02-07 18:00
headerImage: false
tag:
- Terraform
- InSpec
- CI / CD
star: false
category: blog
author: robertnorthard
description: Testing IaaC with InSpec
---


Our Infra structure CI / CD pipeline is a key enabler for us failing fast, controlling releases to environments, delivering with agility, ensuring parity between environments but The typical steps include: linting, Terraform validate, plan and apply.

We often face issues with Terraform apply passing and changes being promoted to higher environments, but the cloud account not being in the desired state – “Null Resources” try to avoid them at all costs (not idempotent). Manual testing is also slow and painful. We are also aspiring to Continuous Deployment for infrastructure as code – we need tests to achieve this.

After a brief investigation we discovered a few approaches:

* InSpec – RSpec audit and compliance as code framework for testing cloud account configuration
* Terratest
* AWSSpec
* Test Kitchen terraform driver – Manages Terraform lifecycle + InSpec

We concluded in using InSpec because:

* It’s well documented
* Tests are readable, follows RSpec BDD framework
* Has libraries for testing with different cloud providers GCP, Azure, AWS
* We didn’t need Test Kitchen as we already use a Makefile to manage the Terraform lifecycle of our environments and would not benefit from further abstractions – we use a Makefile to abstract build steps from Jenkinsfile but also to ensure our CI environment and developers workflow is identical.

What did we do:

* We updated our Dockerfile.ci to include Ruby and InSpec gem which defines our Jenkins slave execution environment and lives alongside our Jenkinsfile and infrastructure code.
* Extended our Makefile with a action to invoke InSpec and pass in an “attributes” file which contains environment specific config (e.g environment resource prefix for resource naming convention)

````
test-development:
   inspec detect -t azure://
   inspec vendor test –overwrite
   inspec exec test -t azure://$(AZURE_SUBSCRIPTION_ID) –attrs test/fixtures/development.yml
````

* Developed some simple tests to validate Terraform code (e.g. Virtual Networks exists with correct tags, in correct regions)

````
describe azurerm_virtual_network(resource_group: resource_group, name: vnet_name) do
    it { should exist }
    its(‘location’) { should eq ‘ukwest’ }
    its(‘type’) { should eq ‘Microsoft.Network/virtualNetworks’ }
end
````

* Developed some general tests to validate security conformance:
  * No any protocol, destination address and port Network Security Group rules
  * All NSGs have explicit deny all inbound and outbound rules

In my opinion, we are not using this in force, but it’s a great first step to validating our Terraform code and can be used for security compliance. The next steps are to look into CIS benchmark implementations in InSpec.

~ Robert
