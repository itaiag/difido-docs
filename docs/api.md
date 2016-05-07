# Difido Server API Documentation

Root URL: http://{server}:{port}/api/

## Execution Resource

### Add execution
Adding new execution in the server or joining to an existing shared execution

**Request**

URI: executions/

Method: POST

Content Type: application/json

Body:
~~~~json
{
   "description":"<Execution description>",
   "executionProperties":{
      "key0":"val0",
      "key1":"val2"
   },
   "shared":false,
   "forceNew":false
}
~~~~
**Response**

The call will return the execution id
Body:

```
5
```

### End Execution
Setting execution to not active. This will not allow any reports to be added to the executions. This is an irreversible process that 

URI: executions/{execution}?active=false

Method: PUT

Content Type: text/plain

## Machine Resource
After having the execution id, user should add his own machine to the execution.

### Add Machine

**Request**

URI: executions/{execution}/machines

Method: POST

Content Type: application/json

Body:
~~~~json
{
   "type":"machine",
   "name":"<Machine name>",
   "status":"success",
   "children":null
}
~~~~
**Response**

The call will return index of the added machine in the execution
Body:

```
5
```

### Update Machine

The update machine is actually used to update all the scenarios and tests that were executed until this point. The json can be pretty complex since it holds all the scenario tree.

**Request**

URI: executions/{execution}/machines/{machine}

Method: PUT

Content Type: application/json

Body:
~~~~json
{
   "type":"machine",
   "name":"agmon-PC",
   "status":"error",
   "children":[
      {
         "type":"scenario",
         "name":"regression",
         "status":"error",
         "children":[
            {
               "type":"scenario",
               "name":"sub02",
               "status":"error",
               "children":[
                  {
                     "type":"test",
                     "name":"reporterWithCustomHtml",
                     "status":"success",
                     "index":0,
                     "uid":"431438075599-1",
                     "duration":5207,
                     "timestamp":"12:27:03:"
                  },
                  {
                     "type":"test",
                     "name":"reporterWithLinkToTest",
                     "status":"error",
                     "index":1,
                     "uid":"431438075599-2",
                     "duration":1137108,
                     "timestamp":"12:27:08:"
                  },
                  {
                     "type":"test",
                     "name":"reporterWithLeveling",
                     "status":"success",
                     "index":2,
                     "uid":"431438075599-3",
                     "duration":0,
                     "timestamp":"12:47:09:"
                  }
               ],
               "scenarioProperties":null
            }
         ],
         "scenarioProperties":{
            "station":"10.100.102.7",
            "sutFile":"mystation.xml",
            "version":"unknown",
            "user":"agmon",
            "testDir":"projects/jsystemServices/target/classes"
         }
      }
   ]
}
~~~~

## Test Details Resource

### Add Test Details

This service is used to add and update a single test details. That means, attributes like the test name, description and uid, the test properties and parameters and the report elements that describes the steps that were performed during the test.

URI: /executions/{execution}/details

Method: POST

Content type: application/json

Body:
~~~~json
{
   "name":"reporterWithLinkToTest",
   "uid":"431438075599-2",
   "description":"This test demonstrates how to use the package list feature which was",
   "timestamp":"2015/07/28 at 12:27:08",
   "duration":0,
   "parameters":null,
   "properties":{
      "Test Documentation":"This test demonstrates how to use the package list feature which was",
      "Class":"com.aqua.services.reporter.ReporterTest",
      "Breadcrumb":"regression-->sub02-->ReporterTest.reporterWithLinkToTest",
      "Class Documentation":"Demonstrates reporter capabilities. Issues that are covered:"
   },
   "reportElements":[      
      {
         "title":"Start time: Tue Jul 28 12:45:54 IDT 2015",
         "message":null,
         "status":"success",
         "type":"regular",
         "time":"12:46:04:"
      },
      {
         "title":"End time  : Tue Jul 28 12:46:04 IDT 2015",
         "message":null,
         "status":"success",
         "type":"regular",
         "time":"12:46:04:"
      },
      {
         "title":"Test running time: 9 sec.",
         "message":null,
         "status":"success",
         "type":"regular",
         "time":"12:46:05:"
      }
   ]
   
}
~~~~

### Add File to Test
This service is used to add attachments to tests. The attachments can be images, text or binary files. 

URI: /executions/{execution}/details/{uid}/file

Method: POST

Body: A multipart body with a 'bin' part that stores the binary file