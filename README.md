![Screenshot 2023-12-10 075950](https://github.com/KeanaMay/Package/assets/153400825/5ba6ae33-159e-41b5-a69b-0e7e75dc88ac)
Details:
 This system creates a basic nutrition tracking system that allows users to input information about consumed foods, visualize their nutritional progress, and set goals. It is a basic console-based application designed for tracking individual nutrition.
 from dataclasses import dataclass
import os
import matplotlib.pyplot as plt
import numpy as np

plt.style.use("bmh")

# Define a data class for representing food items
@dataclass
class Food:
    name: str
    calories: int
    protein: int
    fats: int
    carbs: int

# Constants for nutritional goals
PROTEIN_GOAL = 180  # grams
FAT_GOAL = 80       # grams
CARBS_GOAL = 300    # grams
CALORIE_GOAL_LIMIT = 3000  # kcal

# Function to clear the console screen
def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')

# Function to print a summary of nutrition information
def print_summary(total_calories, total_protein, total_fats, total_carbs):
    print("\nNutrition Summary:")
    print(f"Total Calories: {total_calories} kcal")
    print(f"Total Protein: {total_protein} grams")
    print(f"Total Fats: {total_fats} grams")
    print(f"Total Carbs: {total_carbs} grams")

# Main function for the nutrition tracker
def main():
    # Initialize empty list for storing food items and total nutritional values
    foods = []
    total_calories = 0
    total_protein = 0
    total_fats = 0
    total_carbs = 0

    while True:
        clear_screen()
        print("Nutrition Tracker")
        print("(1) Add a new food")
        print("(2) Visualize progress")
        print("(3) Quit")

        # Get user input for menu choice
        choice = input("Choose an option: ")

        if choice == "1":
            clear_screen()
            print("Adding a new food!")
            # Prompt user for food details
            name = input("Name: ")
            calories = int(input("Calories: "))
            protein = int(input("Protein: "))
            fats = int(input("Fat: "))
            carbs = int(input("Carbs: "))
            # Create a Food object and update totals
            food = Food(name, calories, protein, fats, carbs)
            foods.append(food)
            total_calories += food.calories
            total_protein += food.protein
            total_fats += food.fats
            total_carbs += food.carbs
            print("Successfully added!")

        elif choice == "2":
            # Visualization of nutrition progress
            sum(food.calories for food in foods)
            sum(food.protein for food in foods)
            sum(food.fats for food in foods)
            sum(food.carbs for food in foods)

            # Create subplots for visualizations
            fig, axs = plt.subplots(2, 2)

            # Plot macronutrient distribution as a pie chart
            axs[0, 0].pie([total_protein, total_fats, total_carbs], labels=["Proteins", "Fats", "Carbs"],
                          autopct="%1.1f%%")
            axs[0, 0].set_title("Macronutrients Distribution")

            # Plot macronutrient progress as a bar chart
            axs[0, 1].bar([0, 1, 2], [total_protein, total_fats, total_carbs], width=0.4)
            axs[0, 1].bar([0.5, 1.5, 2.5], [PROTEIN_GOAL, FAT_GOAL, CARBS_GOAL], width=0.4)
            axs[0, 1].set_title("Macronutrients Progress")

            # Plot calories goal progress as a pie chart
            axs[1, 0].pie([total_calories, CALORIE_GOAL_LIMIT - total_calories], labels=["Calories", "Remaining"],
                          autopct="%1.1f%%")
            axs[1, 0].set_title("Calories Goal Progress")

            # Plot calories goal over time as a line chart
            axs[1, 1].plot(list(range(len(foods))), np.cumsum([food.calories for food in foods]),
                           label="Calories Eaten")
            axs[1, 1].plot(list(range(len(foods))), [CALORIE_GOAL_LIMIT] * len(foods), label="Calorie Goal")
            axs[1, 1].legend()
            axs[1, 1].set_title("Calories Goal Over Time")

            # Adjust layout and display the plots
            fig.tight_layout()
            plt.show()

        elif choice == "3":
            # Exit the program
            break

        else:
            # Handle invalid input
            print("Invalid Choice!")

if _name_ == "_main_":
    # Call the main function when the script is executed
    main()

![Clean Brown Paper Texture Background Page Border](https://github.com/KeanaMay/Package/assets/153400825/9cbc8b6f-c6b9-49ef-ab83-078b5975a638)
