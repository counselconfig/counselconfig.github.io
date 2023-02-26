---
layout: post
title: Activity and sequence architecture
tags: software behavior diagram flow
---

As you will see in Figure 3, when we use a directed graph with nodes that denotes components and control elements of use case, the execution semantics suffices to represent the stepwise actions of its activity diagrammatically. This feature is inherent in an Activity Diagram, but the means of controlling flow is what adds to the uniqueness of its UML in my view. This is owing to the ability to specify actions based on Petri token principles (Reisig, 2012, p. 3[^fn1]). In other words, actions can be conceptualised as activated events _e_ in places _p_ whenever it receives a passing dot (Seidl, et al., 2012, p. 146[^fn2]).

&nbsp;

![petrinet](/assets/images/petrinet.svg)

_Figure 1 Petri Net (PN) (a) before event (b) after event_

<br>
<br>

<embed src="/assets/images/act.svg">
_Figure 2 Activity diagram_



&nbsp;

Inter-object behaviour is the essence of a Sequence Diagram. If we wanted to specify how partnering objects interact in a use case, this exchange can be plotted as a distribution of sequential messages over time. Accordingly, objects are bound by state transitions with a lifeline connected by message calls that fulfils an executive task. On the flip side, static semantics parallel class organisation used to identify ‘missing objects’ (Bruegge & Dutoit, 2010, p. 185[^fn3]). So, sequence diagrams are different, for we can cross-reference against the UML’s taxonomy in respect to the structure and behaviour of an objects life. Syntactically, its construct is hierarchical, conforming to an ordered branch of roles _r_, classes, _c_ and methods _m_ (Li, et al., 2004, pp. 5-8[^fn4]).


&nbsp;

<object data="{{ site.url }}{{ site.baseurl }}/assets/images/sequence.svg" width="250" height="250" type="application/pdf"></object>

_Figure 3 (a) Sequence (b) hierarchy_

<br>
<br>

<embed src="/assets/images/seq.svg">
_Figure 4 Sequence diagram_

<br>

[^fn1]: Petri Nets - An introduction. First ed. Berlin : Springer-Verlag.
[^fn2]: Seidl, M., Scholz, M., Huemer , C. and Kappel , G., 2012. UML@Classroom - An Introduction to Object-Oriented Modeling. First ed. Heidelberg, Germany : Springer International Publishing
[^fn3]: Bruegge, B. and Dutoit, A.H., 2010. System design: Decomposing the system.
[^fn4]: Li, X., Liu, Z. and Jifeng, H., 2004. A formal semantics of UML sequence diagram. Macau, 2004 Australian Software Engineering Conference. Proceedings.

