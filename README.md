# pton0159
personalised_workoutplan
# Custom Workout Routine Builder with Dynamic Exercise Selection

# Database of exercises by fitness level and category
exercise_catalog = {
    'starter': {
        'aerobic': ["Walking briskly", "Light jogging", "Home stationary bike"],
        'muscle': ["Modified push-ups", "Bodyweight squats", "Basic planks"],
        'stretch': ["Shoulder stretch", "Hamstring stretch", "Quad stretch"]
    },
    'intermediate': {
        'aerobic': ["Running", "Jump Rope", "Cycling"],
        'muscle': ["Dumbbell rows", "Lunges", "Push-ups with rotation"],
        'stretch': ["Downward dog", "Hip flexor stretch", "Cat-Cow pose"]
    },
    'pro': {
        'aerobic': ["HIIT sessions", "Sprints", "Boxing drills"],
        'muscle': ["Pull-ups", "Deadlifts", "Bench press"],
        'stretch': ["Full split", "Deep pigeon pose", "Advanced hamstring stretch"]
    }
}

import random

def show_welcome_message():
    print("\n*** Welcome to the Personalized Fitness Planner ***")
    print("Create your custom workout routine based on your current fitness level.")
    print("Let's begin!\n")

def choose_level():
    options = {
        '1': 'starter',
        '2': 'intermediate',
        '3': 'pro'
    }
    while True:
        print("Select your fitness level:")
        print("1. Beginner")
        print("2. Intermediate")
        print("3. Advanced")
        choice = input("Your choice (1-3): ").strip()
        if choice in options:
            return options[choice]
        print("Invalid input, please try again.")

def pick_exercise_types():
    choices_map = {
        '1': ['aerobic'],
        '2': ['muscle'],
        '3': ['stretch'],
        '4': ['aerobic', 'muscle', 'stretch']
    }
    while True:
        print("\nChoose your preferred workout components:")
        print("1. Cardio")
        print("2. Strength")
        print("3. Flexibility")
        print("4. All of the above")
        user_choice = input("Your selection (1-4): ").strip()
        if user_choice in choices_map:
            return choices_map[user_choice]
        print("Invalid choice, please select again.")

def get_training_days():
    while True:
        try:
            days_input = int(input("Number of days to workout weekly (1-7): "))
            if 1 <= days_input <= 7:
                return days_input
            else:
                print("Please enter a number between 1 and 7.")
        except:
            print("Invalid input, please input a number.")

def assemble_workout_plan(level, categories, days):
    plan_structure = {}
    for day_num in range(1, days + 1):
        daily_plan = ["Warm-up: 5 mins"]
        for cat in categories:
            exercises_list = exercise_catalog[level][cat]
            # Randomly pick exercises
            selected_exercises = random.sample(exercises_list, min(2, len(exercises_list)))
            for ex in selected_exercises:
                daily_plan.append(f"{ex} - 10 mins")
        daily_plan.append("Cool-down: 5 mins")
        plan_structure[f"Day {day_num}"] = daily_plan
    return plan_structure

def display_routine(routine):
    print("\n--- Your Customized Weekly Workout ---\n")
    for day, activities in routine.items():
        print(f"{day}:")
        for act in activities:
            print(f" * {act}")
        print()
    print("Stay motivated and enjoy your workouts!")

def save_routine(routine, filename="my_custom_workout.txt"):
    with open(filename, 'w') as f:
        f.write("=== Personalized Workout Schedule ===\n\n")
        for day, activities in routine.items():
            f.write(f"{day}:\n")
            for act in activities:
                f.write(f" * {act}\n")
            f.write("\n")
    print(f"Workout plan saved to {filename}")

def main_flow():
    show_welcome_message()
    level_choice = choose_level()
    workout_types = pick_exercise_types()
    total_days = get_training_days()
    weekly_plan = assemble_workout_plan(level_choice, workout_types, total_days)
    display_routine(weekly_plan)
    save_choice = input("Would you like to save this plan? (yes/no): ").lower()
    if save_choice in ['yes', 'y']:
        save_routine(weekly_plan)
    print("Thank you! Keep up your fitness journey!")

if __name__ == "__main__":
    main_flow()
