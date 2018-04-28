# ASP.NET Cheatsheet
ASP.NET Cheatsheet

## Table of Contents
* [MVC](#mvc)
* [Basic Controller](#basic-controller)
* [Basic View](#basic-view)
* [Razor](#razor)
* [Layout](#layout)

## MVC
Model–view–controller (MVC) is an architectural pattern commonly used for developing user interfaces that divides an application into three interconnected parts. This is done to separate internal representations of information from the ways information is presented to and accepted from the user.

**Controller** accepts input and converts it to commands for the model or view. It is a class which contains actions and functions. A request to controller can be made by 
```url
http://web-address/controller-name/function-name
```

**Model** is responsible for managing the data of the application.

**View** means presentation of the model in a particular format. It can be output representation of information, such as a chart or a diagram. Multiple views of the same information are possible, such as a bar chart for management and a tabular view for accountants.

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
