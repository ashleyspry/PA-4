/*/ 
Author:             Ashley Spry
BannerID:           001397004
Course:             CS 181
Assignment:         PA4
Date Assigned:      Monday, March 18, 2024
Date/Time Due:      Saturday, March 30, 2024 -- 11:55 pm
Description:        This program will exercise Object-
                        Oriented concepts with C++.
Certification of Authenticity:
        I certify that this assignment is entirely my own work.
/*/
#include <iostream>
#include <iomanip>
#include <string>
#include "Employee.h"
#include "Employee.cpp"

using namespace std;

// Manager class derived from Employee
class Manager : public Employee 
{
    private:
        double bonus;

    public:
        // Constructor
        Manager(string theName, double theWage, double theHours, double theBonus) : Employee(theName, theWage, theHours), bonus(theBonus) 
        {}

        // Calculate pay for manager (including bonus)
        double calcPay() const 
        {
            return Employee::calcPay() + bonus;
        }
};

int main() 
{
    int numManagers;
    // Variables to keep track of highest paid manager and total pay
    double highestPay = 0.0;
    double totalPay = 0.0;
    string highestPaidManagerName;

    cout << "This program calculates the highest paid manager and average pay." << endl;

    cout << "Enter number of managers: ";
    cin >> numManagers;
    cin.ignore(); // consume the newline character left in the buffer

    // Array of pointers to Manager objects
    Manager* managers[numManagers];

    // Input data for each manager
    for (int i = 0; i < numManagers; ++i) 
    {
        string name;
        double wage, hours, bonus;

        cout << "Enter manager " << i << " name: ";
        getline(cin, name);
        cout << "Enter manager " << i << " hourly wage: ";
        cin >> wage;
        cout << "Enter manager " << i << " hours worked: ";
        cin >> hours;
        cout << "Enter manager " << i << " bonus: ";
        cin >> bonus;
        cin.ignore(); // consume the newline character left in the buffer

        // Dynamically create Manager object
        managers[i] = new Manager(name, wage, hours, bonus);

        // Update total pay
        totalPay += managers[i]->calcPay();

        // Check if this manager has the highest pay
        if (managers[i]->calcPay() > highestPay) 
        {
            highestPay = managers[i]->calcPay();
            highestPaidManagerName = name;
        }
    }

    // Calculate average pay
    double averagePay = totalPay / numManagers;

    // Output results
    cout << fixed << setprecision(2);
    cout << "Highest paid manager is " << highestPaidManagerName << " who is paid $" << highestPay << endl;
    cout << "Average pay is $" << averagePay << endl;

    // Deallocate memory for Manager objects
    for (int i = 0; i < numManagers; ++i) 
    {
        delete managers[i];
    }

    return 0;
}
