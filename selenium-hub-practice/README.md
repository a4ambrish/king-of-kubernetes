# Selenium Hub on Openshift Local
Selenium functions as a browser automation tool primarily employed for testing web applications. Yet, when integrating Selenium into a Continuous Integration (CI) pipeline to assess applications, disputes frequently arise concerning the allocation of Selenium resources. The following illustration demonstrates the procedure for deploying Selenium onto a Kubernetes platform with a focus on scalability. 

## check your openshift local status if not running then start it
```
crc status

```
## to start the openshift local
```
crc start
```

## Login as developer
```
eval $(crc oc-env)
oc login -u developer https://api.crc.testing:6443

```
## Create all the PODs need to setup the Selenium Hub Environment 
```
oc create -f selenium-hub-deployment.yaml
```

```
oc create -f selenium-hub-svc.yaml
```

```
oc create -f selenium-node-chrome-deployment.yaml
```

```
oc create -f selenium-node-firefox-deployment.yaml
```

```

```
 
