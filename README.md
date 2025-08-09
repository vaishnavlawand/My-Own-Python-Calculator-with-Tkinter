import tkinter as tk

# Function to handle button clicks
def click(button_text):
    current = entry.get()
    if button_text == "C":
        entry.delete(0, tk.END)
    elif button_text == "=":
        try:
            result = eval(current)
            entry.delete(0, tk.END)
            entry.insert(tk.END, str(result))
        except:
            entry.delete(0, tk.END)
            entry.insert(tk.END, "Error")
    else:
        entry.insert(tk.END, button_text)

# Window setup
root = tk.Tk()
root.title("Python Calculator")
root.configure(bg="#d3d3d3")  # Light gray background
root.resizable(False, False)

# Entry display
entry = tk.Entry(root, font=("Arial", 20), bd=5, relief="flat", justify="right", bg="#ffffff")
entry.grid(row=0, column=0, columnspan=4, pady=10, padx=10, ipady=10)

# Button layout
buttons = [
    ("7", 1, 0), ("8", 1, 1), ("9", 1, 2), ("/", 1, 3),
    ("4", 2, 0), ("5", 2, 1), ("6", 2, 2), ("*", 2, 3),
    ("1", 3, 0), ("2", 3, 1), ("3", 3, 2), ("-", 3, 3),
    ("0", 4, 0), (".", 4, 1), ("+", 4, 2), ("=", 4, 3),
    ("C", 5, 0)
]

# Create buttons
for (text, row, col) in buttons:
    btn_color = "#f06d4c" if text in ("C", "=") else "#e0e0e0"
    btn = tk.Button(root, text=text, font=("Arial", 16, "bold"),
                    bg=btn_color, fg="black", relief="flat", width=5, height=2,
                    command=lambda t=text: click(t))
    btn.grid(row=row, column=col, padx=5, pady=5)

# Fill empty spots for better layout
root.grid_rowconfigure(5, minsize=60)
root.grid_columnconfigure(3, minsize=80)

root.mainloop()
