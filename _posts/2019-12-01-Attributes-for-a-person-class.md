---
layout: post
title: Attributes for a person class
tage: class attributes variables
---
While the transitivity of generalisation passes <span style="font-family:Arial">{abstract}Person</span> class features to multiple child classes, each can have their own additional attributes and operations encapsulated. Class <span style="font-family:Arial">User</span>, for example, has already a unique set of methods, but needs additional attributes such that they ‘partition the universe of objects’ in class <span style="font-family:Arial">{abstract}Person</span> for utility - Dathan & Ramnath (2015)[^fn1]. If a class <span style="font-family:Arial">User</span> is found to be particular useful, and needs extra attributes, a new class can extend from it with the added attributes and methods. To discover attributes that are undefinable for an <span style="font-family:Arial">{abstract}Person</span> class is to find classes that are what Meyer refers to as open for extension so code can be added as an ‘extension’ of the baseclass (Meyer, 1988 [^fn2]).

```java
class User extends Person // class hierarchy extension
{
// User attributes
}
```

Concrete subclasses have two parts. The first, a derived hidden part, and an incremental extended part, forming a ‘substitutable’ subclass for its parent <span style="font-family:Arial">{abstract}Person</span> – Liskov Substitution Principle (1988). A User then will have five attributes that cannot constitute a <span style="font-family:Arial">Person</span>. The first, a (1) <span style="font-family:Arial">UserIDn</span>, - something a Subcontractor cannot possess too – is added with an «invariant» constraint. The rationale for this is that every user will have a user identification number that is not null thereby forming an inheritance contract (Bruegge & Dutoit, 2010 [^fn3]). (2) username, and private login (3) password for a Person is necessary for users to access the system. Since users are employees of the ODS, it would be useful toreveal their National Insurance number (4) <span style="font-family:Arial">nINumber</span> for Pay-As-You-Earn tax. Analysis of use case 1.3 indicates that ODS employees have variable functionality that extends so an enumeration of (5) <span style="font-family:Arial">authorisation</span>, is included in the <span style="font-family:Arial">User</span> class.

<br>

<embed src="/assets/images/derivedatt.svg">
_Figure 1 Dervice attributes_
<br>
<br>
<br>
<br>
<embed src="/assets/images/derivedclasses.svg">
_Figure 2 Five attributes and Java code_
<br>

```java
class User extends Person {
  public int userID;
  public String userName;
  private String password;
  protected String nINumber;
  public UType authorisation;
}
  Enumeration UType {
  root_administrator;
  general_administrator;
  guest_patient;
}
```

[^fn1]: Dathan & Ramnath, 2015. Object-Oriented Analysis, Design and Implementation: An Integrated Approach (Undergraduate Topics in Computer Science)
[^fn2]: Meyer, B., 1988. Object-oriented Software Construction. First ed. Santa Barbara, CA:Prentice-Hall.
[^fn3]: Bruegge & Dutoit, 2010. Object-Oriented Software Engineering Using UML, Patterns, and Java: Pearson New International Edition
