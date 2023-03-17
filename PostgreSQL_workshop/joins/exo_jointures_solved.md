# 1. Nouvelles Tables

1.1. Récupérer toutes les données de la table dept_manager_dup, triés par dept_no 
```sql
SELECT * FROM dept_manager_dup
ORDER BY dept_no;
```

1.2. Récupérer toutes les données de la table departments_dup, triés par dept_no 
```sql
SELECT * FROM departments_dup
ORDER BY dept_no;
```

# 2. INNER JOIN
![SQL-INNER-JOIN](https://user-images.githubusercontent.com/73080397/225478783-7228597a-9685-4d16-aba1-adfd9974635c.png)

2.1. Extraire le numéro d'employé, le numéro de département et le nom du département de tous les managers. Classer par numéro de département du manager
```sql
SELECT m.emp_no, m.dept_no, d.dept_name
FROM dept_manager_dup m
INNER JOIN departments_dup d
ON m.dept_no = d.dept_no
ORDER BY m.dept_no;
```

Ecrire la même requête en ajoutant la date de début et la date de fin de contrat (Indice: vous allez utiliser les mêmes tables)
```sql
SELECT m.emp_no, m.dept_no, d.dept_name, m.from_date, m.to_date
FROM dept_manager_dup m
INNER JOIN departments_dup d
ON m.dept_no = d.dept_no
ORDER BY m.dept_no;
```


2.2. Extraire une liste contenant des informations sur le numéro d'employé, le prénom ,le nom de famille, le numéro de service et la date d'embauche de tous les managers. (Indice : utilisez les tables employees et dept_manager)
```sql
SELECT e.emp_no, e.first_name, e.last_name, e.hire_date, dm.dept_no
FROM employees e
INNER JOIN dept_manager dm
ON e.emp_no = dm.emp_no;
```

# 3. Enregistrements dupliqués

3.1. Ajouter des enregistrements dupliqués dans les tables dept_manager_dup et departments_dup
```sql
INSERT INTO dept_manager_dup 
VALUES 	('110228', 'd003', '1992-03-21', '9999-01-01');
        
INSERT INTO departments_dup 
VALUES	('d009', 'Customer Service');
```
3.2. Sélectionner tous les enregistrements de la table dept_manager_dup
```sql
SELECT * FROM dept_manager_dup;
```
3.3. Sélectionner tous les enregistrements de la table departments_dup
```sql
SELECT * FROM departments_dup;
```

3.4. Effectuer le INNER JOIN comme précédemment 
```sql
SELECT m.emp_no, m.dept_no, d.dept_name
FROM dept_manager_dup m
INNER JOIN departments_dup d
ON m.dept_no = d.dept_no
ORDER BY m.dept_no;
```

3.5. Ajoutez une clause GROUP BY. Veillez à inclure tous les champs dans la clause GROUP BY.
```sql
SELECT m.emp_no, m.dept_no,
FROM dept_manager_dup m
INNER JOIN departments_dup d
ON m.dept_no = d.dept_no
GROUP BY m.emp_no, m.dept_no, d.dept_name
ORDER BY m.dept_no;
```

# 4. LEFT JOIN 

<img width="544" alt="pasted image 0" src="https://user-images.githubusercontent.com/73080397/225485290-9b839101-2587-4f99-a704-8232995b2db7.png">

4.1. Supprimer les doublons des deux tables
```sql
DELETE FROM dept_manager_dup 
WHERE emp_no = '110228';
        
DELETE FROM departments_dup 
WHERE dept_no = 'd009';
```

4.2. Ajouter les enregistrements initiaux
```sql
INSERT INTO dept_manager_dup 
VALUES 	('110228', 'd003', '1992-03-21', '9999-01-01');
        
INSERT INTO departments_dup 
VALUES	('d009', 'Customer Service');
```

4.3. Sélectionner tous les enregistrements de dept_manager_dup
```sql
SELECT * from dept_manager_dup;
```

4.4. Sélectionner tous les enregistrements de departments_dup
```sql
SELECT * from departments_dup;
```

Rappelez-vous, lorsque nous avions INNER JOIN:

```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM dept_manager_dup m
JOIN departments_dup d 
ON m.dept_no = d.dept_no
ORDER BY m.dept_no;
```

4.5. Joindre les tables dept_manager_dup et departments_dup
Extraire un sous-ensemble de tous les numéros d'employé, numéros de département et noms de département de tous les managers. Ordonner par le numéro de département des responsables  
```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM dept_manager_dup m
LEFT JOIN departments_dup d
ON m.dept_no = d.dept_no
ORDER BY m.dept_no;
```

4.6. Que se passera-t-il si nous mettons d LEFT JOIN m ?
```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM departments_dup d
LEFT JOIN dept_manager_dup m
ON d.dept_no = m.dept_no
ORDER BY m.dept_no;
```
Obseravation de la différence en nombre de lignes rendues

# 5. RIGHT JOIN
Nous avons vu LEFT JOIN dans l'exercice précédent:

```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM dept_manager_dup m
LEFT JOIN departments_dup d 
ON m.dept_no = d.dept_no
ORDER BY dept_no;
```

5.1. Utiliser RIGHT JOIN 
```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM dept_manager_dup m
RIGHT OUTER JOIN departments_dup d
ON m.dept_no = d.dept_no
ORDER BY dept_no;
```

5.2. SELECT d.dept_no
```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM dept_manager_dup m
RIGHT OUTER JOIN departments_dup d
ON m.dept_no = d.dept_no
ORDER BY d.dept_no;
```

5.3. Faire d LEFT JOIN m
```sql
SELECT m.dept_no, m.emp_no, d.dept_name
FROM departments_dup d
LEFT JOIN dept_manager_dup m
ON m.dept_no = d.dept_no
ORDER BY dept_no;
```


# 6.Utiliser WHERE et JOIN 

6.1. Extraire le numéro d'employé, le prénom, le nom et le salaire de tous les employés qui gagnent plus de 145000 dollars par an
```
SELECT e.emp_no, e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s
ON e.emp_no = s.emp_no
WHERE salary > 145000;
```

6.2. Quel est le résultat de cette requête ?
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s 
ON e.emp_no = s.emp_no
WHERE s.salary > 145000;
```
6.3. Sélectionner le nom, le prénom, la date d'embauche et le salaire de tous les employés dont le prénom est 'Mario' et le nom 'Straney'
```sql
SELECT e.first_name, e.last_name, e.hire date, s.salary
FROM employees e
JOIN salaries s
ON e.emp_no = s.emp_no
WHERE first_name = 'Mario' AND last_name = 'Straney'
ORDER BY e.emp_no;
```

6.4. Joignez les tables "employees" et "dept_manager" pour obtenir un sous-ensemble de tous les employés dont le nom de famille est "Markovitch". 
 Vérifiez si le résultat contient un manager portant ce nom.
```sql
SELECT e.emp_no, e.first_name, e.last_name, dm.dept_no, dm.from_date
FROM employees e
LEFT JOIN dept_manager dm
ON e.emp_no = dm.emp_no
WHERE e.last_name = 'Markovitch'
ORDER BY dm.dept_no, e.emp_no;
```
6.5. Joindre les tables 'employees' et 'dept_manager' pour obtenir un sous-ensemble de tous les employés qui ont été embauchés avant le 31 janvier 1985.
```sql
SELECT e.emp_no, e.first_name, e.last_name, dm.dept_no, dm.from_date
FROM employees e
LEFT JOIN dept_manager dm
ON e.emp_no = dm.emp_no
WHERE e.hire_date < '1985-01-31'
ORDER BY dm.dept_no, e.emp_no;
```

# 7. Utiliser les fonctions d'agrégation avec JOIN

7.1. Quel est le salaire moyen pour les différents genres ?

7.2. Quel sera le résultat si nous faisons un SELECT de e.emp_no ?

```sql
SELECT e.emp_no, e.gender, AVG(s.salary) AS average_salary
FROM employees e
JOIN salaries s 
ON e.emp_no = s.emp_no
GROUP BY e.emp_no, gender; 
```

7.3. Combien d'hommes et de femmes managers avons-nous dans la base de données des employés ? base de données des employés ?


# 8.Joindre plus de deux tables
8.1. Extraire une liste de tous les noms et prénoms des managers, de leur numéro de service, de leur date d'embauche, de leur date d'entrée en fonction, et le nom du département

8.2. Quel sera le résultat de la requête suivante:
```sql
SELECT e.first_name, e.last_name, m.dept_no, e.hire_date, m.to_date, d.dept_name
FROM departments d
JOIN dept_manager m 
ON d.dept_no = m.dept_no
JOIN employees e 
ON m.emp_no = e.emp_no;
```

8.3. Récupérer le salaire moyen pour les différents départements


8.4. Récupérer le salaire moyen pour les différents départements où le salaire moyen est supérieur à 60000.




