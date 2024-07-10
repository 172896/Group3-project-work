#include <iostream>
#include <vector>
#include <string>
#include <fstream>

struct Student {
    std::string firstname;
    std::string surname;
    std::string gender;
    int age{};
    int group{};
    std::vector<std::string> activities;
};

struct Activity {
    std::string name;
    int max_capacity;
    std::vector<Student> members;
};

std::vector<Student> students;
std::vector<Activity> sports = {{"Rugby", 20}, {"Athletics", 20}, {"Swimming", 20}, {"Soccer", 20}};
std::vector<Activity> clubs = {{"Journalism Club", 60}, {"Red Cross Society", 60}, {"AISEC", 60}, {"Business Club", 60}, {"Computer Science Club", 60}};
void viewStudents() {
    for (const auto& student : students) {
        std::cout << "Name: " << student.firstname << " " << student.surname << ", Gender: " << student.gender << ", Age: " << student.age << ", Group: " << student.group << "\n";
        std::cout << "Activities: ";
        for (const auto& activity : student.activities) {
            std::cout << activity << " ";
        }
        std::cout << "\n";
    }
}

void viewActivities(const std::vector<Activity>& activities) {
    for (const auto& activity : activities) {
        std::cout << "Activity: " << activity.name << ", Capacity: " << activity.members.size() << "/" << activity.max_capacity << "\n";
    }
}

void saveToFile() {
    std::ofstream file("students.csv");
    file << "Firstname,Surname,Gender,Age,Group,Activities\n";
    for (const auto& student : students) {
        file << student.firstname << "," << student.surname << "," << student.gender << "," << student.age << "," << student.group << ",";
        for (const auto& activity : student.activities) {
            file << activity << " ";
        }
        file << "\n";
    }
    file.close();
    std::cout << "Data saved to students.csv\n";
}
