import tkinter as tk
from tkinter import messagebox
import random

# Defining choices for selection
choices = ["goblin", "elves", "moss"]

# Function to show the game page after the welcome page
def show_game_page():
    welcome_frame.pack_forget()  # Hide the welcome screen
    game_frame.pack(padx=10, pady=10, fill="both", expand=True)  # Show the game screen

# Function to play the game
def play_game():
    user_choice = entry.get().lower()  # Get the user input and convert it to lowercase
    if user_choice not in choices:
        # Display custom warning message for incorrect input
        messagebox.showwarning("Invalid Input", "Careful with the spelling punk, you can only fight with 'goblin', 'moss' or 'elves', no mistakes!")
        return

    computer_choice = random.choice(choices)
    
    if user_choice == "goblin" and computer_choice == "elves":
        result = f"Oops! You ran away in fear. You were fighting against {computer_choice}."
    elif user_choice == "goblin" and computer_choice == "moss":
        result = f"Nom nom, delicious! You won against {computer_choice}!"
    elif user_choice == "goblin" and computer_choice == "goblin":
        result = "Oh! It's a tie!"
    elif user_choice == "elves" and computer_choice == "goblin":
        result = "Ýou made a scary face, the Goblin ran away!"
    elif user_choice == "elves" and computer_choice == "moss":
        result = f"Oops! You were fighting against deadly, deadly MOSS you die.."
    elif user_choice == "elves" and computer_choice == "elves":
        result = "Oh! It's your fellow Elves, you gave them a hug! It's a tie."
    elif user_choice == "moss" and computer_choice == "elves":
        result = "Congrats! You 'killed' all the elves he he he!"
    elif user_choice == "moss" and computer_choice == "moss":
        result = "Hey look! It's your fellow Moss friend, it's a tie."
    elif user_choice == "moss" and computer_choice == "goblin":
        result = "AAAH! YOU ARE EATEN!"

    messagebox.showinfo("Game Result", result)
    ask_to_play_again()

# Function to ask if the user wants to play again
def ask_to_play_again():
    play = messagebox.askquestion("Try again", "Try one more time? Yes/No: ")
    if play == "yes":
        # Clear the input for the next round
        entry.delete(0, tk.END)
    else:
        messagebox.showinfo("Exit", "Bye for now! Thanks for stopping by, you fought bravely!")
        root.quit()  # Close the application

# GUI Setup
root = tk.Tk()
root.title("Goblin, Elf, and Moss Game")
root.geometry("1000x500")
root.configure(bg='#8FBC8F')  # Lighter green background

# Welcome Frame
welcome_frame = tk.Frame(root, bg='#8FBC8F')
welcome_frame.pack(padx=10, pady=10, fill="both", expand=True)

# Welcome message
welcome_message = """                                                      𓋼𓍊 𓆩♡𓆪 𓍊𓋼 \n \n \n Welcome to the magical land of Goblin, Elves and (the deadly) Moss game! 
Please insert who you want to fight side by side and start the game.."""
welcome_label = tk.Label(welcome_frame, text=welcome_message, bg='#8FBC8F', fg="black", font=("Skia", 20), justify="left")
welcome_label.pack(pady=20)

# Start button
start_button = tk.Button(welcome_frame, text="Start Game", command=show_game_page, width=15)
start_button.pack(pady=10)

# Game Frame (third screen where the game is played and rules are shown)
game_frame = tk.Frame(root, bg='#2E8B57')  # Darker green background

# Rules message on the same screen as the input form
rules_message = """Note: Do not forget! Goblin is not affected but loves to eat the deadly Moss, yet Goblin is afraid of the Elves.
The Moss is deadly for the Elves so it will kill them. If you find out that you are fighting against one of your fellows it will end in a tie.
\n Choose wisely, you wouldn’t know who you are fighting against until you insert your choice and press enter!"""
rules_label = tk.Label(game_frame, text=rules_message, bg='#2E8B57', fg="white", font=("Helvetica", 16), justify="left")
rules_label.pack(pady=20)

# Label to prompt user input
label = tk.Label(game_frame, text="Type 'goblin', 'elves' or 'moss'", bg='#2E8B57', fg="white", font=("Helvetica", 15, "bold"))
label.pack(pady=5)

# Entry widget (text field) for user input
entry = tk.Entry(game_frame, width=20)
entry.pack(pady=5)

# Button to play the game
play_button = tk.Button(game_frame, text="Enter", command=play_game, width=10)
play_button.pack(pady=10)

# Run the GUI event loop
root.mainloop()
