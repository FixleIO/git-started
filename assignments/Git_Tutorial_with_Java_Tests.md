# Git Tutorial: Adding Unit Tests to the Java To-Do List App

In this guide, we'll enhance the To-Do List app from the [previous tutorial](Git_Tutorial_with_Java_App.md) by adding unit tests using JUnit 5. Unit tests help verify that your code works as expected, and you'll practice Git by committing and pushing these changes. This is designed for first-year college students, so we'll keep the tests simple, focusing on the core functionality of adding and marking tasks as done.

## Prerequisites
- You've completed the [previous tutorial](Git_Tutorial_with_Java_App.md) and have the `java-todo-app` repository with `TodoApp.java`.
- You have Java and Git installed (see [GitHub_Setup_Instructions.md](./GitHub_Setup_Instructions.md)).
- Basic understanding of Java classes and methods.
- A code editor (e.g., VS Code, IntelliJ IDEA).

## Step 1: Set Up JUnit 5
To write unit tests, we need JUnit 5. For simplicity, we'll manually download the JUnit jars and use them in our project. This avoids complex build tools like Maven or Gradle, which might be overwhelming for beginners.

1. Create a `lib` folder in your `java-todo-app` repository:
   ```
   mkdir lib
   ```

2. Download the following JUnit 5 jars (as of September 2025, use the latest stable versions):
   - [JUnit Platform Console Standalone](https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.10.2/junit-platform-console-standalone-1.10.2.jar) (or check for newer versions at [Maven Central](https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/)).
   - Save it in the `lib` folder as `junit-platform-console-standalone.jar`.

3. Add the `lib` folder to Git (we'll commit it later to share dependencies):
   ```
   git add lib
   ```

## Step 2: Refactor TodoApp for Testability
To make testing easier, we'll separate the task management logic from the user interface. We'll create a `TaskManager` class to handle tasks and update `TodoApp` to use it.

1. Create a new file `TaskManager.java` in the `java-todo-app` folder:

   ```java
   import java.util.ArrayList;

   public class TaskManager {
       private ArrayList<String> tasks;

       public TaskManager() {
           tasks = new ArrayList<>();
       }

       public void addTask(String task) {
           tasks.add(task);
       }

       public ArrayList<String> getTasks() {
           return tasks;
       }

       public boolean markTaskDone(int index) {
           if (index >= 0 && index < tasks.size()) {
               String task = tasks.get(index);
               tasks.set(index, task + " [DONE]");
               return true;
           }
           return false;
       }

       public int getTaskCount() {
           return tasks.size();
       }
   }
   ```

2. Update `TodoApp.java` to use `TaskManager`:

   ```java
   import java.util.Scanner;

   public class TodoApp {
       public static void main(String[] args) {
           TaskManager taskManager = new TaskManager();
           Scanner scanner = new Scanner(System.in);
           System.out.println("Welcome to your To-Do List App!");

           boolean running = true;
           while (running) {
               System.out.println("\nOptions: 1. Add task  2. View tasks  3. Mark task as done  4. Exit");
               System.out.print("Choose an option: ");
               int choice = scanner.nextInt();
               scanner.nextLine(); // Consume newline

               if (choice == 1) {
                   System.out.print("Enter task: ");
                   String task = scanner.nextLine();
                   taskManager.addTask(task);
                   System.out.println("Task added!");
               } else if (choice == 2) {
                   if (taskManager.getTaskCount() == 0) {
                       System.out.println("No tasks yet.");
                   } else {
                       int i = 1;
                       for (String task : taskManager.getTasks()) {
                           System.out.println(i + ". " + task);
                           i++;
                       }
                   }
               } else if (choice == 3) {
                   System.out.print("Enter task number to mark as done: ");
                   int index = scanner.nextInt() - 1;
                   scanner.nextLine(); // Consume newline
                   if (taskManager.markTaskDone(index)) {
                       System.out.println("Task marked as done!");
                   } else {
                       System.out.println("Invalid task number.");
                   }
               } else if (choice == 4) {
                   running = false;
               } else {
                   System.out.println("Invalid choice.");
               }
           }
           System.out.println("Goodbye!");
       }
   }
   ```

3. Compile and run to verify:
   ```
   javac TodoApp.java TaskManager.java
   java TodoApp
   ```
   The app should work as before, but the logic is now in `TaskManager`.

4. Commit these changes:
   - Stage: `git add TaskManager.java TodoApp.java`
   - Commit: `git commit -m "Refactor: Add TaskManager class for better testability"`
   - Push: `git push origin main`

## Step 3: Write Unit Tests
Now, let's create tests for `TaskManager`. We'll test adding tasks and marking them as done.

1. Create a new file `TaskManagerTest.java` in the `java-todo-app` folder:

   ```java
   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   public class TaskManagerTest {

       @Test
       public void testAddTask() {
           TaskManager manager = new TaskManager();
           manager.addTask("Learn Git");
           assertEquals(1, manager.getTaskCount(), "Task count should be 1 after adding a task");
           assertEquals("Learn Git", manager.getTasks().get(0), "Task should be added correctly");
       }

       @Test
       public void testMarkTaskDone() {
           TaskManager manager = new TaskManager();
           manager.addTask("Learn Java");
           boolean result = manager.markTaskDone(0);
           assertTrue(result, "Marking valid task should return true");
           assertEquals("Learn Java [DONE]", manager.getTasks().get(0), "Task should be marked as done");
       }

       @Test
       public void testMarkTaskDoneInvalidIndex() {
           TaskManager manager = new TaskManager();
           boolean result = manager.markTaskDone(0);
           assertFalse(result, "Marking invalid task index should return false");
       }
   }
   ```

2. Compile the test file (include the JUnit jar):
   ```
   javac -cp .:lib/junit-platform-console-standalone.jar TaskManagerTest.java TaskManager.java
   ```

3. Run the tests:
   ```
   java -jar lib/junit-platform-console-standalone.jar --class-path . --scan-classpath
   ```
   You should see output indicating all tests passed (3 tests in this case).

4. Commit the test file:
   - Stage: `git add TaskManagerTest.java lib/junit-platform-console-standalone.jar`
   - Commit: `git commit -m "Add JUnit 5 tests for TaskManager class"`
   - Push: `git push origin main`

## Step 4: Add a Test for Empty Task List
Let's add one more test to check the empty task list case.

1. Update `TaskManagerTest.java` by adding a new test method:

   ```java
   import org.junit.jupiter.api.Test;
   import static org.junit.jupiter.api.Assertions.*;

   public class TaskManagerTest {

       @Test
       public void testAddTask() {
           TaskManager manager = new TaskManager();
           manager.addTask("Learn Git");
           assertEquals(1, manager.getTaskCount(), "Task count should be 1 after adding a task");
           assertEquals("Learn Git", manager.getTasks().get(0), "Task should be added correctly");
       }

       @Test
       public void testMarkTaskDone() {
           TaskManager manager = new TaskManager();
           manager.addTask("Learn Java");
           boolean result = manager.markTaskDone(0);
           assertTrue(result, "Marking valid task should return true");
           assertEquals("Learn Java [DONE]", manager.getTasks().get(0), "Task should be marked as done");
       }

       @Test
       public void testMarkTaskDoneInvalidIndex() {
           TaskManager manager = new TaskManager();
           boolean result = manager.markTaskDone(0);
           assertFalse(result, "Marking invalid task index should return false");
       }

       @Test
       public void testEmptyTaskList() {
           TaskManager manager = new TaskManager();
           assertEquals(0, manager.getTaskCount(), "New TaskManager should have zero tasks");
       }
   }
   ```

2. Compile and run tests again:
   ```
   javac -cp .:lib/junit-platform-console-standalone.jar TaskManagerTest.java TaskManager.java
   java -jar lib/junit-platform-console-standalone.jar --class-path . --scan-classpath
   ```
   Now, 4 tests should pass.

3. Commit the change:
   - Stage: `git add TaskManagerTest.java`
   - Commit: `git commit -m "Add test for empty task list"`
   - Push: `git push origin main`

## Step 5: Update README
Add a note about the tests to your `README.md` to document the new feature.

1. Edit `README.md` (append to the "Repository Contents" section or add a new section):

   ```markdown
   ## Repository Contents
   ...
   | [TaskManagerTest.java](./TaskManagerTest.java) | Unit tests for the TaskManager class using JUnit 5. |

   ## Running Unit Tests
   To run the unit tests, ensure you have the JUnit 5 jar in the `lib` folder. Then:
   1. Compile: `javac -cp .:lib/junit-platform-console-standalone.jar TaskManagerTest.java TaskManager.java`
   2. Run: `java -jar lib/junit-platform-console-standalone.jar --class-path . --scan-classpath`
   ```

2. Commit and push:
   - Stage: `git add README.md`
   - Commit: `git commit -m "Update README with unit test instructions"`
   - Push: `git push origin main`

## Why This Isn't Complicated
- **JUnit 5 is beginner-friendly**: The `@Test` annotation and `assert` methods are easy to understand.
- **Simple test cases**: We focused on core functionality (adding tasks, marking tasks done, handling edge cases).
- **Manual jar setup**: Avoids complex build tools, keeping it accessible for first-year students.
- **Git integration**: Each step reinforces Git commits and pushes, mirroring real-world workflows.

## What's Next?
- Try adding more tests, like checking multiple tasks or edge cases.
- Experiment with a test that fails to see how JUnit reports errors.
- Explore [GitHub_Student_Workflow.md](./GitHub_Student_Workflow.md) to collaborate on tests with others.
- For advanced students, consider introducing Maven or Gradle for dependency management (but keep it optional).

Check your GitHub repo to see all your commits! You're now testing like a pro. 🎉