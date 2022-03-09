# Pewlett-Hackard-Analysis-
Deliverable 3 Written Report
Overview of the analysis: 
The Overview of this analysis was by using Postgre SQL Database PGAdmin Software I was able to conduct an outcome from the different CSV files for creating tables of the data to them
be able to draw a conclusion with the Query tables. In Deliverable 1 we focused on finding the number of employees that will be retiring soon by their job title. 
Then in Deliverable 2 the focus was on how many employees were eligible for the mentorship program in which the company conducts. 
Results:
From The Results of Deliverable 1 the conclusion that was drawn was that there will be two major jobs that are going to have a large number of employees retirement coming of 
this upcoming year. There will be the senior staff with 24,926 employees retiring as well as Senior Engineering will be again a large number of staff 25,916. The highest amount
of employees is the Senior staff, and the Senior Engineering.  
The Outcome for Deliverable 1  Table Query. 
![image](https://user-images.githubusercontent.com/95897182/157515147-53073f5e-0084-44fa-9442-2a50d4ba59f3.png)

 The code that was used to create this table was: 

SELECT	e.emp_no,
		e.first_name,
		e.last_name,
		t.title,
		t.from_date,
		t.to_date
INTO retirement_titles
FROM employees AS e
JOIN titles AS t
	ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
ORDER BY e.emp_no ASC;
SELECT DISTINCT ON (rt.emp_no) rt.emp_no,
	rt.first_name,
	rt.last_name,
	rt.title
INTO unique_titles
FROM retiring_titles AS rt
WHERE rt.to_date = ('9999-01-01')
ORDER BY rt.emp_no, rt.to_date DESC;
-- Number of Titles
SELECT COUNT(title), title  
INTO retiring_titles  
FROM unique_titles
GROUP BY title
ORDER BY COUNT(title) DESC;



Deliverable 2- The Employees Eligible for mentorship program. From Results based of Deliverable 2 I was able to draw the conclusion for the mentorship program.
Several different outcomes and data were gathered. The Mentorship program is meant to help the employees along the way in their title be able to move up along the way of their career. 
The Code That was used to create the tables and outcome was: 

SELECT DISTINCT ON (e.emp_no) e.emp_no,
		e.first_name,
		e.last_name,
		e.birth_date,
		de.from_date,
		de.to_date,
		t.title
INTO mentorship_eligibility
FROM employees AS e
JOIN dept_emp AS de
	ON (e.emp_no = de.emp_no)
JOIN titles AS t
	ON (e.emp_no = t.emp_no)
WHERE de.to_date = ('9999-01-01')
	AND (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY e.emp_no ASC;
SELECT DISTINCT ON (e.emp_no) e.emp_no,
		e.first_name,
		e.last_name, 
		ce.to_date,
		s.salary
INTO sal_saved
FROM employees AS e
JOIN salaries AS s
	ON (e.emp_no = s.emp_no)
JOIN current_emp AS ce
	ON (e.emp_no = ce.emp_no)
WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
	AND (e.hire_date BETWEEN '1985-01-01' AND '1988-12-31')
	AND ce.to_date = ('9999-01-01')
ORDER BY e.emp_no, ce.to_date DESC;

SELECT CAST(SUM(salary) as money)
FROM sal_saved
SELECT	dm.dept_no,
		d.dept_name,
		dm.emp_no,
		e.first_name,
		e.last_name,
		e.birth_date,
		dm.from_date
FROM dept_manager AS dm
JOIN departments AS d
	ON (dm.dept_no = d.dept_no)
JOIN employees AS e
	ON (dm.emp_no = e.emp_no)
WHERE to_date = '9999-01-01'
 Deliverable 2 Tables Queries.
 
![image](https://user-images.githubusercontent.com/95897182/153771665-f2d2eafe-e60e-4114-aeb5-1b380a285398.png)

![image](https://user-images.githubusercontent.com/95897182/153771713-0af4b70f-d946-42a1-86e4-3bd2e2ce4541.png)

![image](https://user-images.githubusercontent.com/95897182/153771769-20cab65a-90bf-40a7-8db6-40f9e2aaf52c.png) 
 
How many roles will need to be filled as the "silver tsunami" begins to make an impact? There is a decent number of roles that will be needed, with 1,900 employees retiring soon from each department.
The Pewlett Hackard company will have a huge silver tsunami with a whopping grand total of 72,000 employees 
that will be retiring this year. 
The major of them come from the job title as a senior engineer and senior staff. Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees? 
Yes, I think based on this analysis there were a huge number of employees that were in this mentorship where they did mentor the next generation to come that even though there are more employees retiring then 
staying in the company there were enough from the program that they will be able to know their position title and then as the company continues to hire more the mentorship program will be able to continue to educate and mentor fellow employees.
