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


















