apiQL
=====

Simple Class for PHP MySQLi Connections with JSON Output Support.

Note: This class is still very much in development, use with caution.

## Getting Started

The first thing to do is to set globals for the connection:

```php
define("MYSQL_HOST","your_host");
define("MYSQL_USER","username");
define("MYSQL_PASS","password");
define("MYSQL_BASE","database");
```
    
Next, include/require the class file:

```php
require_once('apiQL.php');
```

## Usage


To use the class instatiate it, passing in either 'true' (JSON Output) or 'false' (Standard PHP access):

```php
$apiQL= new apiQL(true);
```
    
The class currently supports four methods; SELECT, INSERT, UPDATE, and DELETE:

###1.) SELECT

```php
$apiQL->table = "table_name";
$apiQL->columns = array("column1","column2");
$apiQL->order = "column1 DESC";
$apiQL->Select();
```
    
'columns' and 'order' are both optional and default to '*' and 'null' respectively.

If using the non-JSON mode an array is returned which can be acted on:

```php
...
$output = $apiQL->Select();

if(!$apiQL->test){
    // Loop through output
    foreach($output as $record){
        echo($record['column1'] . ' ' . $record['column2'] ... );
    }
}
```
    
When outputting JSON the following is returned:

```javascript
{
    "status": "success",
    "data": [
        {
            "column1": "some_value",
            "column2": "some_value",
            ...
        },
        {
            "column1": "some_value",
            "column2": "some_value",
            ...
        },
        ...
    ]
}
```
    
###2.) INSERT

```php
$apiQL->table = "table_name";
$apiQL->data = array("column1"=>"value1","column2"=>"value2", ... );
$apiQL->Insert();
```
    
Using the non-JSON mode the ID of the inserted element is returned:

```php
...
$id = $apiQL->Insert();
```
    
When outputting JSON the following is returned:

```javascript
{"status":"success","data":{"id":"some_value"}}
```
    
###3.) UPDATE

```php
$apiQL->table = "table_name";
$apiQL->data = array("column"=>"value", ... );
$apiQL->where = "column='condition'";
$apiQL->Update();
```
    
The 'where' is opional. The function returns 'success' on completion either in string format (non-JSON) or in JSEND format 

```javascript
{"status":"success","data":null}
```

###4.) DELETE

```php
$apiQL->table = "table_name";
$apiQL->where = "column='condition';
$apiQL->Delete();
```
    
The 'where' is optional. The function returns 'success' on completion either in string format (non-JSON) or in JSEND format 

```javascript
{"status":"success","data":null}
```

## Close Connection

To close the connection simply apply the following command:

```php
$apiQL->Close();
```