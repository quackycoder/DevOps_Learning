### [Taken from this video](https://youtu.be/1uFVr15xDGg)

### We will see what __YAML__ is used for and we'll go through the syntax of how to write a valid __YAML__ file.

- Most of the configuration files are written in yaml because it has become a pretty widely used format for writing configurations for many different DevOps tools and applications. 
- That's why when using these tools, it's important to understand the details of yaml syntax and its main concepts.
- Generally speaking, __YAML__ is a serialization language just like __XML__ and
__JSON__.
- Serialization language basically means that applications written in different technologies languages etc which have different data structures can transfer data to each other using a common agreed-on or a standard format.

- The most popular such formats are `YAML` `JSON` and `XML`. 
- The name __YAML__ actually stands for YAML Ain't Markup Language.
- You can create YAML file with one of those two extensions: `.yaml` or `.yml`. 
- They're the same. 
- One of the main reasons of why YAML _popularity has increased_ so much over the past years is that it's super __human readable__ and __intuitive__ which makes it a _great fit for writing configuration files_ for all those recent DevOps tools like docker kubernetes etc.

- Let's see a comparison between YAML, XML, and JSON formats:

## - This is how YAML file would look like:
```
microservices:
  - app: user-authentication
    port: 9000
    version: 1.0
```
- It's very straightforward. It's pretty clean. 

## - This is the same data in XML format:
```
<microservices>
  <microservice>
    <app>user-authentication</app>
    <version>1.0</version>
  </microservice>
<microservices>
```
## - Then you have the JSON format
```
{
  microservices: [
    {
      app: "user-authentication",
      port: 9000,
      version: "1.0"
    }
  [
}
```
- As you see in XML and JSON data structures are defined using special characters. 
- In XML, you have so-called __text with angle brackets__ and in JSON, you have __curly brackets__.
- But in YAML, you don't have those special characters.
- So data structure is defined in the YAML is through __line separations__ and __spaces with indentations__.
- That's why you can __indent__ in space in XML and JSON as you wish BUT in the YAML, you get __validation error__ if you have _one single space_ and data structure wrong which may be a little bit annoying.
- But it makes YAML format __the cleanest, most human readable format__ of all three. 

- Some of the most use cases YAML format is used for __docker composed files__, __Ansible__,  __prometheus__, __kubernetes__ and many more tools.

- Now let's dive into YAML syntax:

 - It started with the basic syntax which is simple __key value pairs__. 
 
 - Let's take an example:
   
```
app: user-authentication and we have a
port: 9000
version: 1.7 
```
- These are simple __key value pairs__ 
- You have different datatypes here.
- We have a _string_ which, __note that__ we _don't have to enclose_ it with _quotes_. 
- You can if you want to. You can use either __double
03:37
quotes__ or __single quotes__ or __no quotes__ at all unless you use special character like line
03:47
character ("\n").
- In YAML, you also have __comments__. So everything that starts with #, YAML interprets as a _comment_.

- To make my file even __more readable and understandable__, you can group the __key-value pair__ inside of an __object__. 

- You can create an __object__ in YAML and you can do that by indenting the individual __key-value pairs__ and __enclosing it in an object__.

- Let's call the object: microservice like in the above YAML example.

- __Note__ that the __space has to be exactly same__ for __each attribute__ _within the object_.

- As YAML is so __sensitive about the spaces__ and __indentation__, it's always a good idea to use a [_YAML validator_](http://www.yamllint.com/) before you execute a configuration file in kubernetes. 

- In YAML, you can also have __lists__.

- For example, if you have multiple microservices, I can create a list of those microservices simply by using __-__. like in the example above. 
- __Important__ thing that those _attributes_ __stay at the same level__.

- You can also have boolean values. 
- For example, if we have deployed attributes. So you can say __true__ or __false__ and, also you can express boolean expressions with __yes__ or __no__, also with __on__ or __off__. All these 3 pairs of values are expressions of boolean values.
```
microservices:
  - app: user-authentication
    port: 9000
    version: 1.0
    deployed: true/yes/on
    # deployed: false/no/off
```
- So this is a list and these are the items of the list.

- I can add second item, let's say, shopping-cart, or whatever with port 9002 and version 1.9 
```
microservices:
  - app: user-authentication
    port: 9000
    version: 1.0
  - app: shopping-cart
    port: 9002
    version: 1.9
```

- This way you can define __lists of objects__.

- You can also define __lists of simple values__. For example, if you had a list of just the microservice names you could do like this:
```
microservices:
 - user-authentication
 - shopping-cart
```

- You can also use lists inside of a list item. For example, if you have _multiple versions_ of a shopping-cart that you want to list here for some reason, you can actually list them like this: 
```
microservices:
  - app: user-authentication
    port: 9000
    version: 1.0
  - app: shopping-cart
    port: 9002
    versions:
    - 1.9
    - 2.0
    - 2.1
```
- Don't be confused if you see different alignments of the lists. Both work because YAML recognizes that it's a _list item_.
- What will not work is if you don't align the list items using indentation.
- You can also use square brackets to wrap the multiple items like in case of version which makes it more readable: 
```
microservices:
  - app: user-authentication
    port: 9000
    version: 1.0
  - app: shopping-cart
    port: 9002
    versions: [1.9, 2.0, 2.1]
```
-

- To make it more practical and realistic, let's actually look at real kubernetes YAML example to see how these basic syntax is expressed there.

- Let's look at a pod configuration 
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: nginx-vol
      mountpath: /usr/nginx/html
  - name: sidecar-container
    image: some-image
    command: ["/bin/sh"]
    args: ["-c", "echo Hello from sidecar-container; sleep 300"]  
```

- So, this is basically the main part where the __metadata__ and __kind__ etc is defined.
- You can see these are super simple _key-value pairs_ and then you have these _objects_.
- You have the __spec__ and __containers__ and in containers, a list.
- Let's use nginx as image, then you have __ports__ which is another list.
- So again we start with __-__ to list ports.
- Then you have the attribute which is container port value there.
- Inside container, you also can have __volumeMounts__ which is another list.
- Here you list all your __volumes__ and this is a list of objects.
- Again we have _key-value pairs_
- This is how a pod configuration will look like.
- You can also have multiple containers inside.For example if I were to define a __sidecar__ container, I would have another item expression __-__
- __Note__ you can deploy a _curl_ image as a sidecar. 

- So knowing how YAML syntax works should make it easier to understand the kubernetes configuration file structure better.

- Another important concept of YAML syntax is when you have multi-line strings. 
- For example file contents multi-line string and the way I can do that is by using the __pipe |__ symbol.
```
multilinestring: |
  this is amultiline string
  for which i need to use a pipe 
  symbol.
```
- So YAML will see that character and will interpret everything here as a multi-line text. so this line breaks("\n") will actually stay.

- Another case could be if you have this super long string which has to be on a single line, for example, this is a single line string that should be all on one line, but you also don't want to write all out on one line because it's
13:14
just not very readable.
- That's why you want YAML to interprete as a single line. So instead of pipe, you actually replace it with a __greater than sign >__ and this will be interpreted as single line. 

- Let's use some real use cases: I have a config file of kubernetes and here you see the basic key-value stuff and name of the attribute.
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: mosquitto-config-file
data:
  mosquitto.config: |
    log_dest student
    log_type all
    log_timestamp true
    listener 9001
```
   
- We use that pipe and these are actually the contents of the file. This is going to be displayed exactly like this with line carriages because this has to be each one on its own line and this way you can actually write configuration files for different applications like this one is for mosquitto, you also have for fluentd and they have their own different formats and you can write the whole thing as a file represented by multi-line string in YAML.

- Another example of using this multi-line string that you may actually encounter in kubernetes configuration files is this one:
```
command:
 - sh
 - -c
 - |
   #!#/usr/bin/env bash -e 
   http () {
        local path="${1}"
        set -- -XGET -s --fail
        # some more stuff here
        curl -k "$@" "http://localhost:5601${path}"
   }
   http "/app/kibana"
```

- This is part of configuration of a pod. So you have this __command__ attribute, list and pipe that is followed by a multi-line string and this is an example of kibana. 
So basically what it does is that it executes shell command and this is a shell script so you can actually put the whole contents of a shell script as you would have that as shell script file after that pipe symbol as a multi-line text and this will execute as a shell script.

- One thing that I've also needed to use in YAML was environmental variables.
- For example if a pod that has environmental variables defined inside and you have to use one of those inside the pod configuration, you can actually access them using a __dollar sign $__ inside your YAML configuration.
- So this is an example of a mySQL pod:
```
#readiness prob
command:
  - /bin/sh
  - -ec
  - >-
    mysql -h 127.0.0.1 -u root -p$MYSQL_ROOT_PASSWORD -e 'SELECT 1'
```

- You have the comment and we are executing a mySQL command.
- I am accessing the environmental variable that is available inside the pod using the name of the environmental variable and the dollar sign $ before that.

- YAML also has a concept of placeholders one of its use cases is in
16:13
HELM.
- For example, instead of directly writing the values inside, you define placeholders and the syntax for using placeholders is double curly braces {} around that placeholder.
```
apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.service.name }}
spec:
  selector:
    app: {{ .Values.service.app }}
  ports:
    - protocol: TCP
      port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.targetport }}
``` 

- This value gets replaced using template generator and I believe the same concept is used in Ansible as well.
- So if you use HELM or in Ansible and you see this syntax, you should know what it stands for!

- Lastly, inside one YAML file, you can actually define multiple components and you can separate these components using three dishes like this:

A yellow file where I want to put all my configurations:
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: mosquitto-config-file
data:
  mosquitto.config: |
    log_dest student
    log_type all
    log_timestamp true
    listener 9001

---
apiVersion: v1
kind: Service
metadata:
  name: {{ .Values.service.name }}
spec:
  selector:
    app: {{ .Values.service.app }}
  ports:
    - protocol: TCP
      port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.targetport }}

---

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: nginx-vol
      mountpath: /usr/nginx/html
  - name: sidecar-container
    image: some-image
    command: ["/bin/sh"]
    args: ["-c", "echo Hello from sidecar-container; sleep 300"]  
```

- This will be a valid YAML file and this can be very handy in case especially where you have multiple components like service and you want to group them in a single YAML file.
So for that use case this is the way to go!

Note that in kubernetes dashboard, if you click to edit one of your components, You can see both YAML and JSON formats available.
 
