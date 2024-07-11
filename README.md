#include <iostream>
#include <vector>
#include <string>
#include <fstream>

struct Student { //Group related information about the student
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
void addStudent() {
    Student student;
    std::cout << "Enter first name: ";
    std::cin >> student.firstname;
    std::cout << "Enter surname: ";
    std::cin >> student.surname;
    std::cout << "Enter gender (Male/Female): ";
    std::cin >> student.gender;
    std::cout << "Enter age: ";
    std::cin >> student.age;
    std::cout << "Enter group (1-3): ";
    std::cin >> student.group;

    int choice;
    do {
        std::cout << "Choose activity type: 1. Sport 2. Club/Society 3. Done: ";
        std::cin >> choice;

        if (choice == 1) {
            std::cout << "Choose sport: ";
            for (size_t i = 0; i < sports.size(); ++i) {
                std::cout << i+1 << ". " << sports[i].name << " (" << sports[i].members.size() << "/" << sports[i].max_capacity << ")\n";
            }
            int sport_choice;
            std::cin >> sport_choice;
            if (sport_choice >= 1 && sport_choice <= sports.size()) {
                if (sports[sport_choice-1].members.size() < sports[sport_choice-1].max_capacity) {
                    student.activities.push_back(sports[sport_choice-1].name);
                    sports[sport_choice-1].members.push_back(student);
                } else {
                    std::cout << "Sport is at full capacity.\n";
                }
            }
        } else if (choice == 2) {
            std::cout << "Choose club/society: ";
            for (size_t i = 0; i < clubs.size(); ++i) {
                std::cout << i+1 << ". " << clubs[i].name << " (" << clubs[i].members.size() << "/" << clubs[i].max_capacity << ")\n";
            }
            int club_choice;
            std::cin >> club_choice;
            if (club_choice >= 1 && club_choice <= clubs.size()) {
                if (clubs[club_choice-1].members.size() < clubs[club_choice-1].max_capacity) {
                    student.activities.push_back(clubs[club_choice-1].name);
                    clubs[club_choice-1].members.push_back(student);
                } else {
                    std::cout << "Club/Society is at full capacity.\n";
                }
            }
        }
    } while (choice != 3);

    students.push_back(student);
}
    

void viewStudents() { //Add a function called veiw students .
    for (const auto& student : students) {
        std::cout << "Name: " << student.firstname << " " << student.surname << ", Gender: " << student.gender << ", Age: " << student.age << ", Group: " << student.group << "\n";
        std::cout << "Activities: ";
        for (const auto& activity : student.activities) {
            std::cout << activity << " ";
        }
        std::cout << "\n";
    }
}

void viewActivities(const std::vector<Activity>& activities) { //add a function called activities
    for (const auto& activity : activities) {
        std::cout << "Activity: " << activity.name << ", Capacity: " << activity.members.size() << "/" << activity.max_capacity << "\n";
    }
}
void viewGroupedStudents() {
    for (int i = 1; i <= 3; i++) {
        std::cout<< "Group "<< i <<":" << "endl";
        for (auto& s : students) {
            if (s.group == i) {
                std::cout << s.firstname << " " << s.surname;
                for (auto& activity : s.activities) {
                    std::cout<< "\t" << activity;
                }
                std::cout<<"endl";
            }
        }
    }
}
void saveToFile() {//add a function called saveToFile
        std::ofstream file("students.csv", std::ios::app);
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

int main() {
    int choice;
    do {
        std::cout << "Menu:\n";
        std::cout << "1. Add Student\n";
        std::cout << "2. View Students\n";
        std::cout << "3. View Clubs/Societies\n";
        std::cout << "4. View Sports\n";
        std::cout << "5. View grouped students\n";
        std::cout << "6. Save all Files\n ";
        std::cout << "7. Exit\n";
        std::cin >> choice;

        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                viewStudents();
                break;
            
                case 3:
                viewActivities(clubs);
                break;
            case 4:
                viewActivities(sports);
                break;
           case 5:
                viewGroupedStudents();
            break;
            case 6:
                saveToFile();
            break;
            case 7:
                std::cout << "Exiting...\n";
            break;
            default:
                std::cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 6);

    return 0;
}
