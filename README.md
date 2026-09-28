# EcoPile Expert — Local Installation and Running Guide

EcoPile Expert is a rule-based home-compost troubleshooting system developed using SWI-Prolog.

The application provides a graphical user interface that asks 23 questions about a compost pile. It uses 25 source-backed rules to identify possible problems and recommend corrective actions.

## Project Files

Ensure all the following files are located in the same folder:

```text
EcoPileExpert/
├── gui.pl
├── main.pl
├── knowledge_base.pl
├── inference_engine.pl
├── test_system.pl
├── README.md
└── .gitignore
```

File purposes:

- `gui.pl` — graphical user interface
- `main.pl` — optional command-line interface
- `knowledge_base.pl` — 25 expert-system rules
- `inference_engine.pl` — rule-matching and fact-derivation logic
- `test_system.pl` — automated tests

## System Requirements

The system requires:

- Windows 10 or Windows 11
- SWI-Prolog 10.0.2 or a compatible version
- Approximately 100 MB of available storage
- A graphical desktop environment

Python and external Prolog packages are not required.

## Step 1: Download the Project

### Option A — Download from GitHub

1. Open the EcoPile Expert GitHub repository.
2. Select the green **Code** button.
3. Select **Download ZIP**.
4. Open the downloaded ZIP file.
5. Extract the project folder.
6. Open the extracted `EcoPileExpert` folder.

### Option B — Clone with Git

If Git is installed, open PowerShell and run:

```powershell
git clone <repository-url>
cd EcoPileExpert
```

Replace `<repository-url>` with the actual EcoPile Expert GitHub repository URL.

## Step 2: Install SWI-Prolog

Download the stable 64-bit Windows version of SWI-Prolog:

https://www.swi-prolog.org/download/stable

During installation:

1. Use the default installation options.
2. Associate `.pl` files with SWI-Prolog if asked.
3. Enable the option to add SWI-Prolog to the system path if it is available.
4. Complete the installation.
5. Close and reopen PowerShell or Visual Studio Code.

## Step 3: Verify the Installation

Open PowerShell and run:

```powershell
swipl --version
```

Expected output will be similar to:

```text
SWI-Prolog version 10.0.2 for x64-win64
```

The exact version number may be different if a newer compatible version is installed.

## Step 4: Open a Terminal in the Project Folder

### Using Visual Studio Code

1. Open Visual Studio Code.
2. Select **File → Open Folder**.
3. Select the extracted `EcoPileExpert` folder.
4. Select **Terminal → New Terminal**.

### Using Windows File Explorer

1. Open the extracted `EcoPileExpert` folder.
2. Right-click an empty area inside the folder.
3. Select **Open in Terminal**.

The terminal path should end with the project-folder name:

```text
PS C:\Users\User\Downloads\EcoPileExpert>
```

You can confirm that the required files are present by running:

```powershell
Get-ChildItem
```

## Step 5: Run the Graphical Application

From inside the project folder, run:

```powershell
swipl -q -s gui.pl
```

The EcoPile Expert graphical interface should open.

Do not close the PowerShell terminal while using the application. Closing the terminal will also stop the Prolog program.

## How to Use the GUI

The application displays one question at a time.

For each question:

1. Open the answer dropdown.
2. Select the answer that best describes the compost pile.
3. Select **Next**.
4. Continue until all 23 questions have been answered.

The question progress is displayed in the interface:

```text
Question 1 of 23
```

After question 23, the results area displays:

- The number of matching rules
- The identifiers of the rules that fired
- The problem category
- The diagnosis
- The recommended corrective action
- The knowledge sources supporting the conclusion

Use the scroll bar to read all the recommendations.

## GUI Buttons

### Next

Saves the selected answer and displays the next question.

After question 23, the **Next** button becomes disabled.

### Restart

Clears the current answers and starts a new assessment from question 1.

### Exit

Closes EcoPile Expert.

## Example Assessment

To test a wet compost pile with an odor problem, select answers representing:

- Soggy or excessively wet moisture
- Rotten-egg or sulfur smell
- Not turned recently
- Exposure to significant rain
- Poor drainage
- Insufficient brown material

After the final question, the results should include several of these rules:

```text
r02
r03
r09
r10
r11
r12
r13
```

The exact set depends on all the answers supplied during the assessment.

## Running the Command-Line Version

A command-line version is also included as a fallback.

Run:

```powershell
swipl -q -s main.pl
```

For numbered questions, enter the number beside the required answer:

```text
1. Dry
2. Balanced - like a wrung-out sponge
3. Soggy or excessively wet

Your choice: 3
```

For yes-or-no questions, enter:

```text
yes
```

or:

```text
no
```

The command-line version displays the same rule-based diagnoses and recommendations.

## Running the Automated Tests

Open a terminal inside the project folder and run:

```powershell
swipl -q -s test_system.pl -g run_tests -t halt
```

Successful tests are represented by dots. There should be no failed-test or error messages.

For detailed test output, run:

```powershell
swipl -s test_system.pl -g run_tests -t halt
```

The automated tests verify:

- The knowledge base contains exactly 25 rules
- Every rule ID is unique
- Every rule contains at least one condition
- Every rule has a valid knowledge source
- Bad odors produce the correct derived facts
- Animal-attracting materials are detected
- Dry-pile problems are identified
- Wet-pile problems are identified
- Odor problems are identified
- Heating problems are identified
- Unsuitable materials are detected
- Pest problems are identified
- Finished compost is recognized
- A normal active pile does not produce unnecessary warnings

## Troubleshooting

### The `swipl` command is not recognized

If PowerShell displays:

```text
swipl : The term 'swipl' is not recognized
```

Try the following:

1. Close PowerShell or Visual Studio Code.
2. Reopen it.
3. Run `swipl --version` again.

If the error remains, reinstall SWI-Prolog and ensure it is added to the Windows system path.

### The GUI does not open

Confirm that `gui.pl` is present:

```powershell
Get-ChildItem gui.pl
```

Check the GUI source file for syntax errors:

```powershell
swipl -q -g "consult('gui.pl'),halt"
```

If no message appears, the file loaded successfully.

Then run:

```powershell
swipl -q -s gui.pl
```

### XPCE cannot be loaded

Check that the SWI-Prolog graphical library is available:

```powershell
swipl -q -g "use_module(library(pce)),writeln('XPCE ready'),halt"
```

Expected output:

```text
XPCE ready
```

If XPCE is unavailable, reinstall the complete 64-bit version of SWI-Prolog.

### A project file cannot be found

All Prolog files must be in the same folder:

```text
gui.pl
main.pl
knowledge_base.pl
inference_engine.pl
test_system.pl
```

Make sure the terminal is opened inside that folder before running the application.

### The GUI opens but does not produce recommendations

Check that `knowledge_base.pl` contains all 25 rules and that `inference_engine.pl` is in the same folder.

Run the automated tests:

```powershell
swipl -q -s test_system.pl -g run_tests -t halt
```

If any tests fail, review the error displayed in the terminal.

### Stop the application from the terminal

Close the GUI using the **Exit** button.

If the interface is unresponsive, return to the terminal and press:

```text
Ctrl+C
```

Then follow the SWI-Prolog prompt to abort the program.

## Quick Command Reference

Run the graphical interface:

```powershell
swipl -q -s gui.pl
```

Run the command-line interface:

```powershell
swipl -q -s main.pl
```

Run the automated tests:

```powershell
swipl -q -s test_system.pl -g run_tests -t halt
```

Check the SWI-Prolog version:

```powershell
swipl --version
```

Check XPCE availability:

```powershell
swipl -q -g "use_module(library(pce)),writeln('XPCE ready'),halt"
```
