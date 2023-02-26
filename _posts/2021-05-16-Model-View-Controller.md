---
layout: post
title: Model View Controller note
tags: patterns application layers
---

The Model-View-Controller (MVC) is a well known software pattern to architect an entire appplication - here are some notes about it. 

MVC can be acheived with ASP.NET Core to partition the required layers (Troelsen & Japikse, 2020)[^fn1]. The MVC handles the bidirectional communications with a user of a graphical interface via a ‘controller’. The controller is a broker in the business layer to handle input for a ‘model’ at the data layer behaving as the state for a rendered ‘view’ at the presentation layer (Parson, 2020). Because an MVC derives from O-O programming (Thakur & Pandey, 2019)[^fn2], it also made a suitable ASP.NET Core architecture for object creation, following Figure 1.

<br>

<embed src="/assets/images/layeredmvc.svg" width="60%" height="60%" style="display: block; margin: 0 auto">

_Figure 1 Layered and tiered MVC architecture - adapted from Dissanayake & Dias (2017) and Liu & Gupta (2019)[^fn3][^fn4]_

<br>

This model was a real product I developed for an online hardware shop, note that tiers are not synonymous with layers. They are both architectures typically divided thrice, but the former relates to the physical deployment and the latter to the repository structure (Esposito & Saltarello, 2014)[^fn5]. MVC initiation can be found in the `startup.cs` public class method `services.AddControllersWithViews();`. This brings into effect the layers: `Controllers`, `View`, `ViewModels`, and `Models`. The decision to have a viewmodel was created as a way to contain listed transitory categorised hardware data that could be constructed in a `HardwareController` first and then passed to the `HardwareListViewModel` at the presentation layer:

```c#
namespace MVC_DL.ViewModels
{
    public class HardwareListViewModel
    {
        public IEnumerable<Hardware> Hardwares { get; set; }
        public string CurrentCategory { get; set; }
    }
}
```
This is an architecture often associated with Model-View-ViewModel scaffolding where `ViewModel` represents the `View` state with changeable data (Kouraklis, 2016)[^fn6].

Thge MVC is not a static artifact, but rather a kinetic system - bekiw is a portrayal.


<embed src="/assets/images/mvcpipeline.svg" width="100%" height="100%" style="display: block; margin: 0 auto">

<center><i>Figure 2 ASP.NET MVC Pipeline Request Lifecycle - adapted from Simple Talk (2011)</i></center>


[^fn1]: Troelsen, A. & Japikse, P., 2020. MVC Applications with ASP.NET Core. In: Pro C# 8 with .NET Core 3. Berkeley, CA:Apress.
[^fn2]: Thakur, R. N. & Pandey, U. S., 2019. The Role of Model-View Controller in Object Oriented Software Development.. Nepal Journal of Multidisciplinary Research, 2(2), pp. 1-6.
[^fn3]: Dissanayake, N. R. & Dias, G. . K. A., 2017. Balanced Abstract Web-MVC Style: An Abstract MVC Implementation for Web-based Applications. GSTF Journal on Computing (JoC), 5(3), pp. 27-41.
[^fn4]: Liu, Z. & Gupta, B., 2019. Study of Secured Full-Stack Web Development. Honolulu, Hawaii, USA, Proceedings of 34th International Conference on Computers and Their Applications, p. 317–324.
[^fn5]: Esposito, D. & Saltarello, A., 2014. Microsoft .NET - Architecting Applications for the Enterprise. Second ed. Redmond, Washington: Microsoft Press.
[^fn6]: Kouraklis, J., 2016. MVVM in Delphi: Architecting and Building Model View ViewModel Applications. London, United Kingdom: Apress.

