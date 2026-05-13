# 1. Sample Dataset (employees collection)

db.employees.insertMany([  
{ name: "Amit", age: 28, department: "Computer Science", salary: 70000, expertise: "Java" },  
{ name: "Anjali", age: 32, department: "Mathematics", salary: 65000, expertise: "Data Analysis" },  
{ name: "Rohit", age: 40, department: "Physics", salary: 80000, expertise: "Quantum Physics" },  
{ name: "Sneha", age: 27, department: "Biology", salary: 55000, expertise: "Genetics" },  
{ name: "Arjun", age: 35, department: "Mathematics", salary: 72000, expertise: "Algebra" },  
{ name: "Priya", age: 29, department: "Computer Science", salary: 60000, expertise: "Data Science" },  
{ name: "Karan", age: 45, department: "Physics", salary: 90000, expertise: "Astrophysics" },  
{ name: "Meena", age: 31, department: "Biology", salary: 58000, expertise: "Microbiology" },  
{ name: "Akash", age: 26, department: "Computer Science", salary: 52000, expertise: "Java" },  
{ name: "Pooja", age: 38, department: "Mathematics", salary: 67000, expertise: "Statistics" },  
{ name: "Alok", age: 33, department: "Physics", salary: 75000, expertise: "Thermodynamics" },  
{ name: "Neha", age: 24, department: "Biology", salary: 50000, expertise: "Botany" },  
{ name: "Aditya", age: 36, department: "Computer Science", salary: 82000, expertise: "Data Engineering" },  
{ name: "Rahul", age: 41, department: "Mathematics", salary: 71000, expertise: "Calculus" },  
{ name: "Simran", age: 30, department: "Physics", salary: 68000, expertise: "Optics" }  
])
 store this data in your mongo database first copy and run this query
---

# 2. Queries with Answers

---

## 1. Salary > 65000

db.employees.find({ salary: { $gt: 65000 } })

Answer:  
Amit, Rohit, Arjun, Karan, Pooja, Alok, Aditya, Rahul, Simran

---

## 2. Age < 30

db.employees.find({ age: { $lt: 30 } })

Answer:  
Amit, Sneha, Priya, Akash, Neha

---

## 3. Mathematics Department

db.employees.find({ department: "Mathematics" })

Answer:  
Anjali, Arjun, Pooja, Rahul

---

## 4. Expertise in Java

db.employees.find({ expertise: "Java" })

Answer:  
Amit, Akash

---

## 5. Count Employees

db.employees.countDocuments()

Answer:  
15

---

## 6. Top 5 Highest Paid

db.employees.find().sort({ salary: -1 }).limit(5)

Answer:  
Karan, Aditya, Rohit, Alok, Arjun

---

## 7. Lowest 5 Salaries

db.employees.find().sort({ salary: 1 }).limit(5)

Answer:  
Neha, Akash, Sneha, Meena, Priya

---

## 8. Age Between 30 and 40

db.employees.find({ age: { $gte: 30, $lte: 40 } })

Answer:  
Anjali, Arjun, Meena, Pooja, Alok, Aditya, Simran

---

## 9. Name starts with A

db.employees.find({ name: { $regex: "^A" } })

Answer:  
Amit, Anjali, Arjun, Akash, Alok, Aditya

---

## 10. Not in Physics

db.employees.find({ department: { $ne: "Physics" } })

Answer:  
All except Rohit, Karan, Alok, Simran

---

## 11. Average Salary

db.employees.aggregate([  
  { $group: { _id: null, avgSalary: { $avg: "$salary" } } }  
])

Answer:  
Around 67,333

---

## 12. Maximum Salary

db.employees.aggregate([  
  { $group: { _id: null, maxSalary: { $max: "$salary" } } }  
])

Answer:  
90000

---

## 13. Minimum Salary

db.employees.aggregate([  
  { $group: { _id: null, minSalary: { $min: "$salary" } } }  
])

Answer:  
50000

---

## 14. Group by Department

db.employees.aggregate([  
  { $group: { _id: "$department" } }  
])

Answer:  
Computer Science, Mathematics, Physics, Biology

---

## 15. Total Salary per Department

db.employees.aggregate([  
  { $group: { _id: "$department", total: { $sum: "$salary" } } }  
])

---

## 16. Average Age per Department

db.employees.aggregate([  
  { $group: { _id: "$department", avgAge: { $avg: "$age" } } }  
])

---

## 17. Salary Between 50000 and 60000

db.employees.find({ salary: { $gte: 50000, $lte: 60000 } })

Answer:  
Sneha, Priya, Meena, Akash, Neha

---

## 18. Sort by Age Descending

db.employees.find().sort({ age: -1 })

---

## 19. Distinct Departments

db.employees.distinct("department")

Answer:  
Computer Science, Mathematics, Physics, Biology

---

## 20. Expertise contains "Data"

db.employees.find({ expertise: { $regex: "Data" } })

Answer:  
Anjali, Priya, Aditya

---

## 21. Skip First 10 Records

db.employees.find().skip(10)

---

## 22. Salary >60000 AND age <40

db.employees.find({  
  salary: { $gt: 60000 },  
  age: { $lt: 40 }  
})

Answer:  
Amit, Anjali, Arjun, Pooja, Alok, Aditya, Simran

---

## 23. Computer Science OR Physics

db.employees.find({  
  $or: [  
    { department: "Computer Science" },  
    { department: "Physics" }  
  ]  
})

---

## 24. Not in Biology

db.employees.find({ department: { $ne: "Biology" } })

---

## 25. Show Only Name and Salary

db.employees.find({}, { name: 1, salary: 1, _id: 0 })

---

# Final Tip for Students

- `find()` → filtering
- `sort()` → ordering
- `limit()` → top records
- `aggregate()` → calculations
- `distinct()` → unique values