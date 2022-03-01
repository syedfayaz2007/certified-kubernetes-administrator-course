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
  
  
  
