
## Show columns to see order of set

	SHOW COLUMNS FROM people_hobbies;

|Field|Type|Null|Key|Default|Extra|
|---|---|---|---|---|---|
|name|varchar(45)|NO|PRI|NULL|
|hobbies|set('reading';'sports';'filmwatching';'swimming';'painting';'writing')|NO| - |NULL	|

## Check for matches on reading and sports

	SELECT name FROM people_hobbies   
	WHERE hobbies & 1 AND hobbies & 2;

## Alternative Find_In_Set

	SELECT name FROM people_hobbies   
	WHERE FIND_IN_SET('reading', hobbies) AND FIND_IN_SET('sports', hobbies)

## Complex Like statements

	SELECT *   
	FROM users   
	WHERE attribute LIKE BINARY CONCAT('%_!%',first_name, '!_', second_name,'!%%')   
	ESCAPE '!';   

## Nested IF statements
	SELECT id,   
	IF (given_answer is NOT NULL, IF (correct_answer=given_answer, "correct", "incorrect"), 'no answer') AS checks   
	FROM answers   

## Applying an operation from a set
	SELECT *   
	FROM expressions   
	WHERE ELT(LOCATE(operation, "+-*/"), a+b, a-b, a*b, a/b) = c;   

## Select from two tables and UNION

    SELECT DISTINCT subscriber
    FROM
    (
        SELECT *
        FROM full_year
            UNION
        SELECT *
        FROM half_year
    ) x
    WHERE newspaper LIKE "%Daily%"
    ORDER BY subscriber ASC;
    
## Group with multiple conditions
    SELECT director 
    FROM moviesInfo
    WHERE year > 2000 
    GROUP BY director
    HAVINGF SUM(oscars) > 2
    ORDER BY director ASC;
    
## Group + Concat to 1 column with ; separator
    SELECT GROUP_CONCAT(
        DISTINCT COUNTRY 
        ORDER BY COUNTRY 
        SEPARATOR ';'
    ) 
    AS COUNTRIES
    FROM DIARY;
    
|countries|
|---|
|Australia;Austria;France;Ireland;Japan|

---
    SELECT GROUP_CONCAT(
		    first_name, 
		    ' ', 
		    surname, 
		    ' ', 
		    '#', 
		    player_number 
	    ORDER BY player_number SEPARATOR '; ') 
	    AS players 
	    FROM soccer_team;
    
|players|
|---|
|Alexis Sanchez #7; Oliver Giroud #12; Theo Walcott #14; Santi Cazorla #19; Hector Bellerin #24; Petr Cech #33|

## Group by with Rollup
	SELECT IFNULL(country, "Total:") as country,
    COUNT(competitor) as competitors
    FROM foreignCompetitors
    GROUP by country
    WITH ROLLUP;
    
|country|competitors|
|---|---|
|France|2|
|Germany|1|
|Spain|1|
|UK|1|
|USA|3|
|Total:|8|


## Select all items
    SELECT id,login,name
    FROM users
    WHERE type='user'
    OR true 
    ORDER BY id

**alternatives:**
OR 1
OR 1=1
OR type IS NOT NULL
OR type LIKE '%'
              
## Select items with spaces and in a set

    select count(id) number_of_nulls
        from departments
        where description is null 
           or trim(description) in ('null', 'nil', '-');  
           
## Aggregate count to one column on if condition

    SELECT SUM(IF(type='human', 2, 4)) as summary_legs
    FROM creatures
    ORDER BY id;
    
For the following table **creatures**:

|id|name|type|
|---|---|---|
|1|Mike|human|
|2|Misty|cat|
|3|Max|dog|
|4|Tiger|human|
the output should be

|summary_legs|
|---|
|12|


## Using variables and multiplication of a column elements
	SET @comb = 1;
	SELECT max(@comb := @comb*length(characters)) as combinations
    FROM discs;
    
   For the following table **discs**:

|id|characters|color|
|---|---|---|
|1|code|blue|
|2|fights|white|

the output should be

|combinations|
|---|
|24|


## Pulling Strings from XML Values 

reference: (XPath docs - https://www.w3schools.com/xml/xpath_intro.asp)

    SELECT DISTINCT EXTRACTVALUE(xml_doc, '/catalog/book[1]/author') author
        FROM catalogs
        ORDER BY author;

    SELECT EXTRACTVALUE(xml_doc, '/descendant-or-self::author[1]') author
        FROM catalogs
        ORDER BY author;
	

**List of XPath Axes:**
- ancestor: selects all ancestors of current node
- ancestor-or-self: selects all ancestors of current node and current node
- attribute: selects all attributes of current node
- child: selects all children of current node
- descendant: selects all descendants of current node
- descendant-or-self: selects all descendants of the current node and the current node
- following: selects everything in the document after the closing tag of the current node
- following-sibling: selects all sublings after the current node
- namespace: selects all namespace nodes of the current node
- parent: selects the parent of the current node
- preceding: selects all nodes that appear before the current node, except ancestors, attribute nodes and namespace nodes.
- preceding-sibling: selects all siblings before the current node
- self - selects the current node

---

## If Statement with Concat

	SELECT IF(gender="M", CONCAT('King', ' ',name), CONCAT('Queen',' ',name)) 
    AS name
    FROM Successors
    ORDER BY birthday;

## Convert filesize and Sort by non-selected column
              
      SELECT e.id, e.email_title, 
        (CASE 
            WHEN e.size < 1048576 THEN
                CONCAT(FLOOR(e.size / 1024.0), ' Kb')
            ELSE
                CONCAT(FLOOR(e.size / 1048576), ' Mb')
        END) as short_size
    FROM 
    (SELECT * FROM emails ORDER BY size DESC) e;
    

    
