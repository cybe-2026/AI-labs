# Lab1


# Exercise 1:


## Task:Degree Honors RuleAdd a new rule to `UNIVERSITY_KB["rules"]` for students completing their degree program:
 - Condition: `cgpa >= 3.70` and `disciplinary_warnings == 0` $\rightarrow$ Status: "Graduated with Magna Cum Laude Honors".
 
 ```python
UNIVERSITY_KB = {
    "rules": []
}
UNIVERSITY_KB["rules"].append({
    "id": "RULE_07",
    "conditions": {
        "cgpa_min": 3.70,
        "disciplinary_warnings": 0
    },
    "status": "Graduated with Magna Cum Laude Honors"
})

print("New Degree Honors Rule Added Successfully!")
```
_____________________________________________________________________________________________________________________________
# Exercise 2:-Tracing Forward ChainingModify `evaluate_student()` to print each evaluated rule condition as the loop runs, demonstrating step-by-step logical deduction.

## Task: Modify the evaluate_student() function to print every evaluated rule condition.

def evaluate_student(student_record, kb):
```python
    print(f"\n--- EVALUATING STUDENT: {student_record['student_name']} ---")

    # Step 1: Check Attendance Rule
    print("\nChecking RULE_01: Attendance")

    if student_record["attendance"] < 75:

        print("Condition TRUE: Attendance is below 75%")

        attendance_rule = next(
            r for r in kb["rules"]
            if r["condition_type"] == "attendance_below"
        )

        return {
            "rule_id": attendance_rule["id"],
            "grade": attendance_rule["grade"],
            "status": attendance_rule["status"],
            "action": attendance_rule["action"]
        }

    print("Condition FALSE: Attendance is 75% or above")

    # Step 2: Check Marks Rules
    marks = student_record["total_marks"]

    for rule in kb["rules"]:

        if rule["condition_type"] == "marks_range":

            print(f"\nChecking {rule['id']}")
            print(f"Condition: {rule['conditions']}")

            if rule["conditions"]["marks_min"] <= marks <= rule["conditions"]["marks_max"]:

                print("Condition TRUE: Rule matched!")

                return {
                    "rule_id": rule["id"],
                    "grade": rule["grade"],
                    "status": rule["status"],
                    "action": rule["action"]
                }

            else:
                print("Condition FALSE: Rule not matched")

    return {
        "rule_id": "UNKNOWN",
        "grade": "N/A",
        "status": "Invalid Score Entry",
        "action": "Verify submitted marks with the exam department."
    }
```
