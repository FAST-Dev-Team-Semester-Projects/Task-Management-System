# Task Management System

Welcome to the Task Management System! This application provides a simple and effective way to manage your tasks. You can create, view, edit, and delete tasks through a user-friendly interface. The program utilizes file storage to maintain task information, offering options to sort and filter tasks based on different criteria.

## Project Background

This Task Management System was developed as part of a second-semester project for the course "Object Oriented Programming" at FAST NUCES Karachi. The project aims to apply essential object-oriented programming concepts and techniques learned during the course.

## Features

- **Task Management**: Easily create, view, edit, and delete tasks.
- **Sorting and Filtering**: View tasks sorted by date, priority, or category.
- **Error Handling**: Robust input validation to prevent incorrect entries.
- **File Storage**: Save tasks to a file and retrieve them upon startup.

## How to Use

1. **Main Menu**:
   - **Create Task**: Add a new task with details such as title, priority, date, etc.
   - **View Tasks**: Display tasks sorted by date, priority, or category.
   - **Edit Task**: Update task details, such as priority or status.
   - **Delete Task**: Remove a task by its ID.
   - **Exit Program**: Close the application safely.

2. **Controls**:
   - Enter numbers to select menu options.
   - Input task details when prompted.

3. **Objective**: Efficiently manage tasks to boost productivity and stay organized.

4. **Error Handling**: The system will alert you if an invalid input is detected, allowing for correction.

## Installation

To compile and run the application, follow these steps:

1. **Clone the repository**:

    ```bash
    git clone https://github.com/SHaiderM16/Task-Management-System.git
    ```

2. **Navigate to the project directory**:

    ```bash
    cd Task-Management-System
    ```

3. **Compile the code**:

    ```bash
    g++ -o taskmanager src/main.cpp src/Task.cpp src/TaskManager.cpp
    ```

4. **Run the program**:

    ```bash
    ./taskmanager
    ```

## Code Overview

### Classes and Functions

The program relies on two main classes: `Task` and `TaskManager`.

**`Task` Class**

This class represents individual tasks and includes attributes such as task ID, title, description, deadline, priority, status, category, and label.

**`TaskManager` Class**

The `TaskManager` class handles various task-related operations, providing functionalities for creating, viewing, editing, and deleting tasks. It interfaces with a file system to persist task data.

- **Key Functions:**

  - **`createTask()`**: Prompts the user to enter details for a new task and saves the task to the designated file.
  - **`viewTask(int sortingMethod)`**: Displays tasks based on the selected sorting criteria:
    - `1` for sorting by date
    - `2` for sorting by priority
    - `3` for sorting by category
  - **`editTaskPriorityAndStatus(int taskId)`**: Updates the priority and status of a task specified by its ID.
  - **`deleteTask(const std::string &filename, int taskID)`**: Removes a task identified by its ID from the specified file.

### Example Code Snippets

Here's a quick look at some core functions used in the program. For the full code, please check the [source files](https://github.com/SHaiderM16/Task-Management-System/tree/main/src) in the repository.

#### Create Task Function

```cpp
void TaskManager::createTask() 
{
    Task newTask;
    cin >> newTask; // Utilize the operator>> to input task details

    // Load existing tasks from the file
    ifstream infile("project.txt");
    if (infile.is_open())
    {
        string line;
        while (getline(infile, line))
        {
            stringstream ss(line);
            string idStr;

            getline(ss, idStr, ',');
            int id = stoi(idStr);

            // Skip tasks with the same ID as the one being added
            if (id == newTask.getTaskID())
            {
                cout << "Task with the same ID already exists! Please choose a different ID." << endl;
                infile.close();
                return;
            }
        }
        infile.close();
    }

    // Add the task to the task manager
    tasks.push_back(newTask);

    cout << "Task created successfully!" << endl;

    // Save the task to txt file
    saveTaskToFile("project.txt", newTask.getTaskID());
}
```

#### View Task Function

```cpp
void TaskManager::viewTask(int sortingMethod)
{
    // Check the sorting method provided by the user
    if (sortingMethod == 1)
    {
        // Call viewTasksByDate function if '1' is passed
        viewTasksByDate();
    }
    else if (sortingMethod == 2)
    {
        // Call viewTasksByPriority function if '2' is passed
        viewTasksByPriority();
    }
    else if (sortingMethod == 3)
    {
        // Call viewTasksByCategory function if '3' is passed
        viewTasksByCategory();
    }
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/SHaiderM16/Task-Management-System/blob/main/LICENSE) file for details.

## Future Improvements

We plan to enhance the Task Management System with the following updates:

- **Graphical User Interface (GUI)**: Adding a GUI will make the application more user-friendly and visually appealing. This will involve designing an intuitive interface for task management and interactions.
  
- **Enhanced Error Handling**: We aim to improve the robustness of the application by implementing more comprehensive error handling. This will include better validation of user inputs and more informative error messages to guide users effectively.

## Contact

For any questions or feedback, please contact:

- **Syed Haider Murtaza** at [haidermurtaza16@gmail.com](mailto:haidermurtaza16@gmail.com)
- **Muhammad Rayyan** at [imuhammadrayyan@gmail.com](mailto:imuhammadrayyan@gmail.com)
- **Mujtaba Kamran** at [mujtaba.kamran2004@gmail.com](mujtaba.kamran2004@gmail.com)
