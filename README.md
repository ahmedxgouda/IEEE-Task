# IEEE Task (Intermediate) - Ahmed Gouda

## Programming

### Q1 - What is the best time complexity that can be achieved to count the number of occurrences of a given subsequence in a given array, assuming the subsequence length is always 2? (A subsequence of an array is the array resulted from removing any number of elements (possibly zero) from the original array). Explain the idea of your solution with no code. (Feel free to use Arabic)

---

- **Complexity: O(N).**
- **Idea: to get the number of occurences of the subsequence, we need to sum the counts of the second element that comes after every position of the first element in the array.**
- **Steps:**

> 1. Suppose that the array has a length of n, and the first element of the subsequence is x, and the second is y.  
> 2. We can make two arrays of length "n", with names "countX", and "countY". Where countX[i], and countY[j] represent the number of occurences of "x" until index i, and "y" until index "j" respectively.
> 3. We loop through the array, starting from index 1 to n - 1.
> 4. If we found x we will set countX[i] to countX[i - 1] + 1, else we will set it to countX[i - 1], and same thing with y.
> 5. After the loop is finished, we set a variable to indicate the increase of the countX, lets name it temp, we also set a variable "res" to contain the result.
> 6. We loop through countX and countY from 0 to n - 1.
> 7. If countX[i] > temp, then there is an increase of the count, so we will add (countY[n - 1] - countY[i]) to th result - We subtract countY[i] to exclude the count of occurences before the increase of the count-, we also will set temp to countX[i].
> 8. Else: we will just continue the loop.
> 9. Now, our result has been calculated and we can return "res".

---
---

### Q3: Explain method overloading in terms of an E-commerce OOP application

---

**Method overloading allows different methods to have the same name with different signatures. A method signature defines the return type of the method and the type and the number of the parameters. This helps to avoid using inconsistent names for methods that do the same thing.**

---
---
---

## Web Development

### Q1 JavaScript can run scripts on the client side. Can we use it directly to interact with the database system? Explain your answer

---

**Yes, by making an AJAX call. We can add an event listener via DOM that activates when the event we want occurs.**

---
---

### Q2 What is the difference between Authentication and Authorization?

---

**Authentication is the pass to enter the room. Authorization is the privileges that a roommate has. A more technical example: If a user is allowed to login to the website then they are authenticated, but not all users have the same roles. A superuser can do sensitive operations like deleting the whole site, and deleting users from the databases, but a normal user does not have these privileges.**

---
---

### Q3 HTTP protocol is stateless, how do web servers overcome this to manage the request's state?

---

**They use cookies which are stored on the user's host, and managed by the user's browser.**

---
---
---

## Databases

### Q1 Explain (in Arabic) the difference between LEFT JOIN and INNER JOIN

---

<div dir="rtl">
	<b>
		LEFT JOIN: دا مش بس بيجيب الداتا المتحققة في الشرط، لا دا كمان بيجيب كل الصفوف اللي موجودة في الجدول اللي بعد from ولو ملقاش مكافئ ليها في الطرف الآخر بيعتبر العمود اللي جاي من الجدول اللي بعد JOIN في الصف ب NULL.
		<br>
		INNER JOIN: دا بقى بيجيب الداتا المتحققة في الشرط فقط ولو في صفوف زيادة مش متحققة في الشرط دا بيهملها ومش بيجيبها في النتيجة، وبالتالي مش هيكون في صفوف ب NULL إلا لو كانت موجودة ب NULL بالفعل في الجدول يعني العلاقة ملهاش دخل هنا.
	</b>
</div>

---
---

### Q2 You have a posts table in a blog website database. You need to implement a simple search functionality that looks for the given search query inside the title and the content of the post and returns the post if the query is present. The search functionality should be case insensitive. Order the posts according to the number of views descendingly. Write the SQL query that can be used to achieve this functionality


---

```sql
SELECT *
FROM posts
WHERE LOWER(title) LIKE "%title_search%" AND LOWER(content) LIKE "%content_search%"
ORDER BY num_of_views desc;
```

---
---

### Q3 **(Advanced - Bonus)** A company's executives are interested in seeing who earns the most money in each of the company's departments. A **high earner** in a department is an employee who has a salary in the **top three unique** salaries for that department. Write a solution to find the employees who are **high earners** in each of the departments

> ⚠️ Note: The code works in postgres. I did not test it in another DBMS.

---

```sql
SELECT t1.name as employee_name, employee_rank, t1.salary, d.name as department_name
FROM (
	SELECT ROW_NUMBER() OVER(PARTITION BY e.departmentID ORDER BY e.salary DESC) as employee_rank,
	    e.id, e.name, e.departmentId, e.salary
	from Employee e
	) AS t1
JOIN Department d
ON d.id = t1.departmentId
WHERE employee_rank <= 3;
```

---
---
---
<center><b>End of questions</b></center>
