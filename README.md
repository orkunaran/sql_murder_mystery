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

![image](https://github.com/orkunaran/sql_murder_mystery/blob/main/pics/1.png)

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

![image](https://github.com/orkunaran/sql_murder_mystery/blob/main/pics/2.png)

Morty Schapiro and Annabel Miller



3. Read Interviews with the witnesses:
```sql
SELECT * FROM interview
	WHERE person_id IN (14887,16371)
```
A gold member of Gym with number  started with "48Z". Also he/she got 'H42W' somewhere in his/her car plate. We also know that the murderer was at the gym at $9^th$


![image](https://github.com/orkunaran/sql_murder_mystery/blob/main/pics/3.png)


2 and 3. In one Querry:

OK it's not the best looking querry but I'd like to give it a shot 

```sql
SELECT *, MAX(address_number)
  FROM person JOIN interview ON person.id = interview.person_id
  	WHERE address_street_name = 'Northwestern Dr' 
	UNION 
	  SELECT *, MAX(address_number) FROM person 
	  JOIN interview ON person.id = interview.person_id
	     WHERE (name LIKE 'Annabel%' AND address_street_name = 'Franklin Ave')

```
![image](https://github.com/orkunaran/sql_murder_mystery/blob/main/pics/2-3 together.png)



4. Let's find the murderer suspect
```sql
SELECT * FROM get_fit_now_check_in x
	JOIN get_fit_now_member y
	ON x.membership_id= y.id 
	JOIN person z ON z.id = y.person_id 
	JOIN drivers_license dl ON dl.id = z.license_id
		WHERE membership_id LIKE '48Z%' 
			AND check_in_date = 20180109 
				AND plate_number LIKE '%H42W%'
```


![image](https://github.com/orkunaran/sql_murder_mystery/blob/main/pics/4.png)


	Congrats, you found the murderer! 
	
	
	
More Challenges: Let's find the victim...coming soon...
