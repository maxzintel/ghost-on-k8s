# ghost-on-k8s

Ghost is a popular blogging engine with a clean UI, built on JS.  
  
#### Imperative Steps to Deploy:
(Once you have all the files in ~/infra)
* Ghost is configured using a JS file (infra/ghost-config.js) which we will store as a ConfigMap.
  * `kubectl create cm --from-file infra/ghost-config.js ghost-config-yaml`  
* Create your mysql database:
  * `kubectl apply infra/mysql/mysql-configmap.yml`
  * `kubectl apply infra/mysql/mysql-services.yml`
  * `kubectl apply infra/mysql/mysql-statefulset.yml`
* Then, exec into the mysql master container to create the db table we want to use:
  * `kubectl exec -it mysql-0 -- mysql -u root -p`
  * `create database ghost_db`
  * `exit`
* `kubectl apply infra/ghost.yml` To create your deployment.
* Then, to expose and test it locally:
  * `kubectl expose deployments ghost --port=2368`
  * `kubectl proxy`
  * Navigate to `http://localhost:8001/api/v1/namespaces/default/services/ghost/proxy/` in your browser.
