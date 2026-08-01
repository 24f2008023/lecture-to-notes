# SE2001 — Linux Basic Commands Practice Session
## Study Guide (Week 2 Extra Practice — Online GDB Portal)

> **Session type:** Live coding/practice session on a browser-based "Online GDB" classroom portal. The instructor solves Linux command-line problems live while students follow along. This is **not** a theory lecture — it's hands-on drilling, so this guide is heavy on command-by-command breakdowns.

---

## 0. Session Context & Housekeeping `[0:12 – 2:22]`

Before the actual technical content, a few administrative things were said. These matter for your planning:

| Point | Detail |
|---|---|
| **Course VM** | You must be connected to it *before* the BPT (a graded practice test) is released the next day, or you risk missing it. |
| **BPT (Basic Practice Test?) release pattern** | Released **weekly**, alternating — one week released, next week skipped, then released again. First one from this session releases "tomorrow afternoon." |
| **VMT assignments** | Different from BPT. All VMTs (numbered 1.1 to 1.10, check the grading document) are **already released** — no weekly drip. Deadline for all of them = before the **OPPE exam** (the proctored final practical exam), not a weekly deadline. |
| **New activity introduced this session** | A **bonus, non-graded practice platform** (Online GDB classroom) — separate from the official Course VM. Doing all problems on it before OPPE = **+3 bonus marks**. This mirrors what was done for the C programming course last term. |
| **Why this exists** | The instructor mentioned last cohort's OPPE results were poor, so extra low-stakes practice was added this term. |

**Key terms explained:**
- **Course VM**: A virtual machine (a simulated computer environment) provided by the course where your *actual graded* assignments live and get auto-evaluated.
- **BPT**: A timed practice/graded test released periodically on the Course VM, with a 7-day deadline each time.
- **VMT**: Practice assignments on the Course VM with no weekly deadline — just need to be done before OPPE.
- **OPPE**: Online Proctored Practical Exam — the exam that tests your command-line skills directly, similar in format to these practice problems.

> **Remember This:** BPT = time-bound (7-day deadline each). VMT = no weekly deadline, but must finish before OPPE. The bonus GDB platform = optional but gives +3 marks and is *great* OPPE-style practice.

---

# PART A: Understanding the Practice Platform

## A.1 How the Online GDB Practice Portal Works `[13:41 – 15:09]`

Every problem on this platform gives you **two files**:

1. **`solution.sh`** — the file **you** write. This is a shell script (a text file containing a sequence of terminal commands) where you type the Linux commands needed to solve the problem.
2. **`main.sh`** — the **evaluation/driver script**. You **cannot edit this**. It:
   - Runs your `solution.sh`
   - Checks whether the files/directories your script created match what the question asked for
   - Prints "PASS"/"FAIL" style output by comparing your actual output to a pre-configured expected output

**Why this design exists (the intuition):**
This exactly mirrors how your **real graded Course VM assignments** work. There, you run commands like `sanchro eval` or `sanchro init`, which secretly run a hidden validation script. Here, on the bonus platform, the validation script (`main.sh`) is made **visible** to you on purpose — so you can actually *see* how auto-grading works, which will help you understand *why* your real assignments pass or fail.

**Analogy:** Think of `solution.sh` as your homework answer sheet, and `main.sh` as the teacher's answer key + checking process — except here, unusually, you get to read the teacher's answer key format (not the actual answers, but the *method* of checking).

### The `#!/bin/bash` line — the "Shebang"

At the top of every `solution.sh`, you must write:
```bash
#!/bin/bash
```
- This is called a **shebang** (from "hash-bang", referring to the `#` and `!` characters).
- **What it does:** Tells the Linux operating system *which program* should execute this file. Here, `/bin/bash` is the **file path** to the Bash program (Bash = "Bourne Again SHell", the command-line interpreter).
- **Why it's needed:** Without it, the system wouldn't know whether to treat your file as a Bash script, a Python script, etc. It's essentially a comment (`#` normally means "ignore this line") that the system specifically recognizes as an execution instruction on the very first line.
- **When do you need it?** Only for **executable scripts** (files meant to be *run*, like `.sh` files). You do **NOT** need this in plain text files (like `notes.txt`) that are just meant to store information, not execute commands.
- A student (Vishal) asked whether `bash` is like an executable (`.exe`) — the instructor confirmed: yes, conceptually. Bash is the program/interpreter that reads and executes your script line by line.

> **Remember This:** `#!/bin/bash` = "Hey Linux, run this file using the Bash interpreter." Only needed on script files (`.sh`), not plain data files.

---

# PART B: Problem 1 — Creating a Basic Directory Structure `[6:34 – 48:57]`

### The Goal (Problem Statement)
Create this structure using commands (not manual clicking) inside the current working directory:
```
course/
├── notes.txt          (must contain: "Linux Basics")
├── assignment.txt      (must contain: "Week 1 Assignment")
└── submission/
    ├── student1.txt
    └── student2.txt
```

## B.1 `mkdir` — Make Directory

- **What it is:** A command that creates a new, empty folder (directory).
- **Why it exists:** You need a way to organize files into folders directly from the terminal instead of manually right-clicking in a GUI file explorer.
- **Syntax:** `mkdir <foldername>`
- **Example from the lecture:**
  ```bash
  mkdir course
  ```
  This creates a folder named `course` inside your current location.

**Analogy:** Like creating a new empty folder on your Desktop, except you type its name instead of right-clicking → New Folder.

## B.2 `touch` — Create an Empty File

- **What it is:** A command that creates a new, empty file (or, if the file already exists, updates its "last modified" timestamp without changing its content).
- **Why it exists:** Sometimes you just need a placeholder file to exist (empty), without writing content into it yet.
- **Syntax:** `touch <filename>`
- **Example:**
  ```bash
  touch course/assignment.txt
  ```
  This creates an empty file called `assignment.txt` *inside* the `course` folder — note the `/` used as a path separator (explained below).
- You can create **multiple files in one command**:
  ```bash
  touch student1.txt student2.txt
  ```

## B.3 Paths — Absolute vs. Relative, and the `/` Separator

- A **path** tells the computer *where* a file or folder is located.
- `course/assignment.txt` means: "go into the `course` folder, then find/create `assignment.txt` inside it."
- The instructor did all commands **from the current directory** (without first moving `cd` into `course`), which is why every command explicitly included `course/` as a prefix. This is called working with **relative paths from the outside**.
- **Alternative approach mentioned:** You *could* first `cd course` (move into the folder) and then just write `touch assignment.txt` without the prefix, because you're already inside it. Both approaches give the same final result — just a different way of referencing location.

## B.4 `echo` and Output Redirection (`>`) — Writing Text Into a File

This is one of the most important concepts in this session. Let's build it up slowly.

### Step 1: What does `echo` alone do?
- **What it is:** A command that prints ("echoes back") whatever text you give it.
- **Example:**
  ```bash
  echo hello
  ```
  Output on screen: `hello`
- This kind of output — printed directly to your terminal screen — is called **standard output (stdout)**.

### Step 2: The problem — what if you don't want it on screen, but inside a file?
This is where **redirection** comes in.

- **What it is:** An operator that takes output that would normally go to the screen and sends ("redirects") it into a file instead.
- **The symbol:** `>` (a single greater-than sign)
- **Syntax:**
  ```bash
  echo "Linux Basics" > course/notes.txt
  ```
- **Step-by-step what happens:**
  1. `echo "Linux Basics"` generates the text `Linux Basics` as output.
  2. Instead of printing it to your screen, `>` catches this output.
  3. It checks: does `course/notes.txt` already exist?
     - If **not**, it **creates** the file, then writes the text into it.
     - If it **does exist**, it **overwrites** (completely replaces) the old content with the new text.
- **Critical case-sensitivity lesson from the lecture (`26:00 – 30:00`):** The instructor initially typed `linux basics` in lowercase, but the test failed. The expected output required `Linux basics` (capital L). This teaches you: **exact text matching is case-sensitive.** Always re-read the question statement carefully for exact casing, spacing, and punctuation.

> **Remember This:** `>` = **overwrite** redirection. Creates the file if it doesn't exist; **replaces all content** if it does.

## B.5 Creating Nested Directories with `mkdir`

```bash
mkdir course/submission
```
This creates a `submission` folder *inside* the already-created `course` folder, using the same path-with-slash logic as before.

## B.6 Recap of the Full Solution for Problem 1

```bash
#!/bin/bash
mkdir course
touch course/assignment.txt
echo "Week 1 assignment" > course/assignment.txt
echo "Linux Basics" > course/notes.txt
mkdir course/submission
touch course/submission/student1.txt course/submission/student2.txt
```

**Line-by-line breakdown:**
| Line | What it does |
|---|---|
| `#!/bin/bash` | Tells the system to run this file using Bash |
| `mkdir course` | Creates the `course` folder |
| `touch course/assignment.txt` | Creates an empty `assignment.txt` inside `course` |
| `echo "Week 1 assignment" > course/assignment.txt` | Writes the required text into that file |
| `echo "Linux Basics" > course/notes.txt` | Creates `notes.txt` (via redirection, no separate `touch` needed) AND writes text into it in one line |
| `mkdir course/submission` | Creates the `submission` subfolder inside `course` |
| `touch course/submission/student1.txt course/submission/student2.txt` | Creates two empty files inside `submission` in a single command |

**Beginner note:** You don't strictly need `touch` before `echo >` — `echo "text" > file.txt` will create the file itself if it doesn't already exist. The instructor used `touch` in some places just to demonstrate the concept step by step.

## B.7 The `tree` Command (mentioned, `18:37`)

- **What it is:** A command that visually displays the full folder/file structure as a tree diagram, starting from your current directory.
- **Why it's useful:** After creating a nested structure, it's the fastest way to *visually verify* you built it correctly, instead of guessing.

## B.8 Understanding `main.sh` — How the Evaluator Actually Checks Your Work `[29:38 – 43:10]`

This is a deep-dive the instructor did into reading someone else's Bash script. Let's break every line down.

```bash
rm -rf workspace
mkdir workspace
cd workspace || exit
bash ../solution.sh > /dev/null
```

### `rm -rf workspace`
- **`rm`** = "remove" — deletes files or folders.
- **`-r`** = a **flag/option** meaning "recursive" — if the target is a folder containing other files/folders inside it, delete *all of them* too, not just the empty shell.
- **`-f`** = a flag meaning "force" — don't ask for confirmation, and don't throw an error even if the target doesn't exist.
- **Together (`-rf`):** Forcefully and completely delete the `workspace` folder and everything inside it, silently.
- **Why:** This clears out any leftover files from a *previous* run/attempt, so each test starts from a clean slate.

### `mkdir workspace`
- Creates a fresh, empty `workspace` folder (since the old one was just deleted).

### `cd workspace || exit`
- **`cd`** = "change directory" — moves you *into* a folder.
- **`||`** = the **OR operator**. In shell scripting: `commandA || commandB` means *"run commandA. If (and only if) commandA fails, then run commandB."* If commandA succeeds, commandB is **skipped**.
- **Logic here:** Try to `cd` into `workspace`. If that somehow fails (e.g., folder wasn't created), then `exit` (stop the script immediately) instead of continuing in the wrong location.
- **Contrast with `&&` (AND operator, mentioned at `32:44`):** `commandA && commandB` means *"run commandB **only if** commandA succeeded."* This is the opposite logic — `&&` chains on success, `||` reacts on failure.

  | Operator | Meaning | Analogy |
  |---|---|---|
  | `&&` | Run next command **only if** the previous one succeeded | "Do B, **but only if** A worked" |
  | `\|\|` | Run next command **only if** the previous one failed | "Do B **as backup**, only if A failed" |

### `bash ../solution.sh > /dev/null`
- **`bash ../solution.sh`**: Runs your solution script. The `../` means "go up one directory level first" — because `solution.sh` sits *outside* the `workspace` folder (in the parent directory), since we just `cd`'d into `workspace`.
- **`> /dev/null`**: Redirects any output your script prints to a special "black hole" file (`/dev/null`) that discards everything sent to it. 
  - **Why:** The evaluator doesn't want to see your script's own printed messages cluttering the output — it only cares about the *files/folders* your script created, checked separately below.
  - **Analogy:** `/dev/null` is like a shredder/trash bin — anything sent there vanishes and is never seen again.

### Checking existence with `test -d` and `if`

```bash
if [ -d course ]; then
  echo course
fi
```
- **`[ ... ]`**: Square brackets denote a **conditional test** (technically calls the `test` command).
- **`-d`**: A flag meaning "check if this is a **directory**" (folder). Returns *true* if it exists and is a directory, *false* otherwise.
- **`if [ -d course ]; then ... fi`**: "**If** the `course` directory exists, **then** do the following, **end if**."
- If true → `echo course` prints the word `course` (this becomes part of the "your output" that gets compared to "expected output").
- If false → nothing is printed at all (that line of the output is just blank/missing).

The same pattern (`-d` for directories, `-f` for files, further down) repeats to check `course/submission`, then each expected file.

### Checking file existence with `test -f`
```bash
if [ -f course/notes.txt ]; then
  cat course/notes.txt
fi
```
- **`-f`**: Checks if the target is a **file** (not a directory) and it exists.
- **`cat`** = "concatenate" — prints the **contents** of a file to the screen.
  - **Difference between `cat` and `echo`** (explained after a student's question at `54:01`): `echo "notes.txt"` would just print the literal text `notes.txt` — it does NOT read files. `cat notes.txt` reads the actual **file** named `notes.txt` and prints whatever text is *inside* it. This is a very common beginner confusion — `echo` prints what you type; `cat` prints what's stored inside a file you name.

### Putting it together — how validation logic works
The evaluator script systematically:
1. Cleans the workspace.
2. Runs your solution.
3. Checks each expected directory exists → prints its name if so.
4. Checks each expected file exists → prints its name if so.
5. Prints the **contents** of each expected file (via `cat`) if it exists.
6. All of this printed output becomes "your output," which is then string-compared against a pre-written "expected output." If they match **exactly**, the test passes.

**Live demo of failure (`37:15 – 42:16`):** The instructor deliberately renamed `course` to `course1` in the solution. Because `[ -d course ]` then evaluated to false, **none** of the dependent `if` blocks executed — so the "your output" ended up blank/empty, causing a mismatch against expected output. This is a great debugging insight: **one wrong name early in the structure can cascade and make everything downstream silently skip.**

> **Remember This:** 
> - `-d` tests for **directory** existence, `-f` tests for **file** existence.
> - `cat` reads file *contents*; `echo` just prints literal text you typed.
> - `> /dev/null` throws away output you don't want to see.
> - `if [ condition ]; then ...; fi` is the basic conditional structure in Bash.

## B.9 Navigating Directories: `cd`, `cd ..`, `cd -`, and `pwd` `[43:00 – 48:57]`

| Command | Meaning | Example |
|---|---|---|
| `cd foldername` | Move **into** a folder | `cd course` |
| `cd ..` | Move **up one level** to the parent folder | If you're in `course/submission`, `cd ..` takes you to `course` |
| `cd ../..` | Move up **two** levels at once (double-dot + slash + double-dot) | Chains multiple "up" moves in one command |
| `cd` (no argument) | Return straight to your **home directory** | — |
| `cd -` | Return to the **previous** directory you were in before your last `cd` | Like a "back" button |
| `pwd` | "Print Working Directory" — shows your **current** folder location | Useful when you're lost about where you are |

**A student's important question (`44:00`):** *"How should we know which directory we're in?"* → Answer: use `pwd`. However, on this specific online GDB platform, there's no live interactive terminal to run `pwd` and see immediate feedback — you have to track it mentally by reading your own script.

**Another important clarification (`45:03`, from student Pavan):** *Does it matter what directory you end up in after your script finishes?* 
**Answer: No.** The evaluator (`main.sh`) only checks whether the **required files/folders exist somewhere in the expected relative location** — your *ending* location (current directory) when the script finishes is irrelevant to pass/fail. This is a relief for beginners who worry about "cleaning up" their `cd` navigation.

> **Remember This:** Returning to your starting folder at the end of a script is a nice practice/hygiene habit, but **it does not affect grading**. Grading only checks the final file structure that exists on disk.

### Practice Problem 1 — Summary
- **Concepts covered:** `mkdir`, `touch`, `echo`, `>` redirection, path notation (`folder/file`), `cd`/`cd ..`/`pwd`, reading evaluator logic (`test -d`, `test -f`, `if`, `&&`, `||`, `cat`, `/dev/null`).
- **Key takeaway:** Nearly every Linux "create structure" problem is just a sequence of `mkdir` + `touch`/`echo >` calls, executed either from outside (full paths) or from inside (after `cd`) — both work identically.
- **Common mistakes:** Case-sensitivity in text content (`Linux` vs `linux`); forgetting a folder name matches exactly; assuming ending location matters (it doesn't).
- **Practice Questions:**
  1. Write a one-line command to create a file called `report.txt` containing exactly the text `Draft v1` (mind the capitalization).
  2. What's the difference between `[ -d folder ]` and `[ -f folder ]`? What happens if you use `-f` on something that's actually a directory?
  3. If `cmdA && cmdB` and `cmdA` fails, does `cmdB` run? What about `cmdA || cmdB`?

---

# PART C: Problem 2 — Brace Expansion & Appending Text `[56:52 – 1:10:00]`

### The Goal
Create many similarly-named files/folders (e.g., 20 student submission files) **without typing 20 separate commands**, and learn to **add a second line** to a file without erasing the first line.

## C.1 Brace Expansion — `{1..20}`

- **What it is:** A shell feature that automatically expands a range or list into multiple separate "words" (arguments) that a command then runs against, one by one.
- **Why it exists:** Manually typing `touch student1.txt`, `touch student2.txt`, ... `touch student20.txt` (or worse, for 100+ students) is slow and error-prone. Brace expansion generates the whole sequence in one line.
- **Syntax:** `{start..end}`
- **Example:**
  ```bash
  touch student{1..20}.txt
  ```
  **How it works step by step:**
  1. Bash sees the pattern `student{1..20}.txt`.
  2. It expands `{1..20}` into the list: `1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20`.
  3. It then combines this list with the surrounding text (`student` before, `.txt` after) to build 20 separate filenames: `student1.txt`, `student2.txt`, ..., `student20.txt`.
  4. `touch` then receives all 20 filenames as separate arguments and creates all 20 empty files in one shot.

**Analogy:** It's like a mail-merge template — `student{1..20}.txt` is the template, and Bash "fills in the blank" 20 times automatically.

> **Remember This:** `{1..20}` is a **range** (inclusive of both ends). You can use this pattern with any command, not just `touch` — e.g., `mkdir student{1..20}` would create 20 folders.

## C.2 Appending Text — `>>` (Double Arrow) vs `>` (Single Arrow)

This directly follows from the redirection concept in Problem 1, but solves a new problem: *what if you need to add a SECOND line to a file, without deleting the first line?*

- **The problem demonstrated live (`1:01:43 – 1:02:13`):** If you run `echo "line 1" > file.txt` and then run `echo "line 2" > file.txt` again, the **second command completely erases "line 1"** and replaces it — because `>` always **overwrites**.
- **The fix: `>>` (append redirection)**
  - **What it is:** Like `>`, but instead of erasing existing content, it adds the new text to the **end** of the file, preserving everything already there.
  - **Syntax:**
    ```bash
    echo "Line 1: Linux Basics" > schedule.txt
    echo "Week 1 Linux" >> schedule.txt
    ```
  - **Step-by-step:**
    1. First command: creates `schedule.txt` (didn't exist before) and writes Line 1.
    2. Second command: since `schedule.txt` now exists, `>>` does **not** erase it — it adds the new text as a **new line**, right after existing content.
  - A student asked (`1:02:04`) whether you need to manually add a newline character/backslash between appended lines — **Answer: No.** Each separate `echo ... >>` call automatically starts on a new line; you don't need to manually insert `\n`.

| Operator | Behavior | When to use |
|---|---|---|
| `>` | **Overwrite** — erases existing content, writes fresh | First time writing to a file, or when you deliberately want to replace everything |
| `>>` | **Append** — adds to the end, keeps old content | Adding additional lines/data without destroying what's already there |

> **Remember This:** This is one of the most commonly confused pairs in Bash. `>` = replace. `>>` = add on top. Using the wrong one is a very common beginner mistake that silently deletes data.

## C.3 The "no copy-paste" Rule on the Portal `[59:36]`

The instructor mentioned the platform **disables copy-paste** deliberately, forcing students to actually type out commands themselves — this is intentional friction to build muscle memory, since many students otherwise just copy-paste answers without understanding.

## C.4 Recap — Solution Pattern for Problem 2

```bash
#!/bin/bash
mkdir "training portal"          # or similar nested folder, per question text
cd "training portal"
echo "Welcome to Linux Training" > announcement.txt
echo "Week 1: Linux Basics" > schedule.txt
echo "Week 2: Scripting" >> schedule.txt
mkdir submissions
cd submissions
touch student{1..20}.txt
```

**Line-by-line:**
| Line | Purpose |
|---|---|
| `mkdir "training portal"` | Creates the top folder (quotes used if the name has a space) |
| `cd "training portal"` | Moves inside it |
| `echo "..." > announcement.txt` | Creates + writes first-time content (overwrite is fine since file is new) |
| `echo "..." > schedule.txt` | Creates file, writes line 1 |
| `echo "..." >> schedule.txt` | **Appends** line 2 without erasing line 1 |
| `mkdir submissions` | Creates the submissions subfolder |
| `cd submissions` | Moves inside it |
| `touch student{1..20}.txt` | Creates 20 empty files in one command using brace expansion |

### Practice Problem 2 — Summary
- **Concepts:** Brace expansion `{start..end}`, append redirection `>>` vs overwrite `>`.
- **Common mistakes:** Using `>` a second time and accidentally erasing prior content; forgetting brace expansion needs no spaces inside `{1..20}`.
- **Practice Questions:**
  1. Write one command to create 50 files named `log1.txt` through `log50.txt`.
  2. You already have a file `diary.txt` with one line in it. Write the command to add a second line **without losing the first**.
  3. What would `echo "test" > file.txt` followed by `echo "test2" > file.txt` leave inside `file.txt`?

---

# PART D: The `diff`-style Comparison Output — Reading Pass/Fail Results `[1:06:29 – 1:08:14]`

When your test fails, the portal shows a **colored difference view** comparing your output to the expected output.

- **Red / minus (`-`) lines:** Something the **expected output has, but yours is missing**. (i.e., you need to *add* this.)
- **Green / plus (`+`) lines:** Something **extra in your output** that shouldn't be there, or doesn't match. (i.e., something you need to *fix/remove/correct*.)

This maps directly to the real `diff` command in Linux:
- **`diff file1 file2`**: Compares two files line by line and shows exactly what's different between them.
- **Why this matters for OPPE:** The real Course VM assignments show this **exact same color-coded pass/fail style** output (e.g., "Test case 1: pass", "Test case 2: fail" alongside colored diffs) when you run the official evaluation command. Getting comfortable reading this here directly transfers to your real graded work.

> **Remember This:** In diff-style output: **Red = missing (add it)**, **Green = extra/wrong (fix it)**. This is universal across most diff/comparison tools, not just this platform.

---

# PART E: File Extensions — Creating Non-`.txt` Files `[1:09:04 – 1:14:17]`

Students asked whether other file types (Excel, PDF, Python, C) can be created the same way.

- **Answer: Yes.** `touch` (and `echo >`) work with **any filename + extension** — Linux itself doesn't inherently restrict file types by extension; the extension is just a naming convention that *other programs* use to know how to open the file.
  ```bash
  touch data.xlsx
  touch script.py
  touch program.c
  touch summary.pdf
  ```
- **Important limitation clarified:** You can create a file with `.pdf` extension and even see its raw content (if it were readable text) via `cat`, but you **cannot visually render/view** a PDF, Excel sheet, or any binary/formatted file *inside the terminal*. The terminal only understands **plain text**. To actually *view* such files properly, you need a GUI application (e.g., a PDF viewer, Excel).
- **Opening files in another application from the terminal:**
  ```bash
  notepad somefile.txt
  ```
  - This is an **application-specific command** — `notepad` here is a command your terminal recognizes as "launch the Notepad app and open this file in it." 
  - **Key insight:** There's no universal "open file" command — each application has its **own specific launch command** (e.g., `chrome` for the Chrome browser). You must look up/know the correct command for whichever app you want to use.
  - This only works if you're on a system with a **GUI** (Graphical User Interface) enabled underneath the terminal. Some Linux setups run **headless** (GUI completely disabled), in which case everything, including viewing PDFs, must be done through text-based terminal tools only.

> **Remember This:** Terminal = text only. To view "binary"/formatted files (PDF, Excel, images) properly, you need a GUI app, launched via that app's specific terminal command.

---

# PART F: File Permissions — `chmod` and Octal Notation `[1:32:46 – 1:51:33]`

This is the most conceptually dense part of the session (**Problem 4**). Take this slowly.

## F.1 What Are Permissions? — The Big Picture

Every file/folder in Linux has rules about **who can do what** to it. This exists because Linux is a **multi-user** operating system — many different people (or even different automated programs) might access the same machine, and you don't want everyone to be able to read/edit/run everything.

**Analogy:** Think of a shared office filing cabinet. Some drawers only *you* (the owner) can open and edit. Some drawers your *team* (group) can look into but not change. Some drawers *anyone in the building* (others) can peek at but not touch.

## F.2 The Three Permission Types

| Permission | Symbol | What it allows |
|---|---|---|
| **Read** | `r` | View the file's content (or list a folder's contents) |
| **Write** | `w` | Modify/edit the file's content (or add/remove items in a folder) |
| **Execute** | `x` | **Run** the file as a program/script (or enter into a folder, for directories) |

## F.3 The Three User Categories

| Category | Meaning |
|---|---|
| **Owner** | The specific user who created/owns the file |
| **Group** | A defined set of users who share some collective access |
| **Others** | Everyone else on the system |

## F.4 Reading `ls -la` Permission Output

Running `ls -la` shows something like:
```
-rwxr-xr-x  1 user group  ... filename
```
Breaking down the first 10 characters:
- **Character 1**: File type (`-` = regular file, `d` = directory)
- **Characters 2–4**: Owner's permissions (`rwx` = read, write, execute all allowed)
- **Characters 5–7**: Group's permissions (`r-x` = read + execute, no write — the middle `-` means write is *denied*)
- **Characters 8–10**: Others' permissions (`r-x` = same as group here)

A `-` in any position means that specific permission is **not granted**.

## F.5 Octal (Numeric) Notation for Permissions — The Core Trick

Instead of writing out `rwx` explicitly, Linux lets you represent each category's permission set as a **single number from 0–7**, using **binary logic**:

- Each of the 3 permission slots (r, w, x) is either **ON (1)** or **OFF (0)**.
- Since there are 3 slots, there are `2³ = 8` possible combinations (0 through 7).

| Binary | Octal (Decimal) | Meaning | r | w | x |
|---|---|---|---|---|---|
| 000 | 0 | No permission | ✗ | ✗ | ✗ |
| 001 | 1 | Execute only | ✗ | ✗ | ✔ |
| 010 | 2 | Write only | ✗ | ✔ | ✗ |
| 011 | 3 | Write + Execute | ✗ | ✔ | ✔ |
| 100 | 4 | Read only | ✔ | ✗ | ✗ |
| 101 | 5 | Read + Execute | ✔ | ✗ | ✔ |
| 110 | 6 | Read + Write | ✔ | ✔ | ✗ |
| 111 | 7 | Read + Write + Execute (all) | ✔ | ✔ | ✔ |

**How to build a 3-digit permission code:** You write **three digits in a row**: [Owner][Group][Others].

**Example:** `755` means:
- Owner (`7`) → read, write, execute (all permissions)
- Group (`5`) → read, execute (no write)
- Others (`5`) → read, execute (no write)

**Example:** `600` means:
- Owner (`6`) → read, write only
- Group (`0`) → nothing
- Others (`0`) → nothing

## F.6 The `chmod` Command — Changing Permissions

- **What it is:** "Change mode" — the command used to modify a file/folder's permissions.
- **Syntax:**
  ```bash
  chmod <octal_code> <filename_or_pattern>
  ```
- **Example:**
  ```bash
  chmod 755 script.sh
  ```
  This sets: owner = full access (7), group = read+execute (5), others = read+execute (5).

### Applying `chmod` to Multiple Files with Wildcards (`*`) — Pattern Matching

```bash
chmod 755 scripts/*.sh
```
- **`*`** = a **wildcard** — matches "anything" (zero or more characters).
- **`*.sh`** means: "any filename, as long as it **ends with** `.sh`". 
  - **How it works:** Bash looks inside the `scripts` folder, finds every file whose name ends in `.sh` (regardless of what comes before that), and applies `chmod 755` to *all* of them in a single command.
  - This is a basic form of **pattern matching / regular expression-like behavior** — very useful when you don't want to (or can't) list every filename individually.
  - **Important distinction:** This only matches files ending exactly in `.sh`. A file like `notes.txt` would **not** be affected, even if it's in the same folder.

## F.7 Full Worked Example from the Lecture

**Requirement (paraphrased):**
- All **script files** (`.sh`): owner = read/write/execute, group = read/execute, others = read/execute → **755**
- All **config files** (`.conf`): owner = read/write, group = none, others = none → **600**
- **`readme.txt`**: owner = read/write, group = read only, others = read only → **644**

**Commands:**
```bash
chmod 755 scripts/*.sh
chmod 600 config/*.conf
chmod 644 readme.txt
```

**Step-by-step reasoning for each:**
1. `755` for scripts → owner needs to *run* the script (execute) and *edit* it (write) and *read* it. Group/others just need to run and read it, not modify it (security: don't let random users edit executable scripts).
2. `600` for config files → very restrictive. Config files often hold sensitive settings, so only the owner should read/write them; nobody else should even be able to peek.
3. `644` for readme → a typical "informational" file. Owner can edit it; everyone else can only read it (nobody but the owner should be able to change documentation).

## F.8 Shortcut Symbolic Modifications (mentioned briefly, `1:41:38`)

Besides octal numbers, you can also adjust permissions symbolically:
- `chmod +x filename` → **adds** execute permission (for the owner, by default)
- `chmod +w filename` → **adds** write permission
- `chmod -x filename` → **removes** execute permission (the `-` here means "take away", not "no permission")

The instructor noted the **numeric/octal method is generally more convenient** once you're comfortable with it, since it sets all three categories in one clean shot.

> **Remember This — Permission Cheat Sheet:**
> - `r=4, w=2, x=1` → add them up per category to get the digit (e.g., r+w = 4+2 = 6)
> - Order is always **Owner, Group, Others**
> - `755` = common for **executable scripts** (owner full, others can run+read)
> - `644` = common for **regular readable files** (owner can edit, others read-only)
> - `600` = common for **private/sensitive files** (owner only, no one else)
> - `chmod <code> pattern*.ext` applies permissions to multiple matching files at once

### Practice Problem 4 — Summary
- **Concepts:** `rwx` meaning, owner/group/others, binary→octal permission math, `chmod`, wildcard pattern matching (`*.ext`).
- **Common mistakes:** Mixing up the order (owner, group, others — always in that order); forgetting that `-` in `ls -la` output means "denied," not "unknown"; using `*` incorrectly (e.g., `*` alone would match everything, not just `.sh` files).
- **Practice Questions:**
  1. What octal code gives the owner full access, and read-only to everyone else, with **no** access for the group at all?
  2. Convert `rwxr--r--` into its octal equivalent.
  3. Write a command that gives **execute** permission to every `.py` file in a folder called `bin`, without changing read/write permissions. (Hint: symbolic `chmod +x`, not octal, since octal would reset everything.)

---

# PART G: Brief Preview — Problems 7–9 (Not Solved in Depth) `[1:53:05 – 1:56:00]`

The instructor only *previewed* these, encouraging self-practice:

- These problems introduce an **`init.sh`** file (in addition to `solution.sh` and `main.sh`) — a script that **pre-builds** an initial folder structure for you automatically, similar to the real Course VM's `sanchro init` command (which sets up a starting scaffold for your actual graded assignments).
- Your job in `solution.sh` for these problems is **not** to build the structure from scratch, but to **modify/manipulate** what `init.sh` already created:
  - **`cp file1 file2 destination/`** — the **copy** command: duplicates a file into another location (originals stay intact).
  - **`mv sourcefile destination/`** — the **move** command: relocates a file (also used to **rename** a file, since renaming = "moving" it to a new name in the same folder).
  - **Symbolic links and hard links** (conceptually introduced, not covered in depth here) — special pointer-like files:
    - A **symbolic link** ("symlink") is like a shortcut — a small file that just points to another file's location.
    - A **hard link** is a direct additional name for the *same* underlying file data (more advanced; will likely be covered in a future session in more depth).
  - Additional `chmod` permission changes layered on top of the copied/moved files.

> **Note:** Since these weren't worked through command-by-command in this session, revisit this section once the topic is covered fully in a later class or the weekly PDF — this guide will need a follow-up addendum then.

---

# PART H: Full Command Reference Table (Everything Covered This Session)

| Command / Symbol | Category | What it does |
|---|---|---|
| `mkdir foldername` | Create | Makes a new folder |
| `mkdir -p a/b/c` | Create | Makes nested folders in one go, creating any missing parent folders along the path |
| `touch file.txt` | Create | Makes an empty file (or updates timestamp if it exists) |
| `echo "text"` | Output | Prints text to the screen |
| `echo "text" > file` | Redirect | Writes text into a file, **overwriting** existing content |
| `echo "text" >> file` | Redirect | **Appends** text to the end of a file, keeping old content |
| `cat file` | Read | Prints the full contents of a file to the screen |
| `cd folder` | Navigate | Moves into a folder |
| `cd ..` | Navigate | Moves up one folder level |
| `cd -` | Navigate | Returns to the previous directory |
| `pwd` | Navigate | Shows current directory path |
| `ls -la` | List | Lists all files/folders including hidden ones, with permission details |
| `rm -rf folder` | Delete | Forcefully and recursively deletes a folder and everything inside it |
| `tree` | Visualize | Displays folder structure as a tree diagram |
| `chmod 755 file` | Permissions | Changes read/write/execute permissions using octal code |
| `chmod +x file` | Permissions | Adds execute permission symbolically |
| `cp src dest` | Copy | Duplicates a file |
| `mv src dest` | Move/Rename | Relocates or renames a file |
| `{1..20}` | Brace expansion | Generates a numeric sequence for use in filenames |
| `*.ext` | Wildcard | Matches any filename ending in `.ext` |
| `#!/bin/bash` | Script header | Declares which interpreter should run the script (shebang) |
| `[ -d name ]` | Test | Checks if `name` is an existing directory |
| `[ -f name ]` | Test | Checks if `name` is an existing file |
| `if [ cond ]; then ...; fi` | Conditional | Runs commands only if the condition is true |
| `cmdA && cmdB` | Logic | Runs `cmdB` only if `cmdA` **succeeded** |
| `cmdA \|\| cmdB` | Logic | Runs `cmdB` only if `cmdA` **failed** |
| `> /dev/null` | Redirect | Discards output completely (sends it to a "black hole") |

---

# Overall Session Summary

- This was a **hands-on drilling session**, not a concept lecture — its purpose was **repetition and muscle memory** on foundational Linux commands before the OPPE.
- The four "pillars" practiced: **(1)** creating structures (`mkdir`, `touch`, `echo >`), **(2)** scaling up efficiently (`{range}` brace expansion, `>>` append), **(3)** understanding how auto-grading scripts work (`if`, `-d`/`-f` tests, `&&`/`||`), **(4)** permissions (`chmod`, octal math).
- **Direct relevance to your BPT/OPPE:** The evaluation mechanism shown here (`main.sh` reading directory/file existence and content, printing colored diffs) is explicitly the **same style of evaluation** used on your real graded Course VM assignments (via `sanchro eval`/`sanchro init`) — so mastering *how to read* this kind of script is as valuable as mastering the commands themselves.
- A **surprise quiz** was conducted near the end (~`1:56:10` onward) covering Week 1 material — if you have access to quiz results/questions separately, review those alongside this guide.

## Final "Remember This" — Exam-Critical Points
1. `>` overwrites, `>>` appends. Mixing these up silently destroys data — a classic exam trap.
2. Case-sensitivity and exact text matching matter in every auto-graded question — read problem statements character-by-character.
3. `-d` tests directories, `-f` tests files — using the wrong flag makes conditions silently fail.
4. Octal permission digits = Owner, Group, Others, in that fixed order — memorize `r=4, w=2, x=1`.
5. `{1..N}` brace expansion + wildcard `*.ext` pattern matching are the two biggest "avoid manual repetition" tools — expect OPPE questions designed specifically to test whether you use these instead of typing everything by hand.
6. Your script's **ending directory location does not affect grading** — only the final file/folder structure on disk matters.
7. The shebang `#!/bin/bash` goes on script files only, not plain text data files.

## Suggested Next Steps
- Redo Problems 1–4 **from scratch, without watching**, timing yourself.
- Attempt Problem 3 (the `student1..20` nested folders + `work.txt` variant) fully on your own — it was left as self-practice in the lecture.
- When Problems 7–9 (`cp`, `mv`, symbolic/hard links) are covered in a future session, request a follow-up guide to append to this one.
