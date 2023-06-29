import difflib
import tkinter as tk
from tkinter import messagebox

def check_plagiarism():
    text1 = entry_text1.get("1.0", tk.END)
    text2 = entry_text2.get("1.0", tk.END)

    # Remove leading/trailing whitespaces and convert to lowercase
    text1 = text1.strip().lower()
    text2 = text2.strip().lower()

    # Split the texts into individual words
    words1 = text1.split()
    words2 = text2.split()

    # Calculate the similarity ratio using difflib's SequenceMatcher
    similarity_ratio = difflib.SequenceMatcher(None, words1, words2).ratio()

    output_text.delete("1.0", tk.END)
    output_text.insert(tk.END, f"Similarity Ratio: {similarity_ratio:.2f}")

def reset_fields():
    entry_text1.delete("1.0", tk.END)
    entry_text2.delete("1.0", tk.END)
    output_text.delete("1.0", tk.END)

# Create GUI
window = tk.Tk()
window.title("Plagiarism Checker")
window.configure(bg="#F0F0F0")  # Set background color

# Text Entry for Input
label_text1 = tk.Label(window, text="Text 1:", font=("Arial", 14), bg="#F0F0F0")
label_text1.pack()
entry_text1 = tk.Text(window, height=5, width=30, font=("Arial", 14))
entry_text1.pack()

label_text2 = tk.Label(window, text="Text 2:", font=("Arial", 14), bg="#F0F0F0")
label_text2.pack()
entry_text2 = tk.Text(window, height=5, width=30, font=("Arial", 14))
entry_text2.pack()

# Button to Check Plagiarism
button_check = tk.Button(window, text="Check Plagiarism", command=check_plagiarism, font=("Arial", 14), bg="#4CAF50", fg="white")
button_check.pack()

# Button to Reset Fields
button_reset = tk.Button(window, text="Reset", command=reset_fields, font=("Arial", 14), bg="#FF4500", fg="white")
button_reset.pack()

# Output Display
output_text = tk.Text(window, height=2, width=30, font=("Arial", 14))
output_text.pack()

# Run the GUI
window.mainloop()
