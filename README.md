# weatherman

The application is designed to take a 5 digit US zip code, and return the current weather conditions and temperature for the zip code.   Additionally, you can use the "Lookup my location" button to have the browser detect your approximate lat and long coordinates, and then use reverse Geocoding to determine an approximate Zip code. (Note: The calls that are made to the Google Maps API all indicate that the current device does NOT have a true GPS sensor. Even if you are accessing the website through a phone or tablet that does have a true GPS sensor.)  Once a valid 5 digit Zip code is entered, the application uses "World Weather Online" API (http://www.worldweatheronline.com/). For the purpose of this exercise the calls made "server-side" to this API are all done synchronously.

If desired the user, can create an account on the site, which then allows the user to add, previously searched for Zip codes to a "favorites" list.  Once logged into the website another navigation link called "Favorites" is visible.  


To open the code you will want to use Visual Studio 2013 and open "Weatherman.sln"

The "web.config" file contains two connection strings "DefaultConnection", and "weathermanEntities".  They currently point to a database called "weatherman" on the local SQL Express instance.  

In the "/Weatherman/db" directory there is a file "CreateSchema.sql" that can be run to create the database schema.



The application is split up into 3 projects.  
*/Weatherman/Weatherman/WeathermanWeb.csproj
*/Weatherman/WeathermanDataLayer/WeathermanDataLayer.csproj  (Had I had more time, I would have split this into two projects.  As it is now, the service layer knows too much about the data layer. Entity Framework's context, etc.)
*/Weatherman/WeathermanServiceLayer/WeathermanServiceLayer.csproj


The basic idea behind having the three projects was to make sure that no views were directly bound to any of the Entity Framework models, and to be able to switch out the calls to the weather service API.  

The "WeathermanServiceLayer" has a directory "/interfaces/" which contains the "IWeatherLookupService". The "/CastleWindsor/ServiceRegistry.cs" class dictates which concrete implementation of the interfaces to use.  However, the MVC Controllers in the "WeathermanWeb" project only interact with the methods and properties defined in the "IWeatherLookupService".  


I posted a "running" version of the application at http://www.toothdominos.com/. 






Pre-requisites:

* Visual Studio 2013 (Not sure if this will load on 2012 or 2013 Express.  I did not get a chance to test on those.)
* SQL Server 2008 R2 (Express) or higher.
* .Net Framework 4.5


Components used:

* ASP.NET MVC
* Bootstrap for UI
* Castle Windsor as the IoC container.
* Bootstrapper for configuration of Castle Windsor (and Automapper which I ended up not using)
* Entity Framework as the ORM
* jQuery, etc.









