# code-caluse
my intership projects
import tkinter as tk
from tkinter import messagebox

class ToDoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List App")
        self.root.geometry("400x500")
        
        self.tasks = []
        
         UI Components
        self.task_entry = tk.Entry(root, width=40)
        self.task_entry.pack(pady=10)
        
        self.add_button = tk.Button(root, text="Add Task", command=self.add_task)
        self.add_button.pack()
        
        self.task_listbox = tk.Listbox(root, width=50, height=15)
        self.task_listbox.pack(pady=10)
        
        self.complete_button = tk.Button(root, text="Mark Completed", command=self.mark_completed)
        self.complete_button.pack()
        
        self.remove_button = tk.Button(root, text="Remove Completed Tasks", command=self.remove_completed_tasks)
        self.remove_button.pack()
        
    def add_task(self):
        task = self.task_entry.get()
        if task:
            self.tasks.append({'task': task, 'completed': False})
            self.update_task_list()
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "Task cannot be empty!")
    
    def mark_completed(self):
        try:
            selected_index = self.task_listbox.curselection()[0]
            self.tasks[selected_index]['completed'] = True
            self.update_task_list()
        except IndexError:
            messagebox.showwarning("Warning", "Please select a task to mark as completed!")
    
    def remove_completed_tasks(self):
        self.tasks = [task for task in self.tasks if not task['completed']]
        self.update_task_list()
    
    def update_task_list(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.tasks:
            status = "✓" if task['completed'] else "✗"
            self.task_listbox.insert(tk.END, f"[{status}] {task['task']}")
    
# Run the app
if __name__ == "__main__":
    root = tk.Tk()
    app = ToDoApp(root)
    root.mainloop()
