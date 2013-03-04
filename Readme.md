# fastJSON Fork

This is a fork of the [fastJSON](http://www.codeproject.com/Articles/159450/fastJSON) project from Mehdi Gholam.
It is not really meant to be kept in-sync necessarily.

fastJSON uses the [CPOL 1.2 license](http://www.codeproject.com/info/cpol10.aspx)

## Changes from Official

* Name variant support when deserializing. This uses the same logic from RestSharp.
	- `last_name` => `LastName`, `lastName`, etc.
* Root element support. This allows you to specify the first element in the result JSON to use as a starting point for the parser, preventing you from having to create container classes.
	- `fastJSON.JSON.Instance.ToObject<T>(json, rootElement: "container")`
* Auto-generates a multi-targeted Nuget package