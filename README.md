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
