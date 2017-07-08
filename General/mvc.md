# MVC
###### Model-Viewr-Controller
###### A design pattern of software-engineering that defines a way of building & configuring an application

### What are those Model, View and Controller each?
* Model
###### It can be considered data itself and also a bigger unit that processes data. This process includes a database access and data manipulation(CRUD).

* View
###### This is the part of showing we see as users. It takes data provided as a model mentioned above, places it to the right place in the right form and represents it to the users. In short, a way of showing data is set here.

* Controller
###### It defines the relationship between Model and View. Sometimes it make changes to data before giving it to Model or View. Taking data from URI it defines how Model is connected with View.

### Then why is it saparated as three parts and is there any benefit by doing so?
* First of all, we can devide an application into those three parts in terms of purpose : Model, View and Controller
* Second, by doing so we can design, develop, modify, maintain and reuse it independently.
* Which also means that the level of connection & depedency between those parts could decrease.
* This eventually makes it very easy to manage each function as it exists as an individual module.

### Reference
http://webskills.kr/archives/479

https://opentutorials.org/course/697/3828

https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller
