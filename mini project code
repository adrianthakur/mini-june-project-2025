import tkinter as tk
from tkinter import messagebox
import numpy as np
import matplotlib.pyplot as plt

# -------------------------------
# Student Class
# -------------------------------
class Student:
    def __init__(self, name, roll_no, marks):
        self.name = name
        self.roll_no = roll_no
        self.marks = marks  

# -------------------------------
# Database Class
# -------------------------------
class StudentDatabase:
    def __init__(self):
        self.students = []

    def add_student(self, student):
        self.students.append(student)

    def get_all_students(self):
        return self.students

    def find_by_roll(self, roll_no):
        for student in self.students:
            if student.roll_no == roll_no:
                return student
        return None

# -------------------------------
# Performance Analyzer
# -------------------------------
class PerformanceAnalyzer:
    def __init__(self, students):
        self.students = students

    def analyze(self):
        subject_scores = {}
        for student in self.students:
            for subject, score in student.marks.items():
                subject_scores.setdefault(subject, []).append(score)

        if not subject_scores:
            return "No data available."

        results = ""
        for subject, scores in subject_scores.items():
            arr = np.array(scores)
            results += (
                f"{subject}:\n"
                f"  Avg: {np.mean(arr):.2f}, Min: {np.min(arr)}, "
                f"Max: {np.max(arr)}, Std Dev: {np.std(arr):.2f}\n"
            )
        return results

    def visualize_student(self, student):
        subjects = list(student.marks.keys())
        scores = list(student.marks.values())
        plt.bar(subjects, scores, color='skyblue')
        plt.title(f"Performance of {student.name}")
        plt.ylabel("Scores")
        plt.ylim(0, 100)
        plt.show()

    def visualize_all(self):
        for student in self.students:
            self.visualize_student(student)

# -------------------------------
# GUI Functions
# -------------------------------
db = StudentDatabase()

def add_student_ui(name_var, roll_var, marks_var):
    name = name_var.get()
    roll = roll_var.get()
    try:
        marks = eval(marks_var.get())  
        if not isinstance(marks, dict):
            raise ValueError("Marks must be a dictionary!")
        student = Student(name, roll, marks)
        db.add_student(student)
        messagebox.showinfo("Success", f"{name} added successfully.")
    except Exception as e:
        messagebox.showerror("Error", str(e))

def analyze_ui():
    analyzer = PerformanceAnalyzer(db.get_all_students())
    result = analyzer.analyze()
    messagebox.showinfo("Analysis", result)

def visualize_all_ui():
    PerformanceAnalyzer(db.get_all_students()).visualize_all()

# -------------------------------
# Launch GUI
# -------------------------------
def launch_gui():
    root = tk.Tk()
    root.title("🎓 Student Performance Analyzer")

    tk.Label(root, text="Name").pack()
    name_var = tk.StringVar()
    tk.Entry(root, textvariable=name_var).pack()

    tk.Label(root, text="Roll No").pack()
    roll_var = tk.StringVar()
    tk.Entry(root, textvariable=roll_var).pack()

    tk.Label(root, text="Marks (e.g., {'Math': 85, 'Sci': 90})").pack()
    marks_var = tk.StringVar()
    tk.Entry(root, textvariable=marks_var).pack()

    tk.Button(root, text="Add Student",
              command=lambda: add_student_ui(name_var, roll_var, marks_var)).pack(pady=5)

    tk.Button(root, text="Analyze", command=analyze_ui).pack(pady=5)
    tk.Button(root, text="Visualize All", command=visualize_all_ui).pack(pady=5)

    root.mainloop()

# -------------------------------
# Main Entry Point
# -------------------------------
if __name__ == "__main__":
    # ---------------------------------
    # Preloaded Student Data (Optional)
    # ---------------------------------
    preloaded_students = [
        {"name": "Aditi", "roll": "101", "marks": {"Math": 91, "Sci": 88, "Eng": 85}},
        {"name": "Ravi", "roll": "102", "marks": {"Math": 75, "Sci": 82, "Eng": 79}},
        {"name": "Simran", "roll": "103", "marks": {"Math": 89, "Sci": 91, "Eng": 93}},
    ]

    for s in preloaded_students:
        student = Student(s["name"], s["roll"], s["marks"])
        db.add_student(student)

    # Launch GUI
    launch_gui()    
