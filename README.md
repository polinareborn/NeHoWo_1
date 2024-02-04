class Student:
    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}

    def rate_lctr(self, lecturer, course, grade):
        if isinstance(lecturer, Lecturer) and course in self.courses_in_progress and course in lecturer.courses_in_progress:
            if course in lecturer.grades:
                lecturer.grades[course] += [grade]
            else:
                lecturer.grades[course] = [grade]
        else:
            return 'Ошибка'
    def __avg_grades__ (self) :
        sum_grades = 0
        for g in self.grades:
            sum_grades += g
        avg_grades = sum_grades/len(self.grades)
        return avg_grades
    def __str__(self):
        fin_courses = ",".join(self.finished_courses)
        progress_courses = ",".join(self.courses_in_progress)
        return (f'Имя : {self.name}\nФамилия : {self.surname}\nСредняя оценка '
                f'за домашние задания :{self.__avg_grades__}\nКурсы в процессе '
                f'изучения: {progress_courses}\nЗавершённые курсы:{fin_courses}')
    def __lt__(self,other):
        return self.__avg_grades__ < other.__avg.grades


class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []


class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name,surname)
        self.grades = {}

    def __avg_grades__ (self) :
        sum_grades = 0
        for g in self.grades:
            sum_grades += g
        avg_grades = sum_grades/len(self.grades)
        return avg_grades
    def __str__(self):
        return (f'Имя : {self.name}\nФамилия : {self.surname}\nСредняя оценка '
                f'за лекции :{self.__avg_grades__}')
    def __lt__(self,other):
        return self.__avg_grades__ < other.__avg.grades
class Reviewer(Mentor):
    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'
    def __str__(self):
        return f"Имя : {self.name}\nФамилия : {self.surname}"
def average_grade_on_the_course_st(students, course):
    if not isinstance(students, list):
        return "Not list"
    all_average_grade = []
    for student  in students:
        all_average_grade.extend(student.average_grade_course_st.get(course, []))
    if not all_average_grade:
        return "По такому курсу ни у кого нет оценок"
    return round(sum(all_average_grade) / len(all_average_grade), 2)
def average_grade_on_the_course_lctr(lecturers, course):
    if not isinstance(lecturers, list):
        return "Not list"
    all_average_grade = []
    for lecturer  in lecturers:
        all_average_grade.extend(lecturer.average_grade_course_st.get(course, []))
    if not all_average_grade:
        return "По такому курсу ни у кого нет оценок"
    return round(sum(all_average_grade) / len(all_average_grade), 2)

student_1 = Student('Юрий', 'Ананикян', 'Мужчина')
student_1.courses_in_progress += ['Python']
student_1.finished_courses += ['C++']
student_1.finished_courses += ['JavaScript']
student_1.finished_courses += ["Основы программирования"]
student_1.grades = {'Python': [9.5], 'JavaScript': [7.5], 'C++': [9.0]}

student_2 = Student('Надежда', 'Агафонова', 'Женщина')
student_2.courses_in_progress += ['Python']
student_2.finished_courses += ['JavaScript']
student_2.finished_courses +=["Основы программирования"]
student_2.grades = {'Python': [9.5], 'JavaScript': [8.9]}

student_list=[student_1, student_2]

mentor_1=Mentor('Виталий','Одинцов')
mentor_1.courses_attached=['Python', 'C++']

mentor_2=Mentor('Вероника', 'Княжна')
mentor_2.courses_attached=['Python', 'C++','JavaScript']

lecturer_1=Lecturer('Виктор','Беспаленов')
lecturer_1.courses_attached=['Python' ]
lecturer_1.grades={'Python' : [8.5]}

lecturer_2=Lecturer('Анастас','Сихиди')
lecturer_2.courses_attached=['C++', 'JavaScript']
lecturer_2.grades={'С++' : [8.5],'JavaScript' : [7.5]}

reviewer_1=Reviewer('Антон', 'Усепов')
reviewer_1.courses_attached=['Python', 'C++','JavaScript']

reviewer_1=Reviewer('Валентина', 'Шевченко')
reviewer_1.courses_attached=['Python', 'C++','JavaScript']
