# SQL Murder Mystery

![image](http://mystery.knightlab.com/174092-clue-illustration.png)

There's been a Murder in SQL City! The SQL Murder Mystery is designed to be both a self-directed lesson to learn SQL concepts and commands and a fun game for experienced SQL users to solve an intriguing crime.

A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.

## Tables 

![image](http://mystery.knightlab.com/schema.png)

## Solution 

1. We know that the crime is Murder and the date is 15.01.2018 and happened in SQL City. First, let's get crime scene report with that particular specs:
        
```sql
 SELECT * FROM crime_scene_report
    WHERE type = 'murder' 
      AND date = 20180115 
        AND city = 'SQL City''
```

Which Returns: 

The first witness lives at the last house on "Northwestern Dr". 

The second witness, named Annabel, lives somewhere on "Franklin Ave".


2. Time to find the witnesses.

```sql
SELECT *, MAX(address_number)
  FROM person 
  	WHERE address_street_name = 'Northwestern Dr'
	UNION 
	  SELECT *, MAX(address_number) FROM person 
	     WHERE (name LIKE 'Annabel%' AND address_street_name = 'Franklin Ave')
 
```

Which returns :


Morty Schapiro and Annabel Miller



3. Read Interviews with the witnesses:
```sql
SELECT * FROM interview
	WHERE person_id IN (14887,16371)
```
