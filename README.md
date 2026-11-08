# CLI App TipJar - Tenant Tip Tracker

## Vision
This app is for any worker in an apartment building or hotel who has to
keep track of and organize their tips from tenants. It gives them one central place to
view and manage the tips they received: from who, where, and when. It
solves the problem of trying to manage a mix of cash and virtual tips, not knowing how much you made for the year, week or day and storing information about the tip specifically. The long-term goal is an application with a GUI and database
that is easy to manage and search through data of tenant tips.

## Version 1
A terminal app for a friend of mine who works in an apartment building.
You can add, edit, and remove tips, see your total, and search and sort
your tips by date or amount. Tips are stored in a list of dictionaries while the program
runs, soon will implement saving and storing data.

## What each tip records
- **Tenant name** (optional, can be left blank if name is unknown.)
- **Apartment** (for example `4B` or the floor, can be left blank if unknown)
- **Amount** (always a number in dollars; use `0` or an estimated value
  for physical items)
- **Type**: cash, card, gift card, physical item, or other
- **Description** (optional text, for example "bottle of wine" for a
  physical item, or details for "other")
- **Date** the tip was received, in the format `MM-DD-YYYY`
  (for example `12-24-2026`), so tips can be searched by year and yearly
  totals can be calculated

## Menu options (Version 1)
1. Add a tip
2. Edit a tip
3. Remove a tip
4. Show all tips
5. Search tips (by year)
6. Sort tips (by date or by amount)
7. Show total tips
8. Quit

## Prerequisites

- Python 3
- Git

## Setup to Run the Program
```sh
git clone git@github.com:xavinyc-dev/cli-app-tip-jar-tenant-tip-tracker.git
cd cli-app-tip-jar-tenant-tip-tracker

# Run program using:
python3 src/main.py
```

## Setup For Developers / Running Tests
```sh
git clone git@github.com:xavinyc-dev/cli-app-tip-jar-tenant-tip-tracker.git
cd cli-app-tip-jar-tenant-tip-tracker

# Create a virtual environment in a folder named .venv, then turn it on
python3 -m venv .venv
source .venv/bin/activate

# Install required packages (includes pytest)
pip install -r requirements.txt

# Run tests
python3 -m pytest -v
```
Virtual Environment only active in current session. It needs to be activated whenever opening a new terminal for pytests to work.

To test UI and functionality:
```sh
python3 src/main.py
```
Add multiple tips, edit it, show all tips, show the total, search and sort, try a bad input anywhere in the program.

## Version 1.5
- Save tips to a JSON file so they're still there the next time the
  program runs

## Not in Version 1
- A real database (SQL)
- Searching by exact date or date range
- Year-to-year comparison
- A visual interface
- Access from other devices
- Connection to Excel
- Analytics

## Design
Each operation (add, remove, edit, search, sort, total) lives in its own
function. There are 3 modules now containing all the code. 

- The data.py module holds the pure functions that deal with our data and return values that the program uses, nothing here prints or takes in user input. 
- The menu.py module holds our menu functions that take user inputs and displays the menus with data, this module calls the functions from data.py by imports. 
- The main.py module contains the main function that runs the entire program. There lives the tips_jar list of tips, which are dictionary records, as well as the tip_id counter which adds an id digit to each tip. Main calls selects_option after user input and hands user_input, the tips_jar, and the tip_id to selects_option in menu module while also assigning the call to tip_id as selects_option will return tip_id to main. tip_id is only changed if someone adds a tip as add_tip is the only function that can change it. It updates in main when returned by selects_option. The guard at end of main is to ensure the program only runs if that file was run directly.

main -> menu -> data
Main module imports functions from menu, and menu module imports from data.
  
Keeping everything separate will help switching to a real SQL database since now only data.py needs changing when making that switch.

