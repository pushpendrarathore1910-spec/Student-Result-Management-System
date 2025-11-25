# Student-Result-Management-System
import csv
import os

FILE = "students.csv"

# -------------------- Initialize File --------------------
def init_file():
    if not os.path.exists(FILE):
        with open(FILE, 'w', newline='') as f:
            writer = csv.writer(f)
            writer.writerow(["Roll No", "Name", "Sub1", "Sub2", "Sub3", "Sub4", "Sub5", "Percentage", "Grade"])

# -------------------- Add Student --------------------
def add_student():
    roll = input("Enter Roll Number: ")
    name = input("Enter Name: ")

  marks = []
    for i in range(1, 6):
        m = int(input(f"Enter marks for Subject {i}: "))
        marks.append(m)

  percentage = sum(marks) / 5

   # Grade calculation
   if percentage >= 90:
        grade = "A+"
    elif percentage >= 80:
        grade = "A"
    elif percentage >= 70:
        grade = "B"
    elif percentage >= 60:
        grade = "C"
    else:
        grade = "D"

  with open(FILE, 'a', newline='') as f:
        writer = csv.writer(f)
        writer.writerow([roll, name] + marks + [percentage, grade])

  print("\nStudent added successfully!\n")

# -------------------- View All Students --------------------
def view_all():
    with open(FILE, 'r') as f:
        reader = csv.reader(f)
        for row in reader:
            print(row)

# -------------------- Search Student --------------------
def search_student():
    roll = input("Enter Roll Number to search: ")
    found = False

   with open(FILE, 'r') as f:
        reader = csv.reader(f)
        for row in reader:
            if row[0] == roll:
                print("\nStudent Found:")
                print(row)
                found = True
                break

  if not found:
        print("\nNo record found for this Roll Number.\n")

# -------------------- Delete Student --------------------
def delete_student():
    roll = input("Enter Roll Number to delete: ")
    rows = []

  with open(FILE, 'r') as f:
        reader = csv.reader(f)
        for row in reader:
            if row[0] != roll:
                rows.append(row)

   with open(FILE, 'w', newline='') as f:
        writer = csv.writer(f)
        writer.writerows(rows)
    print("\nRecord deleted (if existed).\n")

# -------------------- Main Menu --------------------
def menu():
    init_file()

   while True:
        print("\n===== Student Result Management System =====")
        print("1. Add Student")
        print("2. View All Students")
        print("3. Search Student")
        print("4. Delete Student")
        print("5. Exit")

   choice = input("Enter your choice: ")

   if choice == '1':
            add_student()
        elif choice == '2':
            view_all()
        elif choice == '3':
            search_student()
        elif choice == '4':
            delete_student()
        elif choice == '5':
            print("Exiting...")
            break
        else:
            print("Invalid choice! Try again.")

menu()
