WATER INTAKE TRACKER

Water Intake Tracker is a Python based health and wellness tool designed to help users stay properly hydrated throughout the day. It calculates a personalized daily water intake recommendation based on the user's weight and physical activity level, and then sends regular reminders to drink water.  

 Features

 Calculates daily water needs (based on weight & activity)
 Sends reminder every hour to drink 250ml water
 Tracks how much you've consumed
 Shows how much is left to reach your daily goal
 Desktop notifications using `plyer`
 Simple console interaction

How It Works
1. Enter your name, weight, and activity level (low, moderate, high)
2. The program calculates your water need using the formula:
3. daily_need = weight (kg) × 0.033 + activity bonus
4. You’ll get a reminder every 60 minutes to drink 250ml of water.
5. Each time you drink, press Enter to confirm.
6. When you reach your goal, you'll be congratulated! 

 

If the activity is Low then the additional liters of water will be 0.0                
If the activity is Moderate then the additional liters of water will be +0.5               
If the activity is High then the additional liters of water will be +1.0               



Technology Used

 Python
`time` module (for hourly reminder)
`datetime` (for timestamps)
[`plyer`](https://pypi.org/project/plyer/) – for desktop notifications

For JUPYTER NOTEBOOK
Install `plyer` using pip
pip install plyer

SAMPLE OUTPUT:-
Welcome to Water Intake Tracker 
Enter your name: Sanjay
Enter your weight (in kg): 70
Enter activity level (low / moderate / high): moderate

Sanjay, your recommended daily water intake is 2.81 liters.

[10:00:00] Reminder: Time to drink 250ml of water! 
Press Enter after you drink the water... 

 You've completed 1/11 servings.
 Next reminder in 60 minutes...
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
 This project is open-source and free to use.

plyer is a Python library that provides platform-independent access to common features of a user's device like sending notifications, checking battery level, accessing sensors, etc.
SAMPLE:-
"Hey Python, I want to do things like a mobile app notify users, access the clipboard, or check battery even if I’m running on desktop!"


LINE BY LINE STEP BY STEP EXPLANATION:-


Imports:
python
import time
import datetime
from plyer import notification

time Lets you pause program execution (used to delay reminders).
datetime Used to get the current time (to show timestamp with each reminder).
plyer.notification Allows you to show desktop notifications (like mobile popups).

Function Which is to Calculate Water Intake

def calculate_water_intake(weight, activity_level):
    base = weight * 0.033
    if activity_level == 'moderate':
        return base + 0.5
    elif activity_level == 'high':
        return base + 1
    else:
        return base

Formula is most health sources recommend 33ml of water per kg of body weight.
If you’re more active, you lose more water (sweating), so we add 0.5–1 liter extra.

Function to Send Notification

def send_notification(title, message):
    notification.notify(
        title=title,
        message=message,
        timeout=10
    )


Uses plyer to send a popup notification on your desktop.
timeout=10 notification disappears after 10 seconds.

Main Function for  Water Tracker

def water_tracker():
    print("\n Welcome to Water Intake Tracker ")
    name = input("Enter your name: ")
    weight = float(input("Enter your weight (in kg): "))
    activity = input("Enter activity level (low / moderate / high): ").lower()

Welcomes the user and takes 3 inputs:

Name
Weight (as `float` because kg can be decimal)
Activity level, converted to lowercase for consistency

Calculate Daily Water Need

 daily_target = round(calculate_water_intake(weight, activity), 2)
 print(f"\n{name}, your recommended daily water intake is {daily_target} liters.")

Calls the earlier function to calculate water needs
round(..., 2) is rounds result to 2 decimal places
Prints the daily goal

Divide into Servings
    serving_ml = 250
    servings_needed = int((daily_target * 1000) / serving_ml)
    servings_done = 0

You’ll drink water in 250 ml servings
Converts total liters to milliliters, divides by 250 to know how many servings you need
Starts a counter `servings_done` at 0

Reminder Loop

    print("\nWe’ll remind you every 60 minutes to drink 250ml of water.")
    print("Press Ctrl+C to stop the tracker.\n")
Informs user how the tracker works
    try:
        while servings_done < servings_needed:
            now = datetime.datetime.now().strftime("%H:%M:%S")
            print(f"[{now}] Reminder: Time to drink 250ml of water! ")


Loops while you still have servings left
now holds current time in `HH:MM:SS` format
Prints reminder in console with timestamp

python
            send_notification("Water Reminder ", f"{name}, drink 250ml of water now!")

Sends popup desktop notification

python
            input("Press Enter after you drink the water... \n")
            servings_done += 1

Pauses and waits for the user to press Enter
Increments the water count by 1


            remaining = servings_needed - servings_done
            print(f" You've completed {servings_done}/{servings_needed} servings.")
            print(f" Next reminder in 60 minutes...\n")
            time.sleep(60 * 60)  # 1 hour delay

 Calculates and prints how many servings are left
Pauses the program for 1 hour (`60 * 60` seconds)

Handling Exit
    except KeyboardInterrupt:
        print("\nTracker stopped manually. Stay hydrated! ")

If user presses Ctrl+C, this block handles the manual exit gracefully

Final Success Message
    if servings_done == servings_needed:
        print(f"\n Great job, {name}! You met your daily water goal of {daily_target} liters! ")

When all servings are done, user gets a congratulatory message

Run the Function

python
water_tracker()

This starts the whole process when the script is run
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

