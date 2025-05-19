    Guess the number with an interface game on py




    import tkinter as tk
    from tkinter import messagebox
    import random

    class GuessNumberGame:
        def __init__(self, root):
            self.root = root
            self.root.title("Угадай число")
            self.root.geometry("300x200")
        
            self.secret_number = random.randint(1, 100)
            self.attempts = 0
        
            self.label = tk.Label(root, text="Я загадал число от 1 до 100. Попробуй угадать!")
            self.label.pack(pady=10)
        
            self.entry = tk.Entry(root)
            self.entry.pack(pady=5)
        
            self.guess_button = tk.Button(root, text="Проверить", command=self.check_guess)
            self.guess_button.pack(pady=5)
        
            self.hint_label = tk.Label(root, text="")
            self.hint_label.pack(pady=5)
        
            self.attempts_label = tk.Label(root, text=f"Попытки: {self.attempts}")
            self.attempts_label.pack(pady=5)
        
        def check_guess(self):
            try:
                guess = int(self.entry.get())
                self.attempts += 1
                self.attempts_label.config(text=f"Попытки: {self.attempts}")
            
                if guess < 1 or guess > 100:
                    messagebox.showwarning("Ошибка", "Введите число от 1 до 100!")
                    return
                
                if guess < self.secret_number:
                    self.hint_label.config(text="Загаданное число больше!")
                elif guess > self.secret_number:
                    self.hint_label.config(text="Загаданное число меньше!")
                else:
                    messagebox.showinfo("Победа!", f"Поздравляю! Вы угадали число {self.secret_number} за {self.attempts} попыток!")
                    self.root.destroy()
                
                self.entry.delete(0, tk.END)
            
            except ValueError:
                messagebox.showerror("Ошибка", "Введите целое число!")

    if __name__ == "__main__":
        root = tk.Tk()
        game = GuessNumberGame(root)
        root.mainloop()
