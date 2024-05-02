import tkinter as tk
from tkinter import messagebox
import datetime
import streamlit as st

def calculate_countdown():
    try:
        day = int(day_entry.get())
        month = int(month_entry.get())
        year = int(year_entry.get())
        target_date = datetime.date(year, month, day)
        today = datetime.date.today()

        if target_date < today:
            messagebox.showerror("Fehler", "Bitte geben Sie ein zukünftiges Datum ein.")
        else:
            countdown = target_date - today
            messagebox.showinfo("Countdown", f"Bis zum {target_date.strftime('%d.%m.%Y')} sind es noch {countdown.days} Tage.")
    except ValueError:
        messagebox.showerror("Fehler", "Bitte geben Sie gültige Zahlen ein.")

# GUI erstellen
root = tk.Tk()
root.title("Geburtstags-Countdown")

# Eingabefelder für Tag, Monat und Jahr
day_label = tk.Label(root, text="Tag:")
day_label.grid(row=0, column=0)
day_entry = tk.Entry(root)
day_entry.grid(row=0, column=1)

month_label = tk.Label(root, text="Monat:")
month_label.grid(row=1, column=0)
month_entry = tk.Entry(root)
month_entry.grid(row=1, column=1)

year_label = tk.Label(root, text="Jahr:")
year_label.grid(row=2, column=0)
year_entry = tk.Entry(root)
year_entry.grid(row=2, column=1)

# Button zum Berechnen des Countdowns
calculate_button = tk.Button(root, text="Countdown berechnen", command=calculate_countdown)
calculate_button.grid(row=3, column=0, columnspan=2)

# Streamlit-Bereich für die Berechnung des Geburtstermins
st.write("### Geburtstermin-Timeline")
last_period_date = st.date_input('Letzter Menstruationszyklus' , format="YYYY/MM/DD")
if last_period_date:
    due_date = last_period_date + datetime.timedelta(days=280)
    st.write("Voraussichtlicher Geburtstermin:", due_date)

root.mainloop()
