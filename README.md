# Email-and-phone-extractorimport tkinter as tk
from tkinter import *
from tkinter import ttk
from tkinter.scrolledtext import *
import re

# Regex patterns
email_regex = re.compile(r"[\w\.-]+@[\w\.-]+")
phone_num_regex = re.compile(r'\d\d\d.\d\d\d.\d\d\d\d')
url_regex_https = re.compile(r"https?://www\.?\w+\.\w+")
url_regex = re.compile(r"http?://www\.?\w+\.\w+")

# Main window
window = Tk()
window.geometry('700x500')
window.title("Email & Phone Number Extractor")

# Tabs
tab_control = ttk.Notebook(window)
tab1 = ttk.Frame(tab_control)
tab2 = ttk.Frame(tab_control)
tab3 = ttk.Frame(tab_control)

tab_control.add(tab1, text="Home")
tab_control.add(tab2, text="Urls")
tab_control.add(tab3, text="About")
tab_control.pack(expand=1, fill="both")

# Home Tab
Label(tab1, text="Email & Phone Number Extractor", padx=5, pady=5).grid(column=0, row=0)
Label(tab1, text="Enter Text to Extract", padx=5, pady=5).grid(column=0, row=1)

Entry = ScrolledText(tab1, height=10)
Entry.grid(row=2, column=0, columnspan=2, padx=5, pady=5)

tab1_display = ScrolledText(tab1, height=10)
tab1_display.grid(row=7, column=0, columnspan=2, padx=5, pady=5)

# URL Tab
Label(tab2, text="URL Links Extractor", padx=5, pady=5).grid(column=0, row=0)
Label(tab2, text="Enter Text To Extract Links").grid(row=1, column=0)

Entry2 = ScrolledText(tab2, height=10)
Entry2.grid(row=2, column=0, columnspan=2, padx=5, pady=5)

tab2_display = ScrolledText(tab2, height=10)
tab2_display.grid(row=7, column=0, columnspan=2, padx=5, pady=5)

# Functions
def clear_text():
    Entry.delete('1.0', END)

def clear_display_result():
    tab1_display.delete('1.0', END)

def extract_email():
    raw_text = Entry.get('1.0', END)
    final_extract = email_regex.findall(raw_text)
    num_of_results = len(final_extract)
    results = '\nEmail Count: {}\nEmails: {}'.format(num_of_results, final_extract)
    tab1_display.insert(tk.END, results)

def extract_phonenumbers():
    raw_text = Entry.get('1.0', tk.END)
    final_extract = phone_num_regex.findall(raw_text)
    num_of_results = len(final_extract)
    result = '\nPhone Number Count: {}\nPhone Numbers: {}'.format(num_of_results, final_extract)
    tab1_display.insert(tk.END, result)

def clear_text_url():
    Entry2.delete('1.0', END)

def clear_display_result_url():
    tab2_display.delete('1.0', END)

def extract_http():
    raw_text = Entry2.get('1.0', tk.END)
    final_extract = url_regex.findall(raw_text)
    num_of_results = len(final_extract)
    results = '\nHTTP URL Count: {}\nURLs: {}'.format(num_of_results, final_extract)
    tab2_display.insert(tk.END, results)

def extract_https():
    raw_text = Entry2.get('1.0', tk.END)
    final_extract = url_regex_https.findall(raw_text)
    num_of_results = len(final_extract)
    results = '\nHTTPS URL Count: {}\nURLs: {}'.format(num_of_results, final_extract)
    tab2_display.insert(tk.END, results)

# Buttons - Home Tab
Button(tab1, text="Clear", command=clear_text, width=10, bg="#0349F4", fg="#fff").grid(row=4, column=0, padx=10, pady=10)
Button(tab1, text="Clear Result", command=clear_display_result, width=10, bg="#0349F4", fg="#fff").grid(row=5, column=0, padx=10, pady=10)
Button(tab1, text="Email", command=extract_email, width=10, bg="red", fg="#fff").grid(row=4, column=1, padx=10, pady=10)
Button(tab1, text="Phone", command=extract_phonenumbers, width=10, bg="green", fg="#fff").grid(row=5, column=1, padx=10, pady=10)

# Buttons - URL Tab
Button(tab2, text="Reset", command=clear_text_url, width=10, bg='#03A9F4', fg="#fff").grid(row=4, column=0, padx=10, pady=10)
Button(tab2, text="Extract HTTP", command=extract_http, width=10, bg='red', fg="#fff").grid(row=5, column=0, padx=10, pady=10)
Button(tab2, text="Extract HTTPS", command=extract_https, width=10, bg='blue', fg="#fff").grid(row=6, column=0, padx=10, pady=10)
Button(tab2, text="Clear Result", command=clear_display_result_url, width=10, bg='#03A9F4', fg="#fff").grid(row=7, column=0, padx=10, pady=10)

# About Tab
Label(tab3, text="Email Extractor V.0.0.1\nJesus saves @JCharisTech").grid(column=0, row=1)

window.mainloop()
