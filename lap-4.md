students = {
    "S001": {
        "name": "Alice Chen",
        "courses": {
            "CS101": {"grade": 92, "credits": 3},
            "MATH201": {"grade": 88, "credits": 4},
            "AI301": {"grade": 95, "credits": 3},
        },
        "advisor": "Dr. Smith",
    },
    "S002": {
        "name": "Bob Lee",
        "courses": {
            "CS101": {"grade": 85, "credits": 3},
            "MATH201": {"grade": 90, "credits": 4},
        },
        "advisor": "Dr. Patel",
    },
}

# TODO: Implement the tasks above using nested dict access

ACC = students["S001"]\
    ["courses"]\
    ["AI301"]\
    ["grade"]
print(ACC)
def GPA (grade):

  if grade >= 96:
      gpa = 5
  elif grade >= 90:
      gpa = 4
  elif grade >= 85:
      gpa = 3.5
  else:
      gpa = 3
  print("GPA is ", gpa)
  return gpa
#0-80 c =3
#85-89B=3.5
#90-95A=4
#96-100A+=

OP = GPA(students["S001"]\
    ["courses"]\
    ["AI301"]\
    ["grade"])

Avv = students["S002"]\
    ["courses"]\
    ["CS101"]\
    ["grade"]

print(Avv)

AVV = students["S001"]\
    ["courses"]\
    ["CS101"]\
    ["grade"]
print(AVV)

grades = [92, 90, 85, 95,88]

a = sum(grades)/len(grades)
print(a)
op = GPA(students["S001"]\
    ["courses"]\
    ["MATH201"]\
    ["grade"])
if OP > op:
    print("Alice Chen is the student with highest GPA")
else:
    print("Bob Lee is the student with highest GPA")
