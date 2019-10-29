---
title: "Writing a custom Terraform provider!"
layout: post
date: 2019-10-29 21:00
headerImage: false
tag:
- Terraform
- Provider
star: false
category: blog
author: robertnorthard
description: Writing a custom Terraform provider!
---

So, how do you develop a custom Terraform provider? There are a lot of blogs like this, but the purpose of this one is to learn myself. In this post we will develop a custom terraform provider that exposes a data source for retrieving the Coinable API endpoint.

First, I read the [Terraform plugin SDK getting started guide](https://www.terraform.io/docs/extend/writing-custom-providers.html), which is is a good overview of the SDK which is used for developing a custom Terraform provider. This blog posts assumes you have all "Go" pre-reqs set-up successfully. 

Next, we need to create two boilerplate files:
* provider.go - this is the core of the plugin. This controls the resources that the provider offers and can expose via its interface
* main.go - the entry point when the binary is built, this invokes the "Provider" function in provider.go

```
Provider.go

package main

import (
        "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
)

func Provider() *schema.Provider {
        return &schema.Provider{}
}

```

```
package main

import (
        "github.com/hashicorp/terraform-plugin-sdk/plugin"
        "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func main() {
        plugin.Serve(&plugin.ServeOpts{
                ProviderFunc: func() terraform.ResourceProvider {
                        return Provider()
                },
        })
}
```

Now, we have our boilerplate code set-up, let's start writing our new data source. First we define the Terraform interface we are working towards for the provider. Based on the below we want to create a new data source resource which returns the Coinbase "api_endpoint". Data sources are read-only and therefore, for this basic example we do not have to persist anything in the statefile.

```
data "coinbase_address" "api_address" {}

output "endpoint" {
  value = ["${data.coinbase_address.api_address.api_endpoint}"]
}
```

Next, let's create our data source code. Create a new go file called "data_address". By convention for a provider we name the file type_name, where type is the Terraform component it provides (e.g. data (data source), resource).

Create the file, with the following:

```

package main

import (
        "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
)

func dataCoinbaseAddress() *schema.Resource {
        return &schema.Resource{
                Read:   resourceCoinbaseSourceAddressRead,
                Schema: map[string]*schema.Schema{
                        "api_endpoint": &schema.Schema{
				            Type:     schema.TypeString,
                            Computed: true,
			            },
                },
        }
}

func resourceCoinbaseSourceAddressRead(d *schema.ResourceData, m interface{}) error {
        endpoint := "https://api.coinbase.com/v2" 
        d.SetId(endpoint)
        d.Set("api_endpoint", endpoint)
        return nil
}
```

Breaking this down a bit. The `dataCoinbaseAddress` function returns a new Resource. "Read" is the function to execute when refreshing the Terraform data source and "Schema" is the data resource attributes. This resource has one attribute named "api_endpoint" which is computed and therefore not provided by the user.

The `resourceCoinbaseSourceAddressRead` function takes in the `ResourceData` which is the user provided attributes of the data source. Using `d.Set("api_endpoint", endpoint)` we can then add an attribute to this struct of type `ResourceData`. ResourceData is used for CRUD based operations on the resource e.g. querying or setting attributes and other purposes.

To build the provider you will need to run the following Go commands:

```
go get -v
go build -o terraform-provider-coinbase
```

To test this create a new folder `example/' and a file named `main.tf` with the following contents.

```
data "coinbase_address" "api_address" {}

output "endpoint" {
  value = ["${data.coinbase_address.api_address.api_endpoint}"]
}

```

Now, run terraform init followed by a plan targeting the `/example` folder. You should get similar output to the below: 

```
terraform init example/
Initializing the backend...
Initializing provider plugins...
Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
terraform plan example/
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.

data.coinbase_address.api_address: Refreshing state...

------------------------------------------------------------------------

No changes. Infrastructure is up-to-date.

This means that Terraform did not detect any differences between your
configuration and real physical resources that exist. As a result, no
actions need to be performed.
terraform apply example/
data.coinbase_address.api_address: Refreshing state...

Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

endpoint = [
  "https://api.coinbase.com/v2",
]

```

Checkout the [GitHub repo](https://github.com/RobertNorthard/terraform-provider-skeleton) for the full example source code, along with example Terraform code for testing.

~Robert
