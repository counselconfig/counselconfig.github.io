---
layout: post
title: O-O class modeling
tag: object oriented architectural modeling
---

This blog shows how a new dental system was developed for a small dental practice using O-O class modelling architecture.

There is a <span style="font-family:Arial">Root_administrator</span> with different functions from a <span style="font-family:Arial">General_administrator</span>. It may be assumed that the remaining staff classes can also follow suit to fulfil inheritance from an intermediary General_administrator class. Studying the problem statment yields core entities:

<br>

<!--<embed src="/assets/images/emptyclasses.svg">-->
![initclass](/assets/images/emptyclasses.svg "Initial Classes")
<!--<img src="/assets/images/emptyclasses.svg">-->

_Figure 1 Initial classes acertained from problem statement_

The classes are arranged in the manner of class inheritance e.g.

```java
class Person {
  // methods and fields
}

// extends keyword for inheritance
class Subcontractor extends Person  {

  // methods and fields of Person 
  // methods and fields of Subcontractor
}
```


<br>
![preinherit](/assets/images/preinheritance.svg "Pre-inheritance")
<br>
_Figure 2 Preliminary class structure_

The <span style="font-family:Arial">Subcontractor</span> class has an opposite discriminator set. A subclass of <span style="font-family:Arial">Subcontractor</span>class cannot be a combined instance of another subclass, but could be extended – that is, other types of Subcontractor ‘S’ may be stored in the database.

<br>
![inherit](/assets/images/inheritance.svg "inheritance")
<br>
_Figure 3 Formal inheritance - S_
<br>

Methods and fields are added to the preliminary class structure via associations (including aggregration and qualifiers - figure 4,  and a final draft class structure is built - figure 5:


<br>
![ass](/assets/images/association.svg "Association")
<br>
_Figure 4 Class association User – spT_Case_

<br>
<embed src="/assets/images/classdiagram.svg">
_Figure 5 First draft class diagram_
<br>
