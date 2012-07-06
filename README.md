apiQL
=====

Simple Class for PHP MySQLi Connections with JSON Output Support.

Note: This class is still very much in development, use with caution.

## Getting Started

The first thing to do is to set globals for the connection:

    define("MYSQL_HOST","your_host");
    define("MYSQL_USER","username");
    define("MYSQL_PASS","password");
    define("MYSQL_BASE","database");
    
Next, include/require the class file:

    require_once('apiQL.php');
    
## Usage

To use the class instatiate it, passing in either 'true' (JSON Output) or 'false' (Standard PHP access):

    $apiQL= new apiQL(true);
    
The class currently supports four methods; SELECT, INSERT, UPDATE, and DELETE:

###1.) SELECT

    $apiQL->table = "table_name";
    $apiQL->columns = array("column1","column2");
    $apiQL->order = "column1 DESC";
    $apiQL->Select();
    
'columns' and 'order' are both optional and default to '*' and 'null' respectively.

If using the 'standard' non-JSON mode an array is returned which can be acted on:

    ...
    $output = $apiQL->Select();
    
    if(!$apiQL->test){
        // Loop through output
        foreach($output as $record){
            echo($record['column1'] . ' ' . $record['column2'] ... );
        }
    }
    
###2.) INSERT

    $apiQL->table = "table_name";
    $apiQL->data = array("column1"=>"value1","column2"=>"value2", ... );
    $apiQL->Insert();
    
Using the 'standard' non-JSON mode the ID of the inserted element is returned:

    ...
    $id = $apiQL->Insert();
    
###3.) UPDATE

    $apiQL->table = "table_name";
    $apiQL->data = array("column"=>"value", ... );
    $apiQL->where = "column='condition'";
    $apiQL->Update();
    
The 'where' is opional. The function returns 'success' on completion.

###4.) DELETE

    $apiQL->table = "table_name";
    $apiQL->where = "column='condition';
    $apiQL->Delete();
    
The 'where' is optional. The function returns 'success' on completion.

## Close Connection

To close the connection simply apply the following command:

    $apiQL->Close();