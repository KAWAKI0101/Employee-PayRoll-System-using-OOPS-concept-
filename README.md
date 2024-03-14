import java.util.ArrayList;
import java.util.List;

abstract class Employee{ // I using the Abstraction class for security purpors
    private String name;
    private int id;

    public Employee(String name, int id){  // constructor 
        this.name = name;
        this.id = id;
    }

    public String getName(){
        return name;
    }

    public int getId(){
        return id;
    }

    public abstract double calculateSalary();

    @Override
    public String toString(){
        return "Employee [name = " + name+", id = " + id + ", salary=" + calculateSalary() + "]";
    }
}

  class FullTimeEmployee extends Employee{
    private double monthlySalary;

    // constructor
    public FullTimeEmployee(String name, int id, double monthlySalary){
        super(name, id);
        this.monthlySalary = monthlySalary;
    }

    @Override
    public double calculateSalary(){
        return monthlySalary;
    }

}

class PartTimeEmpoyee extends Employee{
    private int hoursWorked;
    public double hourlyRate;

    public PartTimeEmpoyee(String name, int id, int hourlyWorked,double hourlyRate){
        super(name,id);
        this.hoursWorked = hourlyWorked;
        this.hourlyRate = hourlyRate;
    }

    @Override
    public double calculateSalary() {
        return hoursWorked * hourlyRate;
    }
}
class PayroleSystem{
    private List<Employee> employeeList ;

    public PayroleSystem(){
        employeeList = new ArrayList<>();
    }

    // Add Employees
    public void addEmployee(Employee employee){
        employeeList.add(employee);
    }

    public void RemoveEmployee(int id){
        Employee employeeRemove = null;

        for(Employee employee : employeeList){
            if(employee.getId() == id){
                employeeRemove = employee;
                break;
            }
        }
        if(employeeRemove != null){
            employeeList.remove(employeeRemove);
        }
    }

    public void displayEmployee(){
        for (Employee employee: employeeList){
            System.out.println(employee);
        }
    }
}
public class Main {

    public static void main(String[] args) {
        PayroleSystem payroleSystem = new PayroleSystem();
        FullTimeEmployee emp1 = new FullTimeEmployee("Harsh", 1, 5783909);
        PartTimeEmpoyee emp2 = new PartTimeEmpoyee("yash",12,24, 23.4);

        payroleSystem.addEmployee(emp1);
        payroleSystem.addEmployee(emp2);
        System.out.println("Initial Employee Details");
        payroleSystem.displayEmployee();
        System.out.println("Remove Employee");
        payroleSystem.RemoveEmployee(1);
        System.out.println("Remaining Employee Details: ");
        payroleSystem.displayEmployee();


    }
}
