# Selenium Hub on Openshift Local
Selenium functions as a browser automation tool primarily employed for testing web applications. Yet, when integrating Selenium into a Continuous Integration (CI) pipeline to assess applications, disputes frequently arise concerning the allocation of Selenium resources. The following illustration demonstrates the procedure for deploying Selenium onto a Kubernetes platform with a focus on scalability. 

## check your openshift local status if not running then start it
```
crc status

```
![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/d9c20b00-f1a7-497d-884f-35ac6c967db2)

## to start the openshift local (Note: It will take some to get ready for use)
```
crc start
```
![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/c2f1c1ea-63fe-4659-a4f6-3c558158054c)

![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/06884f9e-a2cd-4973-816d-2bf65a2589e2)

## Login as developer
```
eval $(crc oc-env)
oc login -u developer https://api.crc.testing:6443

```



![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/f7fa4649-7704-422a-944b-b14271559edd)


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
![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/ced3b19e-bf17-400e-8c41-77404b47feda)

![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/1e95794f-1a6d-407f-88fc-fdb82073abc4)

```
export PODNAME=`oc get pods --selector="app=selenium-hub" --output=template --template="{{with index .items 0}}{{.metadata.name}}{{end}}"`
```

```
oc port-forward $PODNAME 4444:4444
```


![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/1777be17-3c06-4bfe-bccc-9ba92bbd0823)


![image](https://github.com/a4ambrish/king-of-kubernetes/assets/16659736/aa27e3fa-2b4b-4029-af52-07978d411811)

## Cleanup (if required)
```
oc delete deployment selenium-hub
oc delete deployment selenium-node-chrome
oc delete deployment selenium-node-firefox
oc delete deployment selenium-python
oc delete svc selenium-hub
```
 
