# Work at Olist
[Olist](https://olist.com/) is a company that offers an integration platform for sellers and
marketplaces allowing them to sell their products across multiple channels.
The Olist development team consists of developers who loves what they do. Our
agile development processes and our search for the best development practices
provide a great environment for professionals who like to create quality
software in good company ;-) .
We are always looking for good programmers who love to improve their work. We give preference to small teams with qualified professionals to large teams
with average professionals.
This repository contains a problem used to evaluate the candidate skills.
It's important to notice that satisfactorily solving the problem is just a part of the evaluation. We also consider other programming disciplines like documentation, testing, versioning, design and coding best practices. 
Hints: 
- carefully ready the specification to understand all the problem and artifact requirements before start.
- check the recommendations and reference material at the end of this specification.
## How to participate
1. Make a fork of this repository on Github. If you can't create a public fork of this project at Github, make a private repository in bitbucket.org (for free) and add read permission for users @osantana and @dvainsencher on project.
1. Follow the instructions of README.md.
1. Deploy your project on a host service. (we recommend Heroku)
1. Apply for the position at our career page with: 
   * Link to the fork on Github (or bitbucket.org)
   * Link to the project in a the deployed host service
  
## Specification
You should implement a Python application that receives call detail records and calculates monthly bills for a given telephone number. 
This Python application must provide a HTTP REST API to attend the requirements.

### 1. Receive telephone call detail records

There are many telecommunications platforms technologies that can potentially be clients of this system. Each one has its own communication flow. It's no safe to believe that when an already sent record can be resent or retrieved later. This context requires system flexibility in receiving information to avoid record losts.

There are two call detailed record types: **Start call record** and **End call record**. To get all telephone call information you should use the records pair. 

Start call record information:
* **record type**: start/end
* **record timestamp**
* **call identifier** (unique for each call record pair)
* **origin phone number**: The subscriber phone number taht originated the call
* **destination phone number**: The phone number receiving the call
   
The End call record has the same information excepting **origin** and **destination** fields.
The phone number format is *AAXXXXXXXXX*, where *AA* is the area code and *XXXXXXXXX* is the phone number. The phone number can have 8 or 9 digits

**Examples**
1. Start of call record

```
{
  "id": "1c10c9d0-0c8b-4161-8e0e-7e246abcb145",
  "type": "start",
  "timestamp": "2018-01-03T14:18:05.088913",
  "source": "11123456789",
  "destination": "11987654321"
}
```

2. End of call record
```
{
   "id": "1c10c9d0-0c8b-4161-8e0e-7e246abcb145",
   "type": "end",
   "timestamp": "2018-01-03T14:58:05.088913",
}
```

### 2. Get telephone bill 
To get a telephone bill we need two information: the subscriber telephone number (required); the reference period (month/year) (optional). If the reference period is not informed the system will consider the last closed period. In other words it will take the previous month. It's only possible to get a telephone bill after the reference period is ended.
The telephone bill itself is composed by subscriber name and period attributes and a list of all  call records of the period. 

Each telephone bill call record has the fields:
* destination
* call start date
* call start time
* call duration (hour, minute and seconds): e.g 0h35m42s
* call price: e.g R$ 3,96

### 3. Pricing rules

The price of a call depends on the tariff time. There are two tariff times:

1. Standard time call:
   * Apply to calls between 6h00 and 22h00 (excluding)
   * Standing charge: R$ 0,36 (fixed charges that are used to pay for the cost of the connection)
   * Call charge/minute: R$ 0,09 (there is no fractioned charge.)
1. Reduced tariff time call: 
   * Apply to calls between 22h00 and 6h00 (excluding)
   * Standing charge: R$ 0,36
   * Call charge/minute: R$ 0,00 (hooray!)

One last rule is that the price rules can change from time to time, but an already calculated call price can not change.

Examples:

1. For a call started at  21:57:13 and finished at 22:10:56 we have
Standing charge: R$ 0,36
Call charge: 
* minutes between 21:57:13 and 22:00 = 2
* Preço: 2 * R$ 0,09 = R$ 0,18
  Total: R$ 0,18 + R$ 0,36 = R$ 0,54
  
## Project Requirements:

* Choose any Python web framework you want to solve the problem
* Use Python >= 3.5
* Every text or code must be in English
* Use PEP-8 for code style
* Write the project documentation containing:
  * description
  * installing and testing instructions
  * Brief description of the work environment used to run this project (Computer/operating system, text editor/IDE, libraries, etc.).
* Provide an API documentation
* English documentation of API.
* Variables, code and strings must be all in English.

## Recommendations
* Write tests!
* Practice the [12 Factor-App](http://12factor.net) concepts.
* Use [Solid](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)) design principles.
* Use programming good practices.
* Use a good [Python Coding Style](http://docs.python-guide.org/en/latest/writing/style/)
* Use versioning (git) best practices: Make small and atomic commits, with clear messages (written in English).
* Be careful with REST API details. They can bite you!

**Have fun!**
