# PRODIGY_CS_03
A tool to check password complexity and understanding of Password standards

import re
import tkinter as tk
from tkinter import messagebox
from datetime import datetime, timedelta



def assess_password_strength(password):
    length_criteria = len(password) >= 8
    uppercase_criteria = bool(re.search(r'[A-Z]', password))
    lowercase_criteria = bool(re.search(r'[a-z]', password))
    number_criteria = bool(re.search(r'[0-9]', password))
    special_criteria = bool(re.search(r'[!@#$%^&*(),.?":{}|<>]', password))
    

    criteria_met = sum([length_criteria, uppercase_criteria, lowercase_criteria, number_criteria, special_criteria])
    
    if criteria_met == 5:
        strength = "Very Strong"
    elif criteria_met == 4:
        strength = "Strong"
    elif criteria_met == 3:
        strength = "Moderate"
    else:
        strength = "Weak"
    
    feedback = []
    if not length_criteria:
        feedback.append("Password should be at least 8 characters long.")
    if not uppercase_criteria:
        feedback.append("Password should contain at least one uppercase letter.")
    if not lowercase_criteria:
        feedback.append("Password should contain at least one lowercase letter.")
    if not number_criteria:
        feedback.append("Password should contain at least one number.")
    if not special_criteria:
        feedback.append("Password should contain at least one special character (e.g., !@#$%^&*()).")
   
   
    return strength, feedback
    

def check_password():
    password = entry.get()
    strength, feedback = assess_password_strength(password)
    
    feedback_text = "\n".join(feedback) if feedback else "Your password meets all the criteria."
    
    messagebox.showinfo("Password Strength", f"Password Strength: {strength}\n\nFeedback:\n{feedback_text}")

# GUI setup
root = tk.Tk()
root.title("Password Strength Checker")

frame = tk.Frame(root, padx=20, pady=20)
frame.pack(padx=10, pady=10)

label = tk.Label(frame, text="Enter your password:")
label.pack(pady=5)

entry = tk.Entry(frame, show="*", width=30)
entry.pack(pady=5)

button = tk.Button(frame, text="Check Password Strength", command=check_password)
button.pack(pady=10)

root.mainloop()

