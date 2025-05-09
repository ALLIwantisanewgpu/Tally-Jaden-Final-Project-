import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk
import os

class CustomerApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Customer Management")
        self.root.geometry("400x500")

        self.name_var = tk.StringVar()
        self.phone_var = tk.StringVar()

        # Load and display image 1
        img1_path = os.path.join(os.path.dirname(__file__), "images", "image1.png")
        img1 = Image.open(img1_path).resize((100, 100))
        self.photo1 = ImageTk.PhotoImage(img1)
        img_label1 = tk.Label(root, image=self.photo1, text="Red Image", compound="top")
        img_label1.pack(pady=10)

        # Labels and entries
        tk.Label(root, text="Customer Name:").pack()
        self.name_entry = tk.Entry(root, textvariable=self.name_var)
        self.name_entry.pack()

        tk.Label(root, text="Phone Number:").pack()
        self.phone_entry = tk.Entry(root, textvariable=self.phone_var)
        self.phone_entry.pack()

        # Buttons
        tk.Button(root, text="Submit", command=self.submit).pack(pady=5)
        tk.Button(root, text="Open Employee Window", command=self.open_employee_window).pack(pady=5)
        tk.Button(root, text="Exit", command=self.exit_app).pack(pady=5)

    def submit(self):
        name = self.name_var.get().strip()
        phone = self.phone_var.get().strip()
        if not name or not phone:
            messagebox.showerror("Input Error", "All fields must be filled.")
            return
        if not phone.isdigit():
            messagebox.showerror("Input Error", "Phone number must contain only digits.")
            return
        messagebox.showinfo("Success", f"Customer '{name}' with phone '{phone}' saved!")

    def open_employee_window(self):
        emp_window = tk.Toplevel(self.root)
        EmployeeWindow(emp_window)

    def exit_app(self):
        if messagebox.askokcancel("Exit", "Do you really want to quit?"):
            self.root.quit()


class EmployeeWindow:
    def __init__(self, window):
        self.window = window
        self.window.title("Employee Information")
        self.window.geometry("400x400")

        self.emp_name_var = tk.StringVar()
        self.emp_id_var = tk.StringVar()

        # Load and display image 2
        img2_path = os.path.join(os.path.dirname(__file__), "images", "image2.png")
        img2 = Image.open(img2_path).resize((100, 100))
        self.photo2 = ImageTk.PhotoImage(img2)
        img_label2 = tk.Label(window, image=self.photo2, text="Blue Image", compound="top")
        img_label2.pack(pady=10)

        tk.Label(window, text="Employee Name:").pack()
        self.emp_name_entry = tk.Entry(window, textvariable=self.emp_name_var)
        self.emp_name_entry.pack()

        tk.Label(window, text="Employee ID:").pack()
        self.emp_id_entry = tk.Entry(window, textvariable=self.emp_id_var)
        self.emp_id_entry.pack()

        tk.Button(window, text="Submit", command=self.submit_employee).pack(pady=5)

    def submit_employee(self):
        name = self.emp_name_var.get().strip()
        emp_id = self.emp_id_var.get().strip()
        if not name or not emp_id:
            messagebox.showerror("Input Error", "All fields must be filled.")
            return
        if not emp_id.isdigit():
            messagebox.showerror("Input Error", "Employee ID must be numeric.")
            return
        messagebox.showinfo("Success", f"Employee '{name}' with ID '{emp_id}' saved!")


if __name__ == "__main__":
    root = tk.Tk()
    app = CustomerApp(root)
    root.mainloop()
