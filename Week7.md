```sql
-- 1. movies
SELECT title, rating FROM movies JOIN ratings ON movies.id = ratings.movie_id WHERE year = 2010 ORDER BY rating DESC, title ASC;

-- 2. fiftyville
SELECT people.id AS person_id, people.name, bank_accounts.account_number 
FROM people 
JOIN bank_accounts ON people.id = bank_accounts.person_id 
LIMIT 5;
