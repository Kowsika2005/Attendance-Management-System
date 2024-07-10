# Attendance-Management-System
import java.util.*;

class Student {
    private String name;
    private String rollNumber;
    private String branch;
    private String section;
    private boolean present;

    public Student(String name, String rollNumber, String branch, String section) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.branch = branch;
        this.section = section;
        this.present = false;
    }

    public String getName() {
        return name;
    }

    public String getRollNumber() {
        return rollNumber;
    }

    public String getBranch() {
        return branch;
    }

    public String getSection() {
        return section;
    }

    public boolean isPresent() {
        return present;
    }

    public void markAttendance(boolean present) {
        this.present = present;
    }
}

class AttendanceManager {
    private ArrayList<Student> students;

    public AttendanceManager() {
        students = new ArrayList<>();
    }

    public void addStudent(String name, String rollNumber, String branch, String section) {
        Student student = new Student(name, rollNumber, branch, section);
        students.add(student);
        System.out.println("Student added");
    }

    public void markAttendance(String rollNumber, boolean present) {
        for (Student student : students) {
            if (student.getRollNumber().equals(rollNumber)) {
                student.markAttendance(present);
                System.out.println("Attendance marked");
                return;
            }
        }
        System.out.println("Student not found");
    }

    public void viewAttendanceReport() {
        System.out.println("Attendance Report:");
        for (Student student : students) {
            System.out.println("Roll Number: " + student.getRollNumber() + ", Name: " + student.getName() + ", Present: " + (student.isPresent() ? "Yes" : "No"));
        }
    }
}

public class AttendanceSystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        AttendanceManager manager = new AttendanceManager();
        while (true) {
            System.out.println("1. Add Student");
            System.out.println("2. Mark Attendance");
            System.out.println("3. View Attendance Report");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = sc.nextInt();
            sc.nextLine();
            switch (choice) {
                case 1:
                    System.out.print("Enter name: ");
                    String name = sc.nextLine();
                    System.out.print("Enter roll number: ");
                    String rollNumber = sc.nextLine();
                    System.out.print("Enter branch: ");
                    String branch = sc.nextLine();
                    System.out.print("Enter section: ");
                    String section = sc.nextLine();
                    manager.addStudent(name, rollNumber, branch, section);
                    break;
                case 2:
                    System.out.print("Enter student roll number: ");
                    String roll = sc.nextLine();
                    System.out.print("Is the student present YES or NO: ");
                    boolean present = sc.nextBoolean();
                    manager.markAttendance(roll, present);
                    break;
                case 3:
                    manager.viewAttendanceReport();
                    break;
                case 4:
                    System.out.println("Exiting");
                    sc.close();
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice");
            }
        }
    }
}
