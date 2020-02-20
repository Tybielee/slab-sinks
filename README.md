# Project Status
This project is no longer in active development and is being archived. Please fork the repository if you need to make your own changes.

slab-sinks
==========
This project contains Semantic Logging Application Block (SLAB) sinks to persist application events published to ETW and consumed by SLAB.
Now contains the ability to write to a Shield Authenticated Elasticsearch (primarily used with Elastic Cloud) 
Also can write events to Logsene (another hosted Elasticsearch) 


__Sinks__
* Elasticsearch (Where else would you write events?)

## Elasticsearch Sink
A sink to write [Semantic Logging Application Block (SLAB)](http://slab.codeplex.com) events to [Elasticsearch](http://www.elasticsearch.org).

### 0 Create an event source
Create a class derived from [EventSource](http://msdn.microsoft.com/en-us/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx)

You could also use [EventSourceProxy](https://github.com/jonwagner/EventSourceProxy)

### 1 Install NuGet
```
Install-Package EnterpriseLibrary.SemanticLogging.Elasticsearch
```
### 2 Create a listener and enable events
```C#
var listener = new ObservableEventListener();

listener.EnableEvents(CommonEventSource.Log, EventLevel.LogAlways, ~EventKeywords.None);
```

### 3 Send events to Elasticsearch
```
listener.LogToElasticsearch(
    Environment.MachineName,
    "http://localhost:9200",
    "slab",
    "mylogs");
```

### 4 Send events to Logsene
```
listener.LogToElasticsearch(
    Environment.MachineName,
    "http://logsene-receiver.sematext.com:80",
    "LOGSENE_APP_TOKEN",
    "mylogs");
```

### 5 Using Shield Authentication
```
listener.LogToElasticsearch(
    Environment.MachineName,
    "http://YOUR_FOUND_LINK:9200",
    "index_name",
    "type_name",
    userName: "your userName",
    password: "your password");
```
The username and password are not hashed or encrypted so if that is a concern for your use-case please feel free to fork this repository and update it to suit your needs.

