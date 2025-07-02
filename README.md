# Language Localisation demo in PsychoPy (local)

You have created a [PsychoPy experiment](https://psychopy.org/index.html). PsychoPy is great because it is **open-source** (free), and therefore easy to exchange with other researchers or your collaborators, reuse, reproduce, etc.

In your experiment, you **present text to the participant** with instructions or other information. You want to present the text **in the participants' most comfortable language**, as this will enhance their comprehension of the task. You have created your experiment in a **single language**, but you might want to use it in **another language** if your new participants' mother tongue is different. Or you might want to share your experiment with a colleague who works with participants who speak in another language. You could translate word-by-word all your text every time a new language is necessary, but this is tedious and prone to errors. The easiest way to make your experiment scalable and robust is to implement a **language localisation**. This demo and template shows you how to implement it when working in the Builder mode of a PsychoPy local experiment.

## Setup

You work in Builder using Text or TextBox components. You work with Excel sheets to present instructions and text.

## Language Localiser

A language localiser is a **system that dynamically selects the appropriate text based on the participant's preferred language**. Instead of hardcoding text in a single language, you store translations in an Excel sheet or CSV file and refer to them dynamically.

This demo includes:
- A PsychoPy experiment file (.psyexp) that contains a template to illustrate the use of a language localisation.
- A localiser Excel file (`language_localiser.xlsx`) that contains rows for each language and ISO 639 language codes (e.g., English - EN, Spanish - ES, French - FR).
- A localisation Excel file (`messages.xlsx`) that contains rows for each message to display and columns with ISO codes for each translation (e.g., EN: Hello, ES: Hola, FR: Bonjour)
- A `language_settings` routine at the beginning of the experiment which loads the messages variable set at the beginning of the experiment, which can be selected manually or through participant input.
- Builder components that use the `$` syntax to pull the appropriate text based on the current language (e.g., `$welcome_msg`).
- Example routines demonstrating how to set up this logic with minimal code components.

## How does it work

The first routine of the experiment must be the language settings routine. This routine has a code component that only runs Python code (i.e., only works locally). The code is divided into two tabs:
  - BEGIN EXPERIMENT: the code imports the Excel sheet "messages.xlsx" into PsychoPy, creates a dictionary with the messages and allows the variables to be used directly (as global variables in the experiment's environment). This needs to happen **at the beginning of the experiment** because the components to display text require these variables to exist at that stage; otherwise the experiment will crash, looking for a variable not yet defined. At this point all the messages are set to English (EN) by default. This means you **DO NOT NEED to change the code here**, as it will automatically load the most up-to-date version of the messages Excel sheet. This means **the only thing you need to do is to update the 'messages.xlsx' Excel sheet**.  
  - BEGIN ROUTINE: the code updates the language to be used based on the choice made in the dialogue box before the first screen of the experiment actually appears. Because the language settings routine is the first routine of the experiment, this code will **automatically** update all the messages to match the language code as used in the language localiser Excel sheet. Again, this means you **DO NOT NEED to change the code here** to add your language, it will do it automatically for you.

The language settings routine is wrapped in a loop that only runs 1 time, and whose conditions file is the language localiser Excel sheet. This allows to import the available languages by just updating the Excel sheet, without requiring to type any code. The number of rows in the localiser Excel sheet **should match** with the number of conditions that PsychoPy identifies in the loop. If not, click on the loop name and **refresh the Excel sheet by clicking on the green arrows**.

Every text component in the experiment has a variable name in their "Text" field (e.g., "welcome_msg" for the welcome_text component). This variable will be **automatically** updated based on the language choice in the dialogue box. The variable name **MUST BE an existing message as defined in 'messages.xlsx'** before the experiment is launched.

## How to add a new language

If you just want to add a new language without any further modifications (i.e., you do not want to provide other messages than the ones already used), you just need to modify 3 things:
1. In language_localiser.xlsx, add a new **ROW** with your new language and its code. Write this in English (e.g., "Chinese", "CH").
2. In messages.xlsx, add a new **COLUMN**, titled with the code you used in the previous step (e.g., "CH"). For each message, provide the corresponding translation into your desired language.
3. In PsychoPy, go to Experiment Settings and add a new language to the list of languages in the **language field**, with the name being the language you used in Step 1. It is critical that you add your language using '' (e.g., 'Chinese'). If you want your language to be the default choice every time you run the experiment, you just have to **place it at the beginning of the list**.

## Using the language localisation with an Instructions loop

Instructions in PsychoPy are typically shown as loops and the message to show in each iteration of the loop is updated based on an Excel sheet. This is useful to iterate over the instructions without requiring to write code. The repetitions of the loop should be set to 1, and the loop type to 'sequential' (so that the Excel sheet is looped only 1 time and in order, not randomly). Then, once the loop has iterated through all the rows in the corresponding Excel sheet one time and in the order they appear, it will finish and the experiment will progress to the next screen.

This demo includes an instructions routine and instructions loop, as well as an "instructions.xlsx" Excel sheet. The idea is the same as with 'messages.xlsx'. The excel sheet contains **1 column per language available**, and each row corresponds to the corresponding message in that language. The title of the columns must be **identical** and only change in their final part, which is the code of the language (e.g., inst_msg_EN for English, inst_msg_ES for Spanish, etc.). The code **must obviously match the code used in the language localiser** Excel sheet to work appropriately.

## Why Use This Approach?

  ✅ Avoids hardcoding strings into components.
  
  ✅ Reduces risk of translation errors.
  
  ✅ Makes your experiment more reusable and shareable.
  
  ✅ Enables easy switching between languages.
  
  ✅ Supports adding new languages without editing core experiment logic.
  

## Notes

This demo is intended for **offline (local)** PsychoPy experiments. For **online (Pavlovia)** experiments, localisation requires different handling and JavaScript-compatible code.

## Useful 'tips'

- Always use the dollar sign "$" before you call a variable in the Text field of the text component (e.g. use "$variable", not "variable")
- Always set the Text field of the text component to **"Set every repeat"** to update it dyanamically.
- Make sure there are no "hidden" rows/columns in your Excel sheets (i.e., you added text, then removed it, but PsychoPy still interprets there's text there). If you remove rows/columns, use the "Remove rows" button in Excel.
- Make sure your variable names match across their use, remember they are case-sensitive ('TestMessage' does not equal 'testmessage')
- Make sure your loop has the appropriate conditions file and that it is updated in the loop view.

---

Feel free to contribute improvements or suggest other ways of implementing localisation in PsychoPy!


