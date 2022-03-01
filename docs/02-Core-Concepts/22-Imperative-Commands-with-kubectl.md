# Certification Tips - Imperative Commands with kubectl
  - Take me to the [Tutorial](https://kodekloud.com/courses/539883/lectures/10503265)


Imperative --> Need to provide step by step to acheive the required results
Declarative --> It's simply inform the deired state then system will take care and make the system in required state.

Imperative comes under 2 ways -- 
  Throug commands such 
  CREATE  --> run, create , expose
  UPDATE  --> edit scale set
  DELETE 
  
  Through configuratin files --yaml files
  kubectl edit deploymnet nginx --> then it opens a object (K8 memory file) .. it's not actual file which you used to create object. The changes apply to live objects. Not at acutal source file. In future, new people may not know by seeing the file. 
  
  Use --> replace command instead of edit. 
  
  What happens if the ojbect is already exists when you are creating --> it fails
  same as when you update ... if object not exists --> it fails
  
  
  DECLARATIVE -- 
  Apply command helps to create objects and checks 
  if it already exists then it won't throw error
  
  
  While you would be working mostly the declarative way - using definition files, imperative commands can help in getting one time tasks done quickly, as well as generate a definition template easily. 
  
  --dry-run: By default as soon as the command is run, the resource will be created. If you simply want to test your command , use the --dry-run=client option. This will not create the resource, instead, tell you whether the resource can be created and if your command is right.

-o yaml: This will output the resource definition in YAML format on screen.
  
  
  Kubectl Apply Command : 
  When you run apply command by using yaml file 
  then it will create a new object file config with in K8 memory with few additional status parameters. 
  
  When you run apply command then it does few more things internally. 
  - it first creates the json file as last applied configuration.  Going forward any changes happened it will compare all three files. 
  - Ex : if any changes on the yaml file then it will compare with live object ... As a last step it will update the json file of last applied configuration. 
  - 
