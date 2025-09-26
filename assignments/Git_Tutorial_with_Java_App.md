# Git Tutorial: Building a Simple Java To-Do List App

This guide will walk you through creating a simple command-line To-Do List application in Java while learning Git basics. You'll make incremental changes to the code, commit them regularly, and push to GitHub to save your progress on the server. This is designed for first-year college students, so we'll keep the Java code straightforward but build it step by step to add features.

## Prerequisites
- You've set up your GitHub account and Git on your local machine. Refer to [GitHub_Setup_Instructions.md](./GitHub_Setup_Instructions.md) if needed.
- You understand basic Git areas (working directory, staging, repository). See [Git_Areas.md](./Git_Areas.md).
- Basic Java knowledge: classes, methods, loops, and input/output.
- A code editor like VS Code or IntelliJ IDEA Community Edition.
- Java Development Kit (JDK) installed (version 8 or higher).

We'll use a student workflow for Git. For more on that, check [GitHub_Student_Workflow.md](./GitHub_Student_Workflow.md).

## Step 1: Set Up Your Repository
1. Go to GitHub and create a new repository called `java-todo-app`. Make it public or private as you prefer, and initialize it with a README.md file.
2. On your local machine, open a terminal or command prompt.
3. Clone the repository:
   ```
   git clone https://github.com/your-username/java-todo-app.git
   ```
4. Navigate into the folder:
   ```
   cd java-todo-app
   ```

This sets up your local repo synced with GitHub (the "server").

## Step 2: Create the Initial Java File
We'll start with a basic "Hello World" in Java to get the structure going.

1. Create a new file called `TodoApp.java` in the `java-todo-app` folder.
2. Add the following code to `TodoApp.java`:

   ```java
   import java.util.Scanner;

   public class TodoApp {
       public static void main(String[] args) {
           System.out.println("Welcome to your To-Do List App!");
           // We'll add more features here soon.
       }
   }
   ```

3. Compile and run it to test:
   ```
   javac TodoApp.java
   java TodoApp
   ```
   You should see: "Welcome to your To-Do List App!"

4. Now, use Git to save this change:
   - Stage the file: `git add TodoApp.java`
   - Commit: `git commit -m "Initial commit: Add basic TodoApp class with welcome message"`
   - Push to GitHub: `git push origin main` (or `master`, depending on your branch name)

Great! Your code is now saved on the server. Check GitHub to see the new file.

## Step 3: Add a Task List Structure
Next, we'll add an ArrayList to store tasks. This introduces imports and basic data structures.

1. Update `TodoApp.java` by adding an import and initializing a list:

   ```java
   import java.util.ArrayList;
   import java.util.Scanner;

   public class TodoApp {
       public static void main(String[] args) {
           ArrayList<String> tasks = new ArrayList<>();
           System.out.println("Welcome to your To-Do List App!");
           // Add a sample task for testing
           tasks.add("Learn Git");
           System.out.println("Current tasks: " + tasks);
       }
   }
   ```

2. Compile and run:
   ```
   javac TodoApp.java
   java TodoApp
   ```
   Output should show the welcome and the sample task.

3. Git steps:
   - Stage: `git add TodoApp.java`
   - Commit: `git commit -m "Add ArrayList to store tasks and a sample task"`
   - Push: `git push origin main`

Your progress is saved! Committing regularly like this helps track changes and recover if something goes wrong.

## Step 4: Add User Input for Adding Tasks
Now, let's make it interactive. We'll use a Scanner for user input to add tasks.

1. Modify `TodoApp.java` to include a loop for adding tasks:

   ```java
   import java.util.ArrayList;
   import java.util.Scanner;

   public class TodoApp {
       public static void main(String[] args) {
           ArrayList<String> tasks = new ArrayList<>();
           Scanner scanner = new Scanner(System.in);
           System.out.println("Welcome to your To-Do List App!");

           boolean running = true;
           while (running) {
               System.out.println("\nOptions: 1. Add task  2. View tasks  3. Exit");
               System.out.print("Choose an option: ");
               int choice = scanner.nextInt();
               scanner.nextLine(); // Consume newline

               if (choice == 1) {
                   System.out.print("Enter task: ");
                   String task = scanner.nextLine();
                   tasks.add(task);
                   System.out.println("Task added!");
               } else if (choice == 2) {
                   System.out.println("Current tasks: " + tasks);
               } else if (choice == 3) {
                   running = false;
               } else {
                   System.out.println("Invalid choice.");
               }
           }
           System.out.println("Goodbye!");
       }
   }
   ```

2. Compile and run. Try adding and viewing tasks.

3. Git steps:
   - Stage: `git add TodoApp.java`
   - Commit: `git commit -m "Add user input loop for adding and viewing tasks"`
   - Push: `git push origin main`

You're building features incrementally. Each commit represents a small, working change.

## Step 5: Add Task Completion Feature
Let's add the ability to mark tasks as done. We'll modify tasks to include a status (e.g., append "[DONE]" to completed tasks).

1. Update the code in `TodoApp.java` to include a new option:

   ```java
   import java.util.ArrayList;
   import java.util.Scanner;

   public class TodoApp {
       public static void main(String[] args) {
           ArrayList<String> tasks = new ArrayList<>();
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
                   tasks.add(task);
                   System.out.println("Task added!");
               } else if (choice == 2) {
                   if (tasks.isEmpty()) {
                       System.out.println("No tasks yet.");
                   } else {
                       for (int i = 0; i < tasks.size(); i++) {
                           System.out.println((i + 1) + ". " + tasks.get(i));
                       }
                   }
               } else if (choice == 3) {
                   System.out.print("Enter task number to mark as done: ");
                   int index = scanner.nextInt() - 1;
                   scanner.nextLine(); // Consume newline
                   if (index >= 0 && index < tasks.size()) {
                       String task = tasks.get(index);
                       tasks.set(index, task + " [DONE]");
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

2. Compile and run. Add tasks, view them numbered, and mark one as done.

3. Git steps:
   - Stage: `git add TodoApp.java`
   - Commit: `git commit -m "Add feature to mark tasks as done and improve view with numbering"`
   - Push: `git push origin main`

## Step 6: Final Touches and Review
- Run the app again to ensure everything works.
- Use `git log` to see your commit history.
- On GitHub, browse your repo to view the changes over time.

This app is now a functional To-Do List! You've learned to use Git for tracking changes with commits and pushes. For practice, try adding more features like deleting tasks, then commit and push those too.

If you want to collaborate, fork someone else's repo and submit a pull request—see [GitHub_Student_Workflow.md](./GitHub_Student_Workflow.md).

Happy coding and versioning! 🚀