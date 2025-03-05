# LabTest_COMP2080

// Employee class as per the given UML
public class Employee {
    public String employeeCode;
    public String name;
    public String position;
    public String phone;
    public int officeNum;

    // Constructor
    public Employee(String employeeCode, String name, String position, String phone, int officeNum) {
        this.employeeCode = employeeCode;
        this.name = name;
        this.position = position;
        this.phone = phone;
        this.officeNum = officeNum;
    }
}

// OrderedObjects class to store and manage Employee objects
class OrderedObjects {
    private Employee[] employees; // Array to store Employee objects
    private int size; // Tracks the number of stored objects
    private static final int MAX_SIZE = 200; // Maximum allowed objects

    // Constructor
    public OrderedObjects() {
        employees = new Employee[MAX_SIZE];
        size = 0;
    }

    // Method to add an Employee object
    public boolean addObject(String employeeCode, String name, String position, String phone, int officeNum) {
        // Check if name already exists
        if (employeeExists(name) || size >= MAX_SIZE) {
            return false; // Employee with the same name exists OR array is full
        }

        // Add the new Employee object
        employees[size] = new Employee(employeeCode, name, position, phone, officeNum);
        size++;

        // Sort the array using selection sort
        selectionSort();
        return true; // Successfully added
    }

    // Selection Sort to sort employees by name
    private void selectionSort() {
        for (int i = 0; i < size - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < size; j++) {
                if (employees[j].name.compareTo(employees[minIndex].name) < 0) {
                    minIndex = j;
                }
            }
            // Swap
            Employee temp = employees[i];
            employees[i] = employees[minIndex];
            employees[minIndex] = temp;
        }
    }

    // Private binary search method
    private int binarySearch(String name) {
        int left = 0, right = size - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int cmp = employees[mid].name.compareTo(name);
            if (cmp == 0) {
                return mid; // Found
            } else if (cmp < 0) {
                left = mid + 1; // Search right
            } else {
                right = mid - 1; // Search left
            }
        }
        return -1; // Not found
    }

    // Method to check if an employee exists
    public boolean employeeExists(String name) {
        return binarySearch(name) != -1;
    }
}
