This library is licensed under the Apache License Version 2.0.
Please see the file [NOTICE.txt](NOTICE.txt).  

Arthur van Hoff
avh@strangeberry.com

Rick Blair
rickblair@mac.com

Kai Kreuzer
kai@openhab.org

# JmDNS

This is an implemenation of multi-cast DNS in Java. It
supports service discovery and service registration. It is fully
interoperable with Apple's Bonjour. 

## Running jmdns from the Command Line

GUI browser:
```
  java -jar lib/jmdns.jar -browse
```

TTY browser for a particular service type:
```
  java -jar lib/jmdns.jar -bs _http._tcp local.
```

Register a service:
```
  java -jar lib/jmdns.jar -rs foobar _http._tcp local. 1234 path=index.html
```

List service types:
```
  java -jar lib/jmdns.jar -bt
```
  
To print debugging output specify -d as the first argument.  


## Sample Code for Service Registration

```
    import javax.jmdns.*;

    JmDNS jmdns = new JmDNS();
    jmdns.registerService(
    	new ServiceInfo("_http._tcp.local.", "foo._http._tcp.local.", 1234, 0, 0, "path=index.html")
    );
```


## Sample code for Serivice Discovery

```
    import javax.jmdns.*;

    static class SampleListener implements ServiceListener {
    	public void addService(JmDNS jmdns, String type, String name)
    	{
    	    System.out.println("ADD: " + jmdns.getServiceInfo(type, name));
    	}
    	public void removeService(JmDNS jmdns, String type, String name)
    	{
    	    System.out.println("REMOVE: " + name);
    	}
    	public void resolveService(JmDNS jmdns, String type, String name, ServiceInfo info)
    	{
    	    System.out.println("RESOLVED: " + info);
    	}
    }

    JmDNS jmdns = new JmDNS();
    jmdns.addServiceListener("_http._tcp.local.", new SampleListener());
```
