---
layout: page
title: StudentConnect User Guide
---

StudentConnect is a solution for hassle-free team formation for students to browse profiles and connect with others for group projects.

* Table of Contents
  {to be added}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `11` or above installed in your Computer.

2. Download the latest `studentconnect.jar` from [here](). 

3. Copy the file to the folder you want to use as the _home folder_ for your StudentConnect.

4. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar studentconnect.jar` command to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

5. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

    * `list` : Lists all students.

    * `add n/John Doe m/Computer Science y/2 e/johnd@u.nus.edu d/I’m a Frontend Developer sm/https://www.linkedin.com/in/john-doe-123456789` : Adds a student named `John Doe` to the StudentConnect system.

    * `delete [email]` : Deletes the student with the corresponding email.

    * `clear` : Deletes all students.

    * `exit` : Exits the app.

6. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g. `n/NAME [t/TAG]` can be used as `n/John Doe t/friend` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/friend`, `t/friend t/family` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
</div>

### Viewing help : `help`

Shows a message explaining how to access the help page.

![help message](images/helpMessage.png)

Format: `help`

### Adding a student : `add`

Adds a student to the system.

Format: `add n/NAME m/MAJOR y/YEAR e/EMAIL d/DESCRIPTION sm/SOCIALMEDIA`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of social media links (including 0)
</div>

Examples:
* `add n/John Doe m/Computer Science y/2 e/johnd@u.nus.edu d/I’m a Frontend Developer sm/https://www.linkedin.com/in/john-doe-123456789`
* `add n/Betsy Crowe m/Computer Science y/2 e/betsycrowe@u.nus.edu  d/I’m adept at Backend technologies sm/`

Acceptable Values:
* Name: Full names with alphabetical characters
* Major: Valid major names at NUS
* Year: Numeric year level
* Email: Valid email address ending in “@u.nus.edu”
* Description: Maximum 150 characters
* Social Media Link: Valid URL format to social media account (optional to include)

Expected Output (Success):
* GUI: New student entry added in the main student list
* Message: “Details added successfully! New student added: (details of new student)”

Expected Output (Failure):
* Message:  "Invalid command format! add: Adds a person to StudentConnect. <br>
Parameters: n/NAME m/MAJOR y/YEAR e/EMAIL d/DESCRIPTION sm/SOCIAL_MEDIA_LINK <br>
Example: add n/John Doe m/Computer Science y/2 e/johnd@u.nus.edu d/I love programming in my free time <br>
sm/https://www.linkedin.com/in/john-doe-123456789";

Mockup of add feature (Success): <br>
![Add feature](images/add.png)

### Listing all students : `list`

Shows a list of all students in the system.

Format: `list`

#### Expected Output (Success):
* GUI: List of all student entries in the system
* Message: “Viewing all students”

#### Expected Output (Failure):
* Message: “Error: Unable to retrieve student entries. Please try again.”

![sample result for 'list'](images/list.png)

### Editing a person : `edit`

Edits an existing student in the system.

Format: `edit INDEX [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`

* Edits the person at the specified `INDEX`. The index refers to the index number shown in the displayed person list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e. adding of tags is not cumulative.
* You can remove all the person’s tags by typing `t/` without
  specifying any tags after it.

Examples:
*  `edit 1 p/91234567 e/johndoe@example.com` Edits the phone number and email address of the 1st person to be `91234567` and `johndoe@example.com` respectively.
*  `edit 2 n/Betsy Crower t/` Edits the name of the 2nd person to be `Betsy Crower` and clears all existing tags.

### Finding a student by name: `find`

Finds student(s) whose name(s) contain any of the given keywords.

Format: `find KEYWORD [MORE_KEYWORDS]`

* The search is case-insensitive. e.g. `john` will match `John`
* The order of the keywords does not matter. e.g. `John Doe` will match `Doe John`
* Only the name is searched.
* Partial words can be matched. e.g. `John` will match `Johnny`
* Persons matching at least one keyword will be returned (i.e. `OR` search).
  e.g. `John Crowe` will return `John Doe`, `Betsy Crowe`

Examples:
* `find John` returns `john`, `John Doe` and `Johnny Wee`
* `find john betsy` returns `John Doe`, `Betsy Crowe`<br>

Expected Output (Success):
* GUI: List of all student entries whose name(s) match the keyword(s) in the system

Expected Output (Failure):
* Message: “Unable to find students with the given keyword(s).”
  ![result for 'find alex'](images/findAlexResult.png)

### Deleting a person : `delete`

Deletes a specific student and all personal details based on email.

Format: `delete [EMAIL]`

* Deletes the person with the specified `EMAIL`.
* The index refers to the email number shown in the displayed person list.
* The email must be registered in the system.

Examples:
* `list` followed by `delete alexy@u.nus.edu` deletes Alex Yeo from the system.

Acceptable Values:
* Email: a previously registered email address ending in `u.nus.edu`

Expected Output(Success):
* GUI: Student details removed from student list.
* Message: `Person deleted successfully!`
  ![Delete feature](images/delete.png)

Expected Output (Failure):
* Message: `Error! Email not found!`

### Clearing all entries : `clear`

Clears all entries from the system.

Format: `clear`

### Exiting the program : `exit`

Exits the program.

Format: `exit`

#### Expected Output(Success):
* GUI: Application window closes.
* Message (before closing): “Thank you for using StudentConnect!”

#### Expected Output(Failure):
* Message: “Error: Exiting the program failed.”

![Exit](images/exit.png)

### Saving the data

Students' data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

Students' data are saved automatically as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, StudentConnect will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.
</div>

### Archiving data files `[coming in v2.0]`

_Details coming soon ..._

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous StudentConnect home folder.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.

--------------------------------------------------------------------------------------------------------------------

## Command summary

| Action     | Format, Examples                                                                                                                                                                   |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Add**    | `add n/NAME m/MAJOR y/YEAR e/EMAIL d/DESCRIPTION sm/SOCIALMEDIA` <br> e.g., `add n/Betsy Crowe m/Computer Science y/2 e/betsycrowe@u.nus.edu  d/I’m adept at Backend technologies` |
| **Clear**  | `clear`                                                                                                                                                                            |
| **Delete** | `delete EMAIL`<br> e.g., `delete betsycrowe@u.nus.edu`                                                                                                                             |
| **Edit**   | `edit INDEX [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`<br> e.g.,`edit 2 n/James Lee e/jameslee@example.com`                                                        |
| **Find**   | `find KEYWORD [MORE_KEYWORDS]`<br> e.g., `find James Jake`                                                                                                                         |
| **List**   | `list`                                                                                                                                                                             |
| **Help**   | `help`                                                                                                                                                                             |
