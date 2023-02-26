---
layout: post
title: Class associations
tags: class object
---

Where there is a persistent non-hierarchal relation between at least two classifiers, and their instantiated links have common semantics and structures, an ‘association’ is formed. This means that an association is both conceptually and physically disposed, for if class *C*<sub>1</sub> has a binary association *A* with class *C*<sub>2</sub>, a given object of the former will be related to the latter.
<br>
<br>
<br>
<embed src="/assets/images/classbinary.svg">
_Figure 1 Class binary association_

<br>
<br>

### Clinical_Director – Patient


Operation <span style="font-family:Consolas; color:green;">getReport()</span> is defined in the <span style="font-family:Arial;">Patient</span> class preliminary diagram in my earlier blog. This refers to a named method that vests object behaviour bound by a ‘contract or obligation’ of the Patient classifier to disclose records. In other words, a <span style="font-family:Arial;">Patient</span> object has responsibility to give information about itself at the call of knowing objects, so class methods and attribute visibilities are set to public. This is ‘need to know’ management information for a <span style="font-family:Arial;">Clinical_Director</span> object related to an arity __m__ of one:many <span style="font-family:Arial;">Patient</span> objects.

<br>
<br>
<embed src="/assets/images/objectdiagram.svg">
_Figure 2 Object diagram_

A collection class should be used to gather the instances of <span style="font-family:Arial;">Patient</span> objects with each having a reference kept in a vector implementing Java library <span style="font-family:Consolas; color:green;">java.util</span> 
<br>
<br>
<embed src="/assets/images/assovector.svg">
_Figure 3 Class binary association_

<br>

### Orthodontist – Dental assistant

A use case with a precondition ‘A Dentist must write their instructions in the Patient referral case.’ sets us on course to finding an association between <span style="font-family:Arial;">Orthodontist</span> and <span style="font-family:Arial;">Dental_Assistant</span>. A dentist may devolve this precondition to dental assistants who would locate the appropriate Orthodontist to write an instruction email. An <span style="font-family:Arial;">Orthodontist</span> object, from a collection, returns details of the chosen practitioner to outsource. Physically, this association is ‘bi-directional’ with multiplicity <span style="font-family:Arial;">[1..*]</span> at either end.
<br>
<br>
<embed src="/assets/images/biobject.svg">
_Figure 3 Object diagram – Bi-directional links in varying notation_
<br>
<br>
<br>
<br>
<embed src="/assets/images/plauassociation.svg">
_Figure 4 Plausible association Dental_Assistant – Orthodontist_

The association diagram in Figure 4 is missing intermediary elements. This is because use case 1.3 states that it is a <span style="font-family:Arial;">Root_administrator</span> object that sends, but not writes, a commissioning email to an Orthodontist. It also confirms that this communication is associated with a ‘referral queue hub’ to which cases are sent. The sequence between each class can be summarised in an n-array association.
<br>
<br>
<embed src="/assets/images/n-array.svg">
_Figure 5 Plausible n-array association_


