

DoubleRouteConstraint Class
===========================






Constrains a route parameter to represent only 64-bit floating-point values.


Namespace
    :dn:ns:`Microsoft.AspNetCore.Routing.Constraints`
Assemblies
    * Microsoft.AspNetCore.Routing

----

.. contents::
   :local:



Inheritance Hierarchy
---------------------


* :dn:cls:`System.Object`
* :dn:cls:`Microsoft.AspNetCore.Routing.Constraints.DoubleRouteConstraint`








Syntax
------

.. code-block:: csharp

    public class DoubleRouteConstraint : IRouteConstraint








.. dn:class:: Microsoft.AspNetCore.Routing.Constraints.DoubleRouteConstraint
    :hidden:

.. dn:class:: Microsoft.AspNetCore.Routing.Constraints.DoubleRouteConstraint

Methods
-------

.. dn:class:: Microsoft.AspNetCore.Routing.Constraints.DoubleRouteConstraint
    :noindex:
    :hidden:

    
    .. dn:method:: Microsoft.AspNetCore.Routing.Constraints.DoubleRouteConstraint.Match(Microsoft.AspNetCore.Http.HttpContext, Microsoft.AspNetCore.Routing.IRouter, System.String, Microsoft.AspNetCore.Routing.RouteValueDictionary, Microsoft.AspNetCore.Routing.RouteDirection)
    
        
    
        
        :type httpContext: Microsoft.AspNetCore.Http.HttpContext
    
        
        :type route: Microsoft.AspNetCore.Routing.IRouter
    
        
        :type routeKey: System.String
    
        
        :type values: Microsoft.AspNetCore.Routing.RouteValueDictionary
    
        
        :type routeDirection: Microsoft.AspNetCore.Routing.RouteDirection
        :rtype: System.Boolean
    
        
        .. code-block:: csharp
    
            public bool Match(HttpContext httpContext, IRouter route, string routeKey, RouteValueDictionary values, RouteDirection routeDirection)
    

