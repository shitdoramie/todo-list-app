# todo-list-app
A simple Todo List App to help you stay organized and productive
// todo_list.c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_TASKS 100
#define MAX_TASK_LENGTH 50

typedef struct {
    char task[MAX_TASK_LENGTH];
    int completed;
} Task;

Task tasks[MAX_TASKS];
int task_count = 0;

void add_task() {
    if (task_count < MAX_TASKS) {
        printf("Enter task: ");
        fgets(tasks[task_count].task, MAX_TASK_LENGTH, stdin);
        tasks[task_count].task[strcspn(tasks[task_count].task, "\n")] = 0;
        tasks[task_count].completed = 0;
        task_count++;
        printf("Task added!\n");
    } else {
        printf("Task limit reached!\n");
    }
}

void view_tasks() {
    printf("\nTasks:\n");
    for (int i = 0; i < task_count; i++) {
        printf("%d. %s %s\n", i + 1, tasks[i].completed ? "[Completed] " : "", tasks[i].task);
    }
}

void delete_task() {
    int task_number;
    printf("Enter task number to delete: ");
    scanf("%d", &task_number);
    if (task_number > 0 && task_number <= task_count) {
        for (int i = task_number - 1; i < task_count - 1; i++) {
            tasks[i] = tasks[i + 1];
        }
        task_count--;
        printf("Task deleted!\n");
    } else {
        printf("Invalid task number.\n");
    }
}

void mark_completed() {
    int task_number;
    printf("Enter task number to mark completed: ");
    scanf("%d", &task_number);
    if (task_number > 0 && task_number <= task_count) {
        tasks[task_number - 1].completed = 1;
        printf("Task marked completed!\n");
    } else {
        printf("Invalid task number.\n");
    }
}

int main() {
    while (1) {
        printf("\nTodo List App\n");
        printf("1. Add Task\n");
        printf("2. View Tasks\n");
        printf("3. Delete Task\n");
        printf("4. Mark Completed\n");
        printf("5. Quit\n");

        int choice;
        printf("Choose an option: ");
        scanf("%d", &choice);
        getchar(); // Consume newline character

        switch (choice) {
            case 1:
                add_task();
                break;
            case 2:
                view_tasks();
                break;
            case 3:
                delete_task();
                break;
            case 4:
                mark_completed();
                break;
            case 5:
                return 0;
            default:
                printf("Invalid option. Please choose again.\n");
        }
    }
