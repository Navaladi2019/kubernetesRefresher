- comfig maps are defined as key value pairs and these can be referred in pod definition file


kubectl create configmap <config map name> \ --from-literal=APP_COLOR=blue \ --from-literal=APP_MOD=prod