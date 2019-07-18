# How to deploy

## OpenShift deployment

Use the `openshift/httpd` image to deploy Apache HTTPd. THis can be done using the `Apache HTTP Server` 
application in the OpenShift application catalog. 

Specify this GitHub repo as the contents and probably an Application hostname to use as the URL that will
be used to access the pages.

Create the application. It will take a few minutes to build and deploy.
Once working you probably want to add TLS certificates. If [ACME controller](https://github.com/tnozicka/openshift-acme) 
is deployed then all you need to do is edit the route defintion and add this annotation:
```
  annotations:
    kubernetes.io/tls-acme: "true"
```

## Webhook

A webhook will allow the app to be rebuilt and redeployed whenever the contents of the GitHub repo change.
This usually takes about a minute. 

Go to the settings of the appropriate build config that was created (name is dependent on what you specified as the 
appliication name). In the configuration section you will find the GitHub webhook url.

In this GitHub repo add a webhook (found in the Settings section). Specify the webhook url you found above.
The `content type` should be `application/json`. Include the secret if you specified one when creating the 
application.
