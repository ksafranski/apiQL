apiQL
=====

Simple Class for PHP MySQLi Connections with JSON Output Support.

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
    

    
    
