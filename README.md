# GradeMaster

GradeMaster is a Java program developed during my internship at CodTech IT Solutions. This application allows users to input grades for different subjects or assignments, calculates the average grade, displays the overall grade, and provides additional information such as letter grades or GPA.

## Features

- **Input Grades**: Users can input grades for various subjects or assignments.
- **Calculate Average Grade**: The program calculates the average grade based on the inputted grades.
- **Overall Grade Display**: Displays the overall grade with additional information like letter grades or GPA.
- **Grade Management**: Provides options to add, edit, and delete grades as needed.

## Usage

1. **Input Grades**:
   - Start the application and follow the prompts to enter grades for each subject or assignment.

2. **Calculate Average**:
   - Once all grades are entered, the program will calculate and display the average grade.

3. **View Overall Grade**:
   - The program will show the overall grade, including the letter grade and GPA.

4. **Manage Grades**:
   - Use the provided options to add new grades, edit existing grades, or delete grades as needed.

## Usage with BlueJ

To run the program using BlueJ, follow these steps:

1. Open BlueJ and create a new project.
2. Add the GradeMaster.java file to the project.
3. Compile the program by selecting "Compile" from the BlueJ menu.
4. Right-click on the GradeMaster class and select "void main(String[] args)" to execute the program.

## Contact

For any inquiries or feedback, please contact  - [Amrin Shaikh].

Project Link: [https://github.com/your_username/GradeMaster](https://github.com/your_username/GradeMaster)







import java.util.ArrayList;
import java.util.Scanner;

class Grade {
    private String subject;
    private double grade;

    public Grade(String subject, double grade) {
        this.subject = subject;
        this.grade = grade;
    }

    public String getSubject() {
        return subject;
    }

    public double getGrade() {
        return grade;
    }

    public void setGrade(double grade) {
        this.grade = grade;
    }
}

class Student {
    private String name;
    private ArrayList<Grade> grades;

    public Student(String name) {
        this.name = name;
        this.grades = new ArrayList<>();
    }

    public void addGrade(String subject, double grade) {
        grades.add(new Grade(subject, grade));
    }

    public void editGrade(String subject, double newGrade) {
        for (Grade g : grades) {
            if (g.getSubject().equals(subject)) {
                g.setGrade(newGrade);
                break;
            }
        }
    }

    public void deleteGrade(String subject) {
        grades.removeIf(g -> g.getSubject().equals(subject));
    }

    public double calculateAverageGrade() {
        double totalGrade = 0;
        for (Grade g : grades) {
            totalGrade += g.getGrade();
        }
        return totalGrade / grades.size();
    }

    public void displayGrades() {
        System.out.println("Grades for " + name + ":");
        for (Grade g : grades) {
            System.out.println(g.getSubject() + ": " + g.getGrade());
        }
        System.out.println("Average grade: " + calculateAverageGrade());
    }
}

public class StudentGradeTracker {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter student name: ");
        String name = scanner.nextLine();
        Student student = new Student(name);

        while (true) {
            System.out.println("\n1. Add Grade\n2. Edit Grade\n3. Delete Grade\n4. Display Grades\n5. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter subject: ");
                    String subject = scanner.nextLine();
                    System.out.print("Enter grade: ");
                    double grade = scanner.nextDouble();
                    student.addGrade(subject, grade);
                    break;
                case 2:
                    System.out.print("Enter subject to edit grade: ");
                    String subjectToEdit = scanner.nextLine();
                    System.out.print("Enter new grade: ");
                    double newGrade = scanner.nextDouble();
                    student.editGrade(subjectToEdit, newGrade);
                    break;
                case 3:
                    System.out.print("Enter subject to delete grade: ");
                    String subjectToDelete = scanner.nextLine();
                    student.deleteGrade(subjectToDelete);
                    break;
                case 4:
                    student.displayGrades();
                    break;
                case 5:
                    System.out.println("Exiting...");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
