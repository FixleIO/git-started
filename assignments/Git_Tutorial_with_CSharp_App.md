# Git Tutorial: Building a Simple C# To-Do List App

This guide walks you through creating a simple command-line To-Do List application in C# while learning Git basics. You'll make incremental changes, commit regularly, and push to GitHub. Designed for first-year college students, the app uses basic C# concepts like classes, lists, and loops. We'll use the .NET SDK for building and testing—no Visual Studio required.

## Prerequisites
- GitHub account and Git installed ([GitHub_Setup_Instructions.md](./GitHub_Setup_Instructions.md)).
- .NET SDK 8 or later (download from [dotnet.microsoft.com](https://dotnet.microsoft.com/download)). Verify with `dotnet --version`.
- Basic C# knowledge: classes, methods, loops, console I/O.
- Code editor like VS Code with C# extension (optional but recommended).
- Follow [Git_Areas.md](./Git_Areas.md) and [GitHub_Student_Workflow.md](./GitHub_Student_Workflow.md) for Git concepts.

## Step 1: Set Up Your Repository and Project
1. Create a new GitHub repo called `csharp-todo-app`.
2. Clone it locally:
   ```
   git clone https://github.com/your-username/csharp-todo-app.git
   cd csharp-todo-app
   ```
3. Initialize a .NET console project:
   ```
   dotnet new console
   ```
   This creates `Program.cs`, `TodoApp.csproj`, and `.vscode/` (if in VS Code).
4. Update `Program.cs` with a basic welcome:
   ```csharp
   using System;

   namespace TodoApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Welcome to your To-Do List App!");
               // More features coming...
           }
       }
   }
   ```
5. Build and run:
   ```
   dotnet build
   dotnet run
   ```
   Output: "Welcome to your To-Do List App!"

6. Git commit:
   ```
   git add .
   git commit -m "Initial commit: Set up .NET console project with welcome message"
   git push origin main
   ```

Your project is now on GitHub!

## Step 2: Add Task List Structure
Add a List<string> for tasks.

1. Update `Program.cs`:
   ```csharp
   using System;
   using System.Collections.Generic;

   namespace TodoApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               List<string> tasks = new List<string>();
               Console.WriteLine("Welcome to your To-Do List App!");
               tasks.Add("Learn Git");
               Console.WriteLine($"Current tasks: {string.Join(", ", tasks)}");
           }
       }
   }
   ```
2. Build and run to verify.

3. Commit:
   ```
   git add Program.cs
   git commit -m "Add List<string> for tasks and sample task"
   git push origin main
   ```

## Step 3: Add User Input for Tasks
Make it interactive with a loop and Console.ReadLine.

1. Update `Program.cs`:
   ```csharp
   using System;
   using System.Collections.Generic;

   namespace TodoApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               List<string> tasks = new List<string>();
               Console.WriteLine("Welcome to your To-Do List App!");

               bool running = true;
               while (running)
               {
                   Console.WriteLine("\nOptions: 1. Add task  2. View tasks  3. Exit");
                   Console.Write("Choose: ");
                   string choice = Console.ReadLine();

                   if (choice == "1")
                   {
                       Console.Write("Enter task: ");
                       string task = Console.ReadLine();
                       tasks.Add(task);
                       Console.WriteLine("Task added!");
                   }
                   else if (choice == "2")
                   {
                       Console.WriteLine($"Current tasks: {string.Join(", ", tasks)}");
                   }
                   else if (choice == "3")
                   {
                       running = false;
                   }
                   else
                   {
                       Console.WriteLine("Invalid choice.");
                   }
               }
               Console.WriteLine("Goodbye!");
           }
       }
   }
   ```
2. Test by adding/viewing tasks.

3. Commit:
   ```
   git add Program.cs
   git commit -m "Add interactive loop for adding and viewing tasks"
   git push origin main
   ```

## Step 4: Add Task Completion
Mark tasks as done by appending "[DONE]". Number tasks for selection.

1. Update `Program.cs`:
   ```csharp
   using System;
   using System.Collections.Generic;

   namespace TodoApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               List<string> tasks = new List<string>();
               Console.WriteLine("Welcome to your To-Do List App!");

               bool running = true;
               while (running)
               {
                   Console.WriteLine("\nOptions: 1. Add task  2. View tasks  3. Mark done  4. Exit");
                   Console.Write("Choose: ");
                   string choice = Console.ReadLine();

                   if (choice == "1")
                   {
                       Console.Write("Enter task: ");
                       tasks.Add(Console.ReadLine());
                       Console.WriteLine("Task added!");
                   }
                   else if (choice == "2")
                   {
                       if (tasks.Count == 0) Console.WriteLine("No tasks.");
                       else
                       {
                           for (int i = 0; i < tasks.Count; i++)
                           {
                               Console.WriteLine($"{i + 1}. {tasks[i]}");
                           }
                       }
                   }
                   else if (choice == "3")
                   {
                       Console.Write("Task number: ");
                       if (int.TryParse(Console.ReadLine(), out int num) && num > 0 && num <= tasks.Count)
                       {
                           int index = num - 1;
                           tasks[index] += " [DONE]";
                           Console.WriteLine("Marked done!");
                       }
                       else
                       {
                           Console.WriteLine("Invalid number.");
                       }
                   }
                   else if (choice == "4") running = false;
                   else Console.WriteLine("Invalid.");
               }
               Console.WriteLine("Goodbye!");
           }
       }
   }
   ```
2. Test functionality.

3. Commit:
   ```
   git add Program.cs
   git commit -m "Add mark task as done with numbering"
   git push origin main
   ```

## Step 5: Refactor for Testability
Create `TaskManager.cs` to separate logic.

1. Add `TaskManager.cs`:
   ```csharp
   using System.Collections.Generic;

   namespace TodoApp
   {
       public class TaskManager
       {
           private List<string> tasks = new List<string>();

           public void AddTask(string task)
           {
               tasks.Add(task);
           }

           public List<string> GetTasks()
           {
               return tasks;
           }

           public bool MarkTaskDone(int index)
           {
               if (index >= 0 && index < tasks.Count)
               {
                   tasks[index] += " [DONE]";
                   return true;
               }
               return false;
           }

           public int TaskCount => tasks.Count;
       }
   }
   ```
2. Update `Program.cs` to use `TaskManager` (replace List with TaskManager instance, adjust methods accordingly—e.g., taskManager.AddTask(Console.ReadLine()); etc.).

   Full updated `Program.cs`:
   ```csharp
   using System;

   namespace TodoApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               TaskManager taskManager = new TaskManager();
               Console.WriteLine("Welcome to your To-Do List App!");

               bool running = true;
               while (running)
               {
                   Console.WriteLine("\nOptions: 1. Add task  2. View tasks  3. Mark done  4. Exit");
                   Console.Write("Choose: ");
                   string choice = Console.ReadLine();

                   if (choice == "1")
                   {
                       Console.Write("Enter task: ");
                       taskManager.AddTask(Console.ReadLine());
                       Console.WriteLine("Task added!");
                   }
                   else if (choice == "2")
                   {
                       var tasks = taskManager.GetTasks();
                       if (tasks.Count == 0) Console.WriteLine("No tasks.");
                       else
                       {
                           for (int i = 0; i < tasks.Count; i++)
                           {
                               Console.WriteLine($"{i + 1}. {tasks[i]}");
                           }
                       }
                   }
                   else if (choice == "3")
                   {
                       Console.Write("Task number: ");
                       if (int.TryParse(Console.ReadLine(), out int num) && num > 0 && num <= taskManager.TaskCount)
                       {
                           if (taskManager.MarkTaskDone(num - 1))
                               Console.WriteLine("Marked done!");
                           else
                               Console.WriteLine("Invalid.");
                       }
                       else
                       {
                           Console.WriteLine("Invalid number.");
                       }
                   }
                   else if (choice == "4") running = false;
                   else Console.WriteLine("Invalid.");
               }
               Console.WriteLine("Goodbye!");
           }
       }
   }
   ```
3. Build and run to confirm.

4. Commit:
   ```
   git add TaskManager.cs Program.cs
   git commit -m "Refactor: Extract TaskManager class for testability"
   git push origin main
   ```

## Step 6: Add Unit Tests with xUnit
Create a test project for `TaskManager`.

1. Add xUnit test project:
   ```
   dotnet new xunit -o TodoApp.Tests
   cd TodoApp.Tests
   dotnet add reference ../TodoApp.csproj
   cd ..
   dotnet add TodoApp.Tests package xunit
   dotnet add TodoApp.Tests package xunit.runner.visualstudio
   ```
   (Note: xunit is included by default in new xunit project; this ensures.)

2. Update `TodoApp.Tests/UnitTest1.cs` to `TaskManagerTests.cs`:
   ```csharp
   using Xunit;
   using TodoApp;

   namespace TodoApp.Tests
   {
       public class TaskManagerTests
       {
           [Fact]
           public void AddTask_IncreasesCount()
           {
               var manager = new TaskManager();
               manager.AddTask("Test");
               Assert.Equal(1, manager.TaskCount);
           }

           [Fact]
           public void MarkTaskDone_ValidIndex_Succeeds()
           {
               var manager = new TaskManager();
               manager.AddTask("Test");
               bool result = manager.MarkTaskDone(0);
               Assert.True(result);
               Assert.Contains("[DONE]", manager.GetTasks()[0]);
           }

           [Fact]
           public void MarkTaskDone_InvalidIndex_Fails()
           {
               var manager = new TaskManager();
               bool result = manager.MarkTaskDone(0);
               Assert.False(result);
           }

           [Fact]
           public void TaskCount_InitiallyZero()
           {
               var manager = new TaskManager();
               Assert.Equal(0, manager.TaskCount);
           }
       }
   }
   ```
3. Run tests:
   ```
   dotnet test
   ```
   All 4 tests should pass.

4. Commit the test project:
   ```
   git add TodoApp.Tests/
   git commit -m "Add xUnit test project for TaskManager"
   git push origin main
   ```

## Step 7: Update README
Add to your `README.md`:
```
## Running the App
dotnet run

## Running Tests
dotnet test
```

Commit:
```
git add README.md
git commit -m "Update README with run and test instructions"
git push origin main
```

## Why This Setup?
- **.NET CLI is simple**: No IDE needed; commands are straightforward.
- **xUnit is beginner-friendly**: Uses `[Fact]` for tests and `Assert` methods.
- **Project structure**: Encourages good practices; tests are separate.
- **Git integration**: Commits track progress.

## Next Steps
- Add more tests or features (e.g., delete tasks).
- Use `git log` to review history.
- Collaborate via forks/PRs ([GitHub_Student_Workflow.md](./GitHub_Student_Workflow.md)).

Check GitHub for your evolving repo! 🚀