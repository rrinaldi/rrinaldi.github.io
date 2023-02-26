---
title: Grouping controls arbitrarily
date: 2004-06-08
---
Sometimes when building a page, I find that I need to group controls
together so I can show/hide them at the same time, or perform a similar
action on all of them.  Most of the time I can put them in a panel and
just show/hide the panel.  Other times though the controls are located
on various sections of the page that I can't put in a panel because the
panel would affect more controls than I want.  So I wrote a little
function that will allow me to arbitrarily group server controls on a
page.  To use it, you need to add a attribute to your server controls. 
You can call this attribute what ever you want and can give it any value
that you want.  Then just call the little function (source code below)
and it will return an ArrayList of the controls.  The even cooler part
is that the attributes and their values get pushed to the client so you
can even use them client side with a little bit of JavaScript. :) 
Hopefully you'll find it handy.

```csharp
        /// 
         /// Returns an ArrayList of Controls that have the specified
attributeName and attributeValue.
         /// If attributeValue is null, it will return controls that
only have the specified attributeName
         /// 
         /// Name of the attribute to look for
         /// Value of the attribute specified in attributeName.
         /// ControlsCollection to look in
         /// ArrayList of Controls
         protected ArrayList GetControlsByAttribute(string
attributeName, string attributeValue, ControlCollection controls)
         {
             ArrayList myControls = new ArrayList();
             
             foreach(Control control in controls)
             {
                 if(control.HasControls())
                 {
                     ArrayList childControls =
GetControlsByAttribute(attributeName, attributeValue,
control.Controls);
                     foreach(Control childControl in childControls)
                     {
                         myControls.Add(childControl);
                     }
                 }
 
                 System.Reflection.PropertyInfo[] props;
                 props = control.GetType().GetProperties();
 
                 for(int i = 0; i < props.Length; i++ )
                 {
                     if( props[i].Name == "Attributes" )
                     {
                         System.Web.UI.AttributeCollection ac =
(System.Web.UI.AttributeCollection) props[i].GetValue(control, null);
                         
                         if( attributeValue != null )
                         {
                             if( ac[attributeName] == attributeValue)
                             {
                                 myControls.Add(control);
                             }
                         }
                         else
                         {
                             if( ac[attributeName] != null)
                             {
                                 myControls.Add(control);
                             }
                         }
                         break;
                     }
                 }
             }
             return myControls;
         }
```