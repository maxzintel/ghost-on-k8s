# ghost-on-k8s

Ghost is a popular blogging engine with a clean UI, built on JS.  
Ghost is configured using a JS file (infra/ghost-config.js) which we will store as a ConfigMap.
`kubectl create cm --from-file infra/ghost-config.js ghost-config`  
We will mount this ConfigMap as a volume inside of our (future) Ghost container.
