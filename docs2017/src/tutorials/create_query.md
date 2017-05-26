---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creating a Cloudant Query

This tutorial demonstrates how to create a design document and an index, and how to use Cloudant Query to extract specific data 
from the database.

To begin, you create the `rolodex` database and some JSON documents that contain the data for these exercises. Next, you create 
a design document that  
contains information about how to build your indexes. You create two different types of indexes to demonstrate how an index  
can make it easier and faster to find data. Finally, you create and run queries against the database. 

While this tutorial focuses on creating a query with Cloudant Dashboard, you can use either Cloudant 
Dashboard or the command line. Follow the links that are provided throughout this tutorial for information about using the command line. 

You complete the following tasks during this tutorial:

1.  [Creating a database](create_query.html#creating-a-database-using-the-cloudant-dashboard)
2.  [Creating a design document](create_query.html#creating-a-design-document)
3.  [Creating an index](create_query.html#creating-an-index)
4.  [Creating a query](create_query.html#creating-a-query)


## Creating a database

Now, you create the `rolodex` [database](../api/database.html#create) and JSON documents that are used throughout this tutorial.  

1.  If you do not already have one, create an IBM Bluemix Cloudant account [here](https://console.ng.bluemix.net/registration/?target=%2Fcatalog%2Fservices%2Fcloudant-nosql-db%2F) and log in to it.
2.  Log in to the Cloudant Dashboard.
3.  Select the Databases tab. 
4.  Click ![Create Database icon](../images/create_database_icon.png). 
5.  Type `rolodex` and click **Create**.<br>
    The `rolodex` database automatically opens.<br>
    <br>
    From the command line: 
    ```
    acurl https://<username>.bluemix.cloudant.com/rolodex -X PUT
    ```
    Results:
    ```
    {"ok":true}
    ```
6.  From the **All Documents** tab, click ![Create icon](../images/create_icon.png) and select **New Doc**.<br>
    The New Document window opens. <br>
    ![New Document window](../images/add_document_window.png)
7.  To create a JSON document, copy and paste the sample text after the `_id` and inside the bracket.<br>
*First sample document:*
```json
,
"firstname": "Sally",
"lastname": "Brown",
"age": 16,
"city": "New York City",
"state": "New York"                
```
8.  Repeat step 7 and add the remaining documents to the database.<br>
_Second sample document:_
```json
,
"firstname": "John",
"lastname": "Brown",
"age": 21,
"city": "New York City",
"state": "New York"    
```
{:codeblock}

<blockquote>*Third sample document:*<br>
<code>,<br>
"firstname": "Greg",<br>
"lastname": "Greene",<br>
"age": 35,<br>
"city": "San Diego",<br>
"state": "California"<br>
</code>    
</blockquote>

<blockquote>*Fourth sample document:*<br>
<code>,<br>
"firstname": "Amanda",<br>
"lastname": "Greene",<br>
"age": 44,<br>
"city": "Syracuse",<br>
"state": "New York"<br>
</code>    
</blockquote>

<blockquote>*Fifth sample document:*<br>
<code>,<br>
"firstname": "Lois",<br>
"lastname": "Brown",<br>
"age": 33,<br>
"city": "Baton Rouge",<br>
"state": "Louisiana"<br>
</code>    
</blockquote>

From the command line:

1.  Copy and paste the sample document information in the previous step to a data file called `documents.dat`. 
2.  Run the following `curl` command.  
```
curl https://<username>.bluemix.cloudant.com/rolodex -X POST -H "Content-Type: application/json" -d \@documents.dat
```
Notice that the '@' symbol, used to indicate that the data is included in a file, is identified by the supplied name.

The `rolodex` database was created and populated with five JSON documents. 


## Creating a design document

[Design documents](../api/design_documents.html#design-documents) contain instructions about how views 
and indexes must be built. When you change a design document, the index is overwritten and 
re-created from scratch. 

Indexes and views have the same purpose--to improve processing and return time for database queries. However, the mechanics are different. 

A view selectively filters documents. You define 
a view in the `view` field inside a design 
document. In Cloudant, views are written by using JavaScript functions. When you run a query with 
your view, Cloudant applies the JavaScript function to 
all the documents in the database. 

Cloudant search indexes are also defined in design documents. Each index is defined by an index function that determines 
what data to index and then store in the index. These indexes use [Lucene Query 
Parser Syntax](http://lucene.apache.org/core/4_3_0/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Overview) 
to query databases.  

To create a design document: 

1.  From the **Design Documents** tab, click ![Create icon](../images/create_icon.png) > **New Doc**.
2.  Replace the `_id` value with `rolodex-index-design-doc` as seen in the example.
```json
{
  "_id": "rolodex-index-design-doc"
}
```
3.  Click **Create Document**. <br>
    The `rolodex-index-design-doc` design document is created. 

## Creating an index 

In Cloudant, you build [indexes](../api/using_views.html#indexes) by using 
[view (MapReduce)](../api/creating_views.html#views-mapreduce-) and [search indexes](../api/search.html#search). 

### Creating a "type=json" index

Creating a ["type=json"](../api/cloudant_query.html#creating-a-type-json-index) index reduces the load on 
your environment and the size of your data set. 

To create a "type=json" index: 

1.  Select **Design Documents** tab.
2.  Click ![Create icon](../images/create_icon.png) > **New Search Index**. 
3.  Select **New document** from the Save to design document drop-down menu. 
4.  Type `rolodex-index-design-doc` in the `_design` field. 
5.  Type `JSONsearch-index` in the Index name field.
6.  Replace the text in the Search index function field with the text in the sample.
```json
    function (doc) [
    {
        "index": {
            "fields": [
                {
                   "firstname" : "string",
                   "lastname" : "string",
                   "city" : "string"                   
                    }
                ]                    
            },
        }
    ]   
```
{:codeblock}
7.  Accept the remaining default options.
8.  Click **Create Document and Build Index**.
The `JSONsearch-index` was created. See the index by expanding `rolodex=index-design-doc` > **Search Indexes**.

### Creating a "type=text" index

When you create a ["type=text"](../api/cloudant_query.html#creating-a-type-text-index) index, all the documents and fields in your database
are automatically indexed. As such, you can 
search and retrieve information from any field.  

To create the index:

1.  Select **Design Documents** tab.
2.  Click ![Create icon](../images/create_icon.png) > **New Search Index**. 
3.  Select **New document** from the Save to design document drop-down menu. 
4.  Type `rolodex-index-design-doc` in the `_design` field. 
5.  Type `TEXTsearch-index` in the Index name field. 
6.  Replace the text in the Search index function field with the text below.
```json
  function (doc) [
    {
        "index": {
        "fields": [
            {
               "name": "firstname",
               "type": "string"
                },
            {
                "name": "lastname",
                "type": "string"
                },
            {
                "name": "age",
                "type": "number"
                }         
                    ]
            },
        }
    ]
```
7.  Accept the remaining options.
8.  Click **Create Document and Build Index**.
The `TEXTsearch-index` was created. See the index by expanding `rolodex=index-design-doc` > **Search Indexes**.

### Listing Cloudant Query indexes 

You can see all the indexes in the `rolodex` database from the Cloudant Dashboard or 
[list](../api/cloudant_query.html#list-all-cloudant-query-indexes) them from the command line. 

1.  Expand `rolodex-index-design-doc` under Design Documents tab. 
2.  Expand **Search Indexes**.<br>
    The two indexes you created appear. You can edit, clone, or delete indexes here. When you select an index, you can use it to query the database. 

## Creating a query 

When you create your [query](../api/cloudant_query.html#query) statement, you can narrow the data that you search with [selector syntax](../api/cloudant_query.html#selector-syntax) and 
[implicit](../api/cloudant_query.html#implicit-operators) or [explicit](../api/cloudant_query.html#explicit-operators) operators.


### Querying the database with `selector` syntax

In a [selector expression](../api/cloudant_query.html#creating-selector-expressions), you specify at least one field and 
its corresponding value. When the query runs, it uses these values to search the database for matches. The 
selector is a JSON object. For this exercise, you use the selector expression that is described here. 

Specify the documents that you want to find in the database in the `selector` parameter. For example, everyone who lives in New York City, New York. 

```json
{
  "selector": {
        "city" : "New York City",  
        "state": "New York"
    }
```    
{:codeblock}

Specify how you want the information that is returned in the `fields` parameter. In this case, the first and last 
name of everyone in who meets the search criteria. The results are sorted by first name in ascending order based on the `sort` parameters values. 

```json
{
"fields": ["firstname","lastname"  
    ],
  "sort": [
    {
      "firstname": "asc"
    }  
```  
{:codeblock}

To run the query:

1.  Click the `JSONsearch-index` index that you created earlier by expanding `rolodex-index-design-doc` > **Search Indexes** > **JSONsearch-index**.
2.  Copy and paste the following selector statement to the Query field and click **Query**.  
```json
{
  "selector": {
        "city" : "New York City",    
        "state": "New York"      
       },     
   "fields": ["firstname","lastname"
      ],
   "sort": [
    {
      "firstname": "asc"
       }
     ]
}
```
{:codeblock}

_Example results returned from search:_
```json
{
  "docs": [
    {     
        "firstname": "John", 
        "lastname": "Brown",
        "city" : "New York City"        
        }
    {     
        "firstname": "Sally", 
        "lastname": "Brown",
        "city" : "New York City"        
        }        
   ]
}
```
{:codeblock}

### Querying the database with operators

Using operators in your query provides a more granular search. Operators are described 
[here](../api/cloudant_query.html#query-parameters). In this example, the operators `$and`, `$text`, 
and `$gt` define the search parameters. These operators perform the following functions:

    *   $and    Finds a match when all the selectors in the array match. 
    *   $text   Matches any word or string in the document. It is not case-sensitive. The $text operator is only available with the index "type=text". However, searching for field names is an invalid use of the $text operator. 
    *   $gt     Finds matches greater than the specified value.  

This example searches the database for people with the last name Brown and an age greater than 20.

```json
{
    "selector": {
        "$and": [
              {
                "$text": "Brown"
               },
            {
                "$gt": 20
            }
       ]
  },
```   
{:codeblock}

Based on the values in the `field` parameter, the results include the first name, last name, and age sorted by first name in ascending order. 

```json
 },
        "fields": [
            "firstname", "lastname", "age"],
  "sort": [
       {
          "firstname": "asc"
        }
     ]            
 } 
``` 
{:codeblock}

To run the query:

1.  Click the `TEXTsearch-index` index that you created earlier by expanding `rolodex-index-design-doc` > **Search Indexes** > **TEXTsearch-index**.
2.  Copy and paste the example selector statement into the Query field and click **Query**.  
```json
{
    "selector": {
        "$and": [
             {
                "$text": "Brown"
             },
            {
                "$gt": 20
            }
        ]
   },
        "fields": [
            "firstname", "lastname", "age"],
  "sort": [
      {
      "firstname": "asc"
      }
    ]            
 } 
``` 
{:codeblock}

_Example results returned from search:_

```json
{
  "docs": [
 {     
    "firstname": "John",
    "lastname": "Brown",
    "age": "21"
       },
 {     
    "firstname": "Lois",
    "lastname": "Brown",
    "age": "33"
       }       
  ]
}
```
{:codeblock}

