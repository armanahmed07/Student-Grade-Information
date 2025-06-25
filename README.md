#include <stdio.h>
#include <string.h>

struct Student {
    char name[50];
    char id[20];
    char grade;
    float cgpa;
};

int main() {
    struct Student students[100];
    int n, i;
    char searchID[20];

    printf("Enter number of students: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++) {
        printf("\nStudent %d:\n", i + 1);
        printf("Enter Name: ");
        scanf(" %[^\n]", students[i].name);

        printf("Enter ID: ");
        scanf(" %s", students[i].id);

        printf("Enter Grade (A-F): ");
        scanf(" %c", &students[i].grade);

        do {
            printf("Enter CGPA (0.0 - 4.0): ");
            scanf("%f", &students[i].cgpa);
            if (students[i].cgpa < 0.0 || students[i].cgpa > 4.0)
                printf("Invalid CGPA! Try again.\n");
        } while (students[i].cgpa < 0.0 || students[i].cgpa > 4.0);
    }

    // Display all students
    printf("\n=== Student Information ===\n");
    printf("Name\tID\tGrade\tCGPA\n");
    for (i = 0; i < n; i++) {
        printf("%s\t%s\t%c\t%.2f\n", students[i].name, students[i].id, students[i].grade, students[i].cgpa);
    }

    // Search
    while (1) {
        printf("\nEnter ID to search (or 'exit'): ");
        scanf(" %s", searchID);
        if (strcmp(searchID, "exit") == 0)
            break;

        int found = 0;
        for (i = 0; i < n; i++) {
            if (strcmp(students[i].id, searchID) == 0) {
                printf("Found: %s, ID: %s, Grade: %c, CGPA: %.2f\n",
                       students[i].name, students[i].id, students[i].grade, students[i].cgpa);
                found = 1;
                break;
            }
        }

        if (!found)
            printf("ID not found!\n");
    }

    return 0;
}
