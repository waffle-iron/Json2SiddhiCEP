[![Stories in Ready](https://badge.waffle.io/Bera/Json2SiddhiCEP.png?label=ready&title=Ready)](https://waffle.io/Bera/Json2SiddhiCEP)
# Json2Siddhi Query generator from JSON

[![Build Status](https://travis-ci.org/Bera/Json2SiddhiCEP.svg?branch=master)](https://travis-ci.org/Bera/Json2SiddhiCEP)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/e7da0eab5128486ebca9996c3b3a0449)](https://www.codacy.com/app/brunormoura/Json2SiddhiCEP)
[![Coverage Status](https://coveralls.io/repos/github/Bera/Json2SiddhiCEP/badge.svg?branch=master)](https://coveralls.io/github/Bera/Json2SiddhiCEP?branch=master)
[![Dependency Status](https://www.versioneye.com/user/projects/576bcb64cd6d51003e9206e9/badge.svg?style=flat-square)](https://www.versioneye.com/user/projects/576bcb64cd6d51003e9206e9)


> Transform a JSON in a SiddhiQL valid sentence.


## What this project aims to solve or improve 

This project is an attemp to deal with the difficult of business guys to elaborate queries and filters for use with events an them produce de desirable alerts in WSO2 CEP Complex Event Processor, at Produban Brazil.

As [Wikipedia](https://en.wikipedia.org/wiki/Complex_event_processing) states, Complex event processing, or CEP, is event processing that combines data from multiple sources to infer events or patterns that suggest more complicated
circumstances. CEP can executes a set of rules which, as said, can infer events, patterns and sequences.

The idea is to provide for the users a grafical user interface made with love in Angular that allow users to compose rules, filter, windows and combine with Threshold  and any kind of value to compose sofisticated queries for generate alerts in CEP execution plans  WITHOUT dive into Siddhi Query Language, a SQL-like language that lets you work with data stream, se language syntax or details. Remember, the target are the business guys and not the tech geeks only.

The rules are written on JSON and accessed and modified via the REST API by this application. Them the valid query is deployed in the CEP execution plan to be available to fire alerts accordingly.  

Some features available

* Aggregate functions like averages, sums, max, min, stddev and counts.
* Filters and Query Projection using mathematical and logical expressions.
* Default value to an attribute.

Some features available

* Implement window for imput streams.
* Implement partitions .

In fact, a fancy query bellow:.
```sql
from InputStreamName [ metric == “system.dsk.utilization” and value >= 80 and tsName == “I_BIG_DATA_MONITORING” and (fileSystem == “/pdr/bdm” or
                                         fileSystem == “/pdrbdm/tool/level”)]
select
        “BIG_DATA_MONITORING”, metric, “’ do FileSystem: ‘”, fileSystem, “’ above threshold: 80%”, “. Value: “, value, “%.” ) as message,
        “open” as eventstatus,
        “critical” as severity,
        80.0 as threshold,
        csId as id,
        fileSystem as item,
        value as value,
        hostname as hostname,
        businessService as businessService,
        technicalService as technicalService,
        serviceComponent as serviceComponent,
        environment as environment,
        lsFunction as lsFunction,
        hyperName as hyperName,
        csSite as csSite,
        platform as platform,
        rule as rule,
        status as status,
        timestamp as timestamp,
        tool as tool

insert into InputStreamName;
```
 Is generated by the followed JSON data:

```json
{
  "ruleid": "xb1825091352016111717889",
  "created_by_user": "b18er45",
  "edited_by_user": "b18er45: (13/5/2016)-(11:17:17)",
  "tool": "openbus_br_zabbix_v2",
  "rule_filters": [
    {
      "field": "platform",
      "operator": "==",
      "value": "Wintel",
      "condition": "AND"
    },
    {
      "field": "metric",
      "operator": "==",
      "value": "system.dsk.utilization",
      "condition": "AND"
    },
    {
      "field": "hostname",
      "operator": "==",
      "value": "SBRSP3",
      "condition": "AND"
    },
    {
      "field": "fileSystem",
      "operator": "==",
      "value": "E:",
      "condition": "AND"
    },
    {
      "field": "value",
      "operator": ">=",
      "value": "95",
      "condition": "AND"
    },
    {
      "field": "value",
      "operator": "<",
      "value": "99",
      "condition": "END"
    }
  ]
}
```


##  Requirements for setup and to run

If you don't have the runtime at least for Oracle Java 8, you'll need to install it.

Will be necessary to be maven 3 installed and configured too in your system to allow build this project.
 
Only this will be necessary.

## Installation

Windows, OS X & Linux:

Grab the jar in some place that you want or build your self, first clone this repo. 

```sh
git clone git@github.com:Bera/Json2SiddhiCEP.git
```
After access de directory Json2SiddhiCEP and perform the maven goals bellow

```sh
mvn clean package
```
That is, easy isn't it?

## Config

You will need a config file to specify the behavior and the attributes that are part of the stream with its type, and a few other options like the REST URI that will be used to serve the REST API.

## Usage 

TODO - Spice this up with code blocks and potentially more screenshots.

```sh
java -jar target/app.jar -conf src/main/conf/app-conf.json
```
## API

The REST API lets you add, remove, list and synchronize queries on the fly.

Endpoints

The following endpoints should be available demonstrating different features, look at the  Dashboard at http://localhost:8080/.  Base endpoint and UI Admin.

-     GET /api/rules => get all rules (getAll)
-     GET /api/rules/:id => get the rule with the corresponding id (getOne)
-     POST /api/rule => add a new rule (addOne)
-     PUT /api/rule/:id => update a rule (updateOne)
-     DELETE /api/rule/id => delete a rule (deleteOne)

## Release History

* 0.0.1
    * Work in progress

## Roadmap

1. Add hystrix or failsafe circuit braker
2. Use CEP REST API
3. Implement Windows and Partitions SiddhiQL features

## Contributing

1. [Fork it](https://github.com/Bera/Json2SiddhiCEP)
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Create a new Pull Request

## License

Distributed under the MIT license. MIT License

Copyright (c) [2016] [Produban]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

Bruno Moura – [@_Bera_](https://twitter.com/_Bera_) – brunormoura@gmail.com






