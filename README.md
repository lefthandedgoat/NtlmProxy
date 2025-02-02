# NTLM Proxy

So my team is using [Selenium](http://docs.seleniumhq.org/) [WebDriver](http://docs.seleniumhq.org/projects/webdriver/) to test our web application, and it takes balls forever to run on our test browser. Our test browser is [Firefox](http://www.mozilla.org/en-US/firefox/fx/), which, with a name like that, you'd think would be... I dunno, zippy.

Anyway.

I wanted to use [PhantomJS](http://phantomjs.org/) to run headlessly, which would increase the speed of the test runs. Sounds good, right? Too bad we're using Windows Authentication. PhantomJS (currently, 20140205) doesn't like NTLM, and neither do I. The only way to pass Windows credentials is to use some sort of proxy.

## Some sort of proxy

That's why I wrote this little library.

With a simple `using` directive it will create a tiny web proxy and niavely forward any requests sent to it on to a target URL, with NTLM headers for the current user.

It's pretty simple to use:

```csharp
    using (var proxy = new NtlmProxy(new Uri("http://localhost:8081/"), 3999))
    {
		// Make your requests here to http://localhost:3999/whatever
    }
```

You can also leave off the port number to have a port auto-assigned:


```csharp
    using (var proxy = new NtlmProxy(new Uri("http://localhost:8081/")))
    {
		// Make your requests here to http://localhost:3999/{0}, proxy.Port
    }
```

## How do I install it?

You can download the zipped DLL in the Releases section above, or you can use NuGet:

```xml
  <package id="MikeRogers.NtlmProxy" version="1.0.0" targetFramework="net45" />
```

## Why do you keep saying 'naively'?

I'm no NTLM expert, but I think after the first authorization challenge the client should be holding onto the credentials and including the appropriate NTLM headers. I'm pretty sure this proxy server won't do that.

## It's still pretty cool

I know, right?

## License?

As always, we rock the BSD.
