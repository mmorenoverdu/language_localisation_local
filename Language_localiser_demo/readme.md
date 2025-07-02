### LANGUAGE LOCALISER DEMO ###
**Author:** Marcos Moreno Verdu | **Date:** 07/06/2025 | **Last updated PsychoPy version:** 2024.2.3

This demo is intended to demonstrate how to implement a language localisation in PsychoPy without requiring to add any code.

This demo only works for **LOCAL** experiments, not online experiments. The demo is intended for users working on Builder mode.

## Critical considerations ##

We need 2 Excel sheets (with extension type .xlsx) to store:
- The available language localisations: "language_localiser.xlsx"
- The list of messages to use as variables to display text on screen: "messages.xlsx"

In the Experiment Settings button, in the Basic tab, the Experiment Info section must have a "language" field with the list of languages. This allows to select the language **before** every run of the Experiment through a dropdown menu in the pop-up dialogue box. These languages need to be specified as in the language column of the language localiser Excel sheet.

All the text components which should be dynamically updated for language should have their "Text" field in "Set to every repeat". This allows to change dynamically the value of the variable, which therefore changes the text to be shown.

# How does it work #

The first routine of the experiment must be the language settings routine. This routine has a code component that only runs Python code (i.e., only works locally). The code is divided into two tabs:
- BEGIN EXPERIMENT: the code imports the Excel sheet "messages.xlsx" into PsychoPy, creates a dictionary with the messages and allow the variables to be used directly (as global variables in the experiment's environment). This needs to happen **at the beginning of the experiment** because the components to display text require these variables to exist at that stage; otherwise the experiment will crash, looking for a variable not yet defined. At this point all the messages are set to English (EN) by default. This means you **DO NOT NEED to change the code here**, as it will automatically load the most up-to-date version of the messages Excel sheet. This means **the only thing you need to do is to update the 'messages.xlsx' Excel sheet**.  
- BEGIN ROUTINE: the code updates the language to be used based on the choice made in the dialogue box before the first screen of the experiment actually appears. Because the language settings routine is the first routine of the experiment, this code will **automatically** update all the messages to match the language code as used in the language localiser Excel sheet. Again, this means you **DO NOT NEED to change the code here** to add your language, it will do it automatically for you.

The language settings routine is wrapped in a loop that only runs 1 time, and whose conditions file is the language localiser Excel sheet. This allows to import the available languages by just updating the Excel sheet, without requiring to type any code. The number of rows in the localiser Excel sheet **should match** with the number of conditions that PsychoPy identifies in the loop. If not, click on the loop name and **refresh the Excel sheet by clicking on the green arrows**.

Every text component in the experiment has a variable name in their "Text" field (e.g., "welcome_msg" for the welcome_text component). This variable will be **automatically** updated based on the language choice in the dialogue box. The variable name **MUST BE an existing message as defined in 'messages.xlsx'** before the experiment is launched.

# Adding a new language #

If you just want to add a new language without any further modifications (i.e., you do not want to provide other messages than the ones already used), you just need to modify 3 things:
1. In language_localiser.xlsx, add a new **ROW** with your new language and its code. Write this in English (e.g., "Chinese", "CH").
2. In messages.xlsx, add a new **COLUMN**, titled with the code you used in the previous step (e.g., "CH"). For each message, provide the corresponding translation into your desired language.
3. In PsychoPY, go to Experiment Settings and add a new language to the list of languages in the **language field**, with the name being the language you used in Step 1. It is critical that you add your language using '' (e.g., 'Chinese'). If you want your language to be the default choice every time you run the experiment, you just have to **place it at the beginning of the list**.

# Using the language localisation with an Instructions loop #

Instructions in PsychoPy are typically shown as loops and the message to show in each iteration of the loop is updated based on an Excel sheet. This is useful to iterate over the instructions without requiring to write code. The repetitions of the loop should be set to 1, and the loop type to 'sequential' (so that the Excel sheet is looped only 1 time and in order, not randomly). Then, once the loop has iterated through all the rows in the corresponding Excel sheet one time and in the order they appear, it will finish and the experiment will progress to the next screen.

This demo includes an instructions routine and instructions loop, as well as an "instructions.xlsx" Excel sheet. The idea is the same as with 'messages.xlsx'. The excel sheet contains **1 column per language available**, and each row corresponds to the corresponding message in that language. The title of the columns must be **identical** and only change in their final part, which is the code of the language (e.g., inst_msg_EN for English, inst_msg_ES for Spanish, etc.). The code **must obviously match the code used in the language localiser** Excel sheet to work appropriately.

# Expanding the language localisation #

The same logic can be applied while creating new routines which contain text to be displayed on screen and that you want to update dynamically and automatically based on the language choice. To do that, just add a new text component, use $variable_name (e.g., $block_msg) in the Text field, and define this 'variable_name' as a message in the message.xlsx Excel sheet. Provide the corresponding translations in the languages you want to localise. That way the text will be *automatically* updated based on the choice of the 'global' language in the dialogue box!

# Useful tips #

- Always use the dollar sign "$" before you call a variable in the Text field of the text component (e.g. use "$variable", not "variable")
- Always set the Text field of the text component to "Set every repeat" to update it dyanamically.
- Make sure there are no "hidden" rows/columns in your Excel sheets (i.e., you added text, then removed it, but PsychoPy still interprets there's text there). If you remove rows/columns, use the "Remove rows" button in Excel.
- Make sure your variable names match across their use, remember they are case-sensitive ('TestMessage' does not equal 'testmessage')
- Make sure your loop has the appropriate conditions file and that it is updated in the loop view.


 
