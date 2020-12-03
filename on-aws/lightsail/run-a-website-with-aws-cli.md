# How to run a website with Lightsail

## Pre-requisite

Install AWS CLI, check [here](/on-aws/interact.md) to know how to do

## Steps

The entry point for Lightsail is ```aws lightsail```

```
aws lightsail help #gives you the help of the command

# list of instances you have, it should be empty if you start now
aws lightsail get-instances

# list of the possible blueprints that can be used to create your instance
aws lightsail get-blueprints
# 'wordpress' is the blueprint id for wordpress

# get your default region (useful for after)
aws configure get region

# check which bundle (or price plan) you want to use (I suggest the one at 3.5 USD, nano_2_0)
aws lightsail get-bundles
```

Let's create the instance now.

* call the instance 'MyFirstBlogForDemo'
* use as availability zone your favorite one; me is 'eu-central-1a' = 'eu-central-1' + 'a' (region + letter a/b/c...)
* use the bundle is nano_2_0 (the cheapest)

The complete command is this and it can take some seconds to complete

```
aws lightsail create-instances --instance-names MyFirstBlogForDemo --availability-zone eu-central-1a --blueprint-id wordpress --bundle-id nano_2_0
```

When finished you should get an output like this:

```
{
    "operations": [
        {
            "id": "58569926-be45-4188-8d9d-31ca37691690",
            "resourceName": "MyFirstBlogForDemo",
            "resourceType": "Instance",
            "createdAt": "2020-12-03T17:32:24.541000+01:00",
            "location": {
                "availabilityZone": "eu-central-1a",
                "regionName": "eu-central-1"
            },
            "isTerminal": false,
            "operationType": "CreateInstance",
            "status": "Started",
            "statusChangedAt": "2020-12-03T17:32:24.541000+01:00"
        }
    ]
}
```

Now you should be able to see your new instance running:

```
aws lightsail get-instances
```

In the response of get-instance you can see the public IP assigned to your instance, the parameter is called "publicIpAddress", put this value in your favorite browser and you will see your website up & running.

When you finish, let's clean everything by doing:

```
aws lightsail delete-instance --instance-name MyFirstBlogForDemo
```
