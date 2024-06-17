class Student:
    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}

    def grade_s(self, name, grade, course_name):
        pass

    def  grade_lecture(self, name, grade, course_name):
        if isinstance(name, Lecturer) and  course_name in self.courses_in_progress and self.courses_in_progress and course_name in name.courses_attached:
            name.grades.setdefault(course_name, [])
            name.grades[course_name].append(grade)

class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []

    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'

best_student = Student('Ruoy', 'Eman', 'your_gender')
best_student.courses_in_progress += ['Python']

cool_mentor = Mentor('Some', 'Buddy')
cool_mentor.courses_attached += ['Python']

cool_mentor.rate_hw(best_student, 'Python', 10)
cool_mentor.rate_hw(best_student, 'Python', 10)
cool_mentor.rate_hw(best_student, 'Python', 10)

print(best_student.grades)


class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = {}


class Reviewer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = {}

student_1 = Student("Анна", "Моисеева", "жен")
student_1.courses_in_progress.append("python")

student_2 = Student("Борис", "Боев", "муж")
student_2.courses_in_progress.append("java")

lector_1 = Lecturer("Михаил", "Залешин")
lector_1.courses_attached.append("python")
lector_1.courses_attached.append("java")

student_1.grade_lecture(lector_1, 10, "python")
student_2.grade_lecture(lector_1, 10, "java")

print(lector_1.grades)