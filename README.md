How to create a remote codespace for running ibex?
---
- Fork this repository
- Then, open forked repo in your github
- click on **code** on top right of repo
- create a new codespace by pressing '+'
    - if required, with three dots option, choose **new with options** and change machine type to 4 cores 
- Patiently wait for the codespace to setup (will take good 10 to 15 mins)
- Now inside the workspace, click on visual studio code's file explorer, and go to this folder: **home/FYP/**
- now in terminal **cd FYP/ibex**.
- The system setup is done.
- Now run the command to test from **home/FYP/FYP/ibex** directory: **./run.sh**
- if there are no errors, then you will see the output as **yay!All successfully done**

## How to write the test code and analyze through profiling?
- go to **examples/sw/simple_system/hello_test/**
- write your code in **hello_test.c**
- then from ibex as root: run **./run.sh**
- Now in this folder ** examples/sw/simple_system/hello_test/** these files will be created:
-  **function_table.csv**: list of all functions with start address and return address obtained by parsing obj_dump
-   **output.csv**: list of all functions with no. of times they are called, and time taken and amount of cycles: obtained by parsing trace_core_lof in ibex folder with reference from function_table.csv

---
### pls make sure to stop codespace after use as there are only limites hrs codespace can run for free!!


files to be changed for nnom:
simulator_control.vs present in shared->rtl (already updated in docker)
also replace the common and nnom with v2 github in their respective repo.
## make sure too change path in common.mk
run.sh also (updated in docker)
