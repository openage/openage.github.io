---
layout: docs
title: Departments
permalink: /docs/directory/departments
---


#### Model

```JSON
{  
  "name": "string",  
  "code": "string",  
  "inCharge": "string",
  "division": "string"  
}
```

 **Create department**  

[Try it out](http://ems-api-dev.m-sas.com/#!#departments)


**search an department**  
> Search  
  
<h3><a href="http://ems-api-dev.m-sas.com/#!#dependents">Dependents</a></h3>

**Create dependents**

>create
{% highlight ruby %}
{  
  "phone": "string",  
  "email": "string",  
  "profile": {  
    "firstName": "string",  
    "lastName": "string",  
    "dob": "string",  
    "fatherName": "string",  
    "bloodGroup": "string",  
    "gender": "string"  
  }  
}  
{% endhighlight %}

**Create dependents in bulk**  

>create in bulk  
{% highlight ruby %}  
{  
  "dependents": [  
    {  
      "phone": "string",  
      "email": "string",  
      "profile": {  
        "firstName": "string",  
        "lastName": "string",  
        "dob": "string",  
        "fatherName": "string",  
        "bloodGroup": "string",  
        "gender": "string"  
      }  
    }  
  ]  
}  
{% endhighlight %} 
