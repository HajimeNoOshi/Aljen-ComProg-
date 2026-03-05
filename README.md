import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.title("Grading Sheet Form")
root.geometry("420x360")
root.configure(bg="magenta")

# Variables
name = tk.StringVar()
subject = tk.StringVar()
prelim = tk.StringVar()
midterm = tk.StringVar()
final = tk.StringVar()
average = tk.StringVar()
remarks = tk.StringVar()

# Function
def calculate_grade():
    try:
        p = float(prelim.get())
        m = float(midterm.get())
        f = float(final.get())

        if p < 0 or p > 100 or m < 0 or m > 100 or f < 0 or f > 100:
            messagebox.showerror("Invalid Grade", "Grades must be between 0 and 100")
            return

        avg = (p * 0.30) + (m * 0.30) + (f * 0.40)
        average.set(f"{avg:.2f}")

        if avg >= 75:
            remarks.set("Passed")
        else:
            remarks.set("Failed")

    except ValueError:
        messagebox.showerror("Invalid Input", "Enter numeric grades only")

def clear_fields():
    name.set("")
    subject.set("")
    prelim.set("")
    midterm.set("")
    final.set("")
    average.set("")
    remarks.set("")

# Fonts
label_font = ("Broadway", 16, "bold")
entry_font = ("Times New Roman", 11)
button_font = ("Rockwell", 14, "bold")

# Labels and Entries
tk.Label(root, text="Student Name", bg="magenta", font=label_font).grid(row=0, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=name, font=entry_font).grid(row=0, column=1)

tk.Label(root, text="Subject", bg="magenta", font=label_font).grid(row=1, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=subject, font=entry_font).grid(row=1, column=1)

tk.Label(root, text="Prelim Grade", bg="magenta", font=label_font).grid(row=2, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=prelim, font=entry_font).grid(row=2, column=1)

tk.Label(root, text="Midterm Grade", bg="magenta", font=label_font).grid(row=3, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=midterm, font=entry_font).grid(row=3, column=1)

tk.Label(root, text="Final Grade", bg="magenta", font=label_font).grid(row=4, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=final, font=entry_font).grid(row=4, column=1)

# Buttons
tk.Button(root, text="Calculate", font=button_font, command=calculate_grade).grid(row=5, column=0, columnspan=2, pady=10)
tk.Button(root, text="Clear", font=button_font, command=clear_fields).grid(row=6, column=0, columnspan=2)

# Output
tk.Label(root, text="Average", bg="magenta", font=label_font).grid(row=7, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=average, font=entry_font, state="readonly").grid(row=7, column=1)

tk.Label(root, text="Remarks", bg="magenta", font=label_font).grid(row=8, column=0, padx=10, pady=5, sticky="w")
tk.Entry(root, textvariable=remarks, font=entry_font, state="readonly").grid(row=8, column=1)

root.mainloop()
