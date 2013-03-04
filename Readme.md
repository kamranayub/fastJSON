# fastJSON Fork

This is a fork of the [fastJSON](http://www.codeproject.com/Articles/159450/fastJSON) project from Mehdi Gholam.
It is not really meant to be kept in-sync necessarily, it just has some features that I need.

fastJSON uses the [CPOL 1.2 license](http://www.codeproject.com/info/cpol10.aspx).

Name variance based on [RestSharp](https://github.com/restsharp/RestSharp/blob/master/RestSharp/Extensions/StringExtensions.cs) (Apache 2.0).

## Changes from Official

* Windows Phone support out-of-the-box
* Name variant support when deserializing. This uses the same logic from RestSharp.
	- `last_name` => `LastName`, `lastName`, etc.
* Root element support. This allows you to specify the first element in the result JSON to use as a starting point for the parser, preventing you from having to create container classes.
	- `fastJSON.JSON.Instance.ToObject<T>(json, rootElement: "container")`
* Auto-generates a multi-targeted Nuget package

## Name Variance

	// Defaults
	fastJSON.JSONParameters.MatchNameVariantsOnDeserialize = false;
	fastJSON.JSONParameters.EnabledNameVariantFlags = NameVariants.PascalCase;

If your service/API returns a JSON response like this:

```
	{
		"first_name": "Kamran",
		"last_name": "Ayub"
	}
```

And you have a POCO class:

```
	public class Person {
		public string FirstName { get; set; }
		public string LastName { get; set; }
	}
```

fastJSON will not match the property names up as it expects an exact or lowercase match.

However, with the name variance feature, it will properly discover and match up the properties. This adds some extra
overhead, so you can enable it like this:

	fastJSON.JSONParameters.MatchNameVariantsOnDeserialize = true;

Since each variant has a perf impact, you can enable/disable them when you know what response you expect back:

	fastJSON.JSONParameters.EnabledNameVariantFlags = NameVariants.PascalCase;

With all matches enabled, it can add 2-3x the amount of time to deserialize an object.

## License

See LICENSE.txt