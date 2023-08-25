# Folder Struture

On Demand Druid Exhaust Job Service folder structure is designed to organize the different modules and files. It follows a modular approach, facilitating easy management and development of the service.

### The structure is as follows

<pre><code>.
├── main    
<strong>│   └──  exhaust
</strong>│       ├── OnDemandBaseExhaustJob.scala
│       └── OnDemandDruidExhaustJob.scala
└── Test    
    └── exhaust
        └── TestOnDemandDruidExhaustJob.scala
</code></pre>

**main.exhaust**&#x20;

This main directory houses our On Demand Druid Exhaust data-product. The _OnDemandDruidExhaustJob.scala_ file contains main method which internally triggers other functions. _OnDemandBaseExhaustJob.scala_ file contains generic functions such as execution, data transformation, storage in blob storage, and retrieval of file paths.

**test.exhaust**&#x20;

In the exhaust folder we have the main test case file called _TestOnDemandDruidExhaustJob.scala_ that is used to test our data-product.

### **Source code**

{% @github-files/github-code-block %}
