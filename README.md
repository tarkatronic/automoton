# Automoton

This handy little project is a one stop, one command shop to set up a basic web environment.
Fun part is, it will even be a good little soldier and report in when it's ready for duty!
The project is built utilizing two primary technologies: AWS CloudFormation, and Ansible.
CloudFormation provides the provisioning of resources, and Ansible handles all of the
(stateful) system configuration.

There are two easy ways to run this puppy and get everything going. The first is via the
AWS console. All you have to do is upload the `cloudformation.json` into the CloudFormation console,
it will ask you a few questions, and you're off to the races! The alternative is one command from
the console.

```
aws cloudformation create-stack --stack-name <stack name> \
  --template-body https://raw.githubusercontent.com/tarkatronic/automoton/master/cloudformation.json \
  --parameters ParameterKey=KeyName,ParameterValue=<key name> \
  ParameterKey=NotificationEmail,ParameterValue=<email address>
```

The parameters available to this CloudFormation stack are as follows:

* **KeyName**: A valid name for an SSH key available in the selected region to build this system with
* **NotificationEmail**: An email address to which the notification email should be sent when the build is complete
* **InstanceType**: (Optional; default: t2.micro) The type (size) of instance to be created.
  This can be any valid instance type name (t2.micro, m3.large, c3.8xlarge, etc)

Whichever way you use to build this stack, it will put a VERY basic server into place, running nginx,
and with a simple index.html in place. It is not secure. It is not terribly robust. This setup is NOT
recommended for production use. But it's at least a start!

In order to get the link for the site, you have three simple options:

1. Wait for your notification email, and it will contain the address of the newly created instance.
2. Check the `Outputs` tab of the stack in the AWS console
3. Use the AWS CLI:
  ```
  aws cloudformation describe-stacks --stack-name <stack name>
  ```

And that's about all there is to that!
