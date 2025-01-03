// A. Define an abstract named Role with the displayRole method
abstract class Role {
  void displayRole();
}

// B. Create a class Person with name, age, address, and a reference to Role
class Person {
  String name;
  int age;
  String address;
  Role role;

  // Constructor
  Person(this.name, this.age, this.address, this.role);

  // Getter methods
  String get getName => name;
  int get getAge => age;
  String get getAddress => address;
}

// C. Create a class Student that extends Person
class Student extends Person implements Role {
  String studentID;
  String grade;
  List<double> courseScores = [];

  // Constructor
  Student(String name, int age, String address, this.studentID, this.grade, this.courseScores)
      : super(name, age, address, Student(name, age, address, studentID, grade, courseScores));

  // Override the displayRole method
  @override
  void displayRole() {
    print("Role: Student");
  }

  // Method to calculate average score
  double calculateAverageScore() {
    if (courseScores.isEmpty) {
      return 0.0;
    }
    double total = 0.0;
    for (double score in courseScores) {
      total += score;
    }
    return total / courseScores.length;
  }
}

// D. Create another class Teacher that extends Person
class Teacher extends Person implements Role {
  String teacherID;
  List<String> coursesTaught = [];

  // Constructor
  Teacher(String name, int age, String address, this.teacherID, this.coursesTaught)
      : super(name, age, address, Teacher(name, age, address, teacherID, coursesTaught));

  // Override the displayRole method
  @override
  void displayRole() {
    print("Role: Teacher");
  }

  // Method to display the courses taught by the teacher
  void displayCoursesTaught() {
    print("Courses Taught:");
    for (String course in coursesTaught) {
      print("- $course");
    }
  }
}

// E. Create a class StudentManagementSystem
class StudentManagementSystem {
  // Main method to test the system
  static void main() {
    // Creating instances of Student and Teacher classes
    var student = Student("John Doe", 20, "123 Main St", "S001", "A", [90, 85, 82]);
    var teacher = Teacher("Mrs. Smith", 35, "456 Oak St", "T001", ["Math", "English", "Bangla"]);

    // Displaying student information
    print("Student Information:");
    student.displayRole();
    print("Name: ${student.getName}");
    print("Age: ${student.getAge}");
    print("Address: ${student.getAddress}");
    print("Average Score: ${student.calculateAverageScore()}");

    print("");

    // Displaying teacher information
    print("Teacher Information:");
    teacher.displayRole();
    print("Name: ${teacher.getName}");
    print("Age: ${teacher.getAge}");
    print("Address: ${teacher.getAddress}");
    teacher.displayCoursesTaught();
  }
}

// Call the main method to run the system
void main() {
  StudentManagementSystem.main();
}
