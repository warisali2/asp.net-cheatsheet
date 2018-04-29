# ASP.NET Cheatsheet
ASP.NET Cheatsheet

## Table of Contents
* [MVC](#mvc)
* [Controller](#controller)
  * [Basic Controller](#basic-controller)
  * [Action Verb](#action-verb)
* [Basic View](#basic-view)
* [Razor](#razor)
* [Layout](#layout)
  * [Specify Layout for a View](#specify-layout-for-a-view)
  * [Section in a Layout](#section-in-a-layout)
  * [Basic Layout](#basic-layout)
* [Send Data from Controller to View](#send-data-from-controller-to-view)
  * [View Bag](#viewbag)

## MVC
Model–view–controller (MVC) is an architectural pattern commonly used for developing user interfaces that divides an application into three interconnected parts. This is done to separate internal representations of information from the ways information is presented to and accepted from the user.

**Controller** accepts input and converts it to commands for the model or view. It is a class which contains actions and functions. A request to controller can be made by 
```url
http://web-address/controller-name/function-name
```

**Model** is responsible for managing the data of the application.

**View** means presentation of the model in a particular format. It can be output representation of information, such as a chart or a diagram. Multiple views of the same information are possible, such as a bar chart for management and a tabular view for accountants.

# Controller
Controller accepts input and converts it to commands for the model or view. It is a class which contains actions and functions.

## Basic Controller
(As per ASP.NET MVC's conventions) Create a *BasicController.cs* in Controllers directory and add following code
```C#
using System.Web.Mvc;

namespace myWeb.Controllers
{
  public class BasicController : Controller
  {
    public ActionResult Index()
    {
      return View();
    }
  }
}
```
To call this action, go to
```url
http://web-address/basic/index/
```
It will return the HTML code in *index.cshtml* file placed in *Views* folder.

**Note:** We use *basic* instead of *BasicController* in URL for controller name.

## Action Verb
Action Verbs are used to control the selection of action based on request method. There are different action verbs available in ASP.NET MVC. For example `HttpPost`, `HttpGet` and `HttpDelete`

```C#
[HttpGet]
//Accepts only Get requests
public ActionResult GetMethod(int id) { ... }

//Accepts both Post and Get requests
[AcceptVerbs(HttpVerbs.Post | HttpVerbs.Get)]
public ActionResult PostAndGetMethod(MyEditViewModel myEditViewModel) { ... }
```

## Basic View
(As per ASP.NET's conventions) Create *hello.cshtml* in *Views* folder and add following code
```html
<h1>Hello ASP.NET</h1>
```
Now, you can add function for this view in your controller.

## Razor
Razor is a markup syntax for embedding server-based code into webpages. The Razor syntax consists of Razor markup, C#, and HTML. Files containing Razor generally have a .cshtml file extension.

For more details, visit [A Razor Cheatsheet](https://github.com/warisali2/razor-cheatsheet).

# Layout
Most web apps have a common layout that provides the user with a consistent experience as they navigate from page to page. The layout typically includes common user interface elements such as the app header, navigation or menu elements, and footer.

By convention, the default layout for an ASP.NET app is named `_Layout.cshtml`. This layout defines a top level template for views in the app. Apps don't require a layout, and apps can define more than one layout, with different views specifying different layouts.

## Specify Layout for a View
Razor views have a `Layout` property. Individual views specify a layout by setting this property:
```
@{
    Layout = "_Layout";
}
```

The layout specified can use a full path (example: `/Views/Shared/_Layout.cshtml`) or a partial name (example: `_Layout`). When a partial name is provided, the Razor view engine will search for the layout file using its standard discovery process. The controller-associated folder is searched first, followed by the Shared folder. This discovery process is identical to the one used to discover partial views.

By default, every layout must call `RenderBody`. Wherever the call to `RenderBody` is placed, the contents of the view will be rendered.

**Note:** Default layout is defined in `Views/_ViewStart.cshtml` file.

## Section in a Layout
Sections provide a way to organize where certain page elements should be placed. A layout can optionally reference one or more sections, by calling `RenderSection`. Each call to `RenderSection` can specify whether that section is required or optional. If a required section isn't found, an exception will be thrown. Individual views specify the content to be rendered within a section using the `@section` Razor syntax. If a view defines a section, it must be rendered (or an error will occur).

An example `@section` in a view:
```html
@section Scripts 
{
     <script type="text/javascript" src="/scripts/main.js"></script>
}
```

## Basic Layout
(As per ASP.NET conventions) Create a `_MyLayout.cshtml` file in `~/Views/Shared/` folder and add following code
```html
@
{
 Layout = null;
}
<html>
 <head>
  <title>My Web</title>
 </head>
 <body>
   @RenderBody()
   
   <div id="footer">
     @RenderSection("footer", false);
   </div>
 </body>
</html>
```

Code of view that uses this layout:
```html
@
{
 Layout = "~/Views/Shared/_MyLayout.cshtml";
}

<p> Body of view </p>

@section footer
{
 <p>Footer area</p>
}
```

HTML that will be rendered for this view is:
```html
<html>
 <head>
  <title>My Web</title>
 </head>
 <body>
   <p> Body of view </p>
   
   <div id="footer">
     <p>Footer area</p>
   </div>
 </body>
</html>
```

# Send Data from Controller to View
There three ways to send data from Controller to View.

## ViewBag
ViewBag can be useful when you want to transfer temporary data (which is not included in model) from the controller to the view. The ViewBag is a dynamic type property. You can assign any number of properties and values to ViewBag. If you assign the same property name multiple times to ViewBag, then it will only consider last value assigned to the property.
 
 **Note:** The ViewBag's life only lasts during the current http request. ViewBag values will be null if redirection occurs.
 
 We use dot notationg to send data from controller.
 ```c#
 public ActionResult Index() //We'll set the ViewBag values in this action
{
    ViewBag.PageTitle = "This is the page title";
    ViewBag.PageDescription = "This is the page description.  We'll make it rather longer.";

    return View();
}
 ```
 
 This can be accessed in the view like @ViewBag.PageTitle.
 ```html
<h3>@ViewBag.PageTitle</h3>

<p>
    @ViewBag.PageDescription
</p>
```

 **Note:** ViewBag is a wrapper around ViewData. It will throw a runtime exception, if the ViewBag property name matches with the key of ViewData.
