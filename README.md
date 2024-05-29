#include <iostream>
#include <fstream>
#include <string>

void displayMenu() {
    std::cout << "Text File Manager\n";
    std::cout << "1. Create a new file\n";
    std::cout << "2. Read a file\n";
    std::cout << "3. Append to a file\n";
    std::cout << "4. Exit\n";
    std::cout << "Choose an option: ";
}

void createFile(const std::string &filename) {
    std::ofstream file(filename);
    if (file.is_open()) {
        std::string content;
        std::cout << "Enter content (type 'END' to finish):\n";
        while (true) {
            std::getline(std::cin, content);
            if (content == "END") break;
            file << content << std::endl;
        }
        file.close();
        std::cout << "File created successfully.\n";
    } else {
        std::cerr << "Unable to create file.\n";
    }
}

void readFile(const std::string &filename) {
    std::ifstream file(filename);
    if (file.is_open()) {
        std::string line;
        std::cout << "File content:\n";
        while (std::getline(file, line)) {
            std::cout << line << std::endl;
        }
        file.close();
    } else {
        std::cerr << "Unable to open file.\n";
    }
}

void appendToFile(const std::string &filename) {
    std::ofstream file(filename, std::ios::app);
    if (file.is_open()) {
        std::string content;
        std::cout << "Enter content to append (type 'END' to finish):\n";
        while (true) {
            std::getline(std::cin, content);
            if (content == "END") break;
            file << content << std::endl;
        }
        file.close();
        std::cout << "Content appended successfully.\n";
    } else {
        std::cerr << "Unable to open file.\n";
    }
}

int main() {
    int choice;
    std::string filename;

    while (true) {
        displayMenu();
        std::cin >> choice;
        std::cin.ignore(); // Ignore the newline character after the integer input

        switch (choice) {
            case 1:
                std::cout << "Enter filename to create: ";
                std::getline(std::cin, filename);
                createFile(filename);
                break;
            case 2:
                std::cout << "Enter filename to read: ";
                std::getline(std::cin, filename);
                readFile(filename);
                break;
            case 3:
                std::cout << "Enter filename to append to: ";
                std::getline(std::cin, filename);
                appendToFile(filename);
                break;
            case 4:
                std::cout << "Exiting program.\n";
                return 0;
            default:
                std::cout << "Invalid choice. Please try again.\n";
        }
    }
    return 0;
}
