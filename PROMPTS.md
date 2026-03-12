## AI Usage Log

### Interaction 1: Debugging Setup Errors
**1. Context:**  
I was running the "Environment Verification" section of the notebook and encountered a `NotImplementedError`, which stopped the execution of the notebook.

**2. Prompt(s):**  
"me esta dando error este notebook por q sera? [Attached code from the environment check cell]"

**3. Relevant Output:**  
The AI explained that the `NotImplementedError` is an intentional placeholder created by the instructor (`raise NotImplementedError(...)`). It advised me to delete that specific line and replace it with my own code to complete the assignment.

**4. Validation:**  
I verified this by deleting the `raise` line, writing `print("test")` in its place, and running the cell again. The error disappeared, confirming the AI's explanation of the notebook's structure was correct.

**5. Adaptations:**  
No code adaptations were needed from the AI. I just followed the instructions to delete the placeholder and wrote my own system check as required by the assignment.

**6. Final Decision:**  
*Used*. The conceptual explanation solved my blocker and allowed me to continue safely without thinking my Python installation was broken.

---

### Interaction 2: FastF1 Cache Permission Error
**1. Context:**  
While executing the `fastf1.Cache.enable_cache()` block, my system threw a `PermissionError: [WinError 5] Access denied: 'C:\Users\data'`. I needed to fix the file path to enable the cache.

**2. Prompt(s):**  
"con este codigo: [Attached FastF1 cache code], me da este error: PermissionError: [WinError 5] Acceso denegado: 'c:\Users\data'"

**3. Relevant Output:**  
The AI pinpointed that `os.path.join(os.path.dirname(os.getcwd()), '..', 'data')` was navigating too far up my directory tree into a restricted Windows folder because my notebook was placed in the `Downloads` folder instead of the original course directory. It provided a modified `cache_path` using just `os.getcwd()`.

**4. Validation:**  
I validated this by printing `os.getcwd()` to ensure it pointed to my current working directory in `Downloads`. I then checked Windows File Explorer to confirm that a new folder named `data/fastf1_cache` was successfully created there without requiring admin rights.

**5. Adaptations:**  
I modified the AI's suggested script to ensure the `data` folder was ignored by `.gitignore` so I wouldn't accidentally upload heavy cache files to my repository later.

**6. Final Decision:**  
*Modified*. The AI's root cause analysis was perfect, but I adjusted the folder structure to fit my personal workspace setup.

---

### Interaction 3: Missing Module Exception (NameError)
**1. Context:**  
While trying to run the package version check loop in the "Environment Verification" section, my notebook threw a `NameError: name 'importlib' is not defined`. I didn't know why, since I was running the cell exactly as provided.

**2. Prompt(s):**  
"por que me esta dando este error?: NameError Traceback (most recent call last) [Attached code snippet] NameError: name 'importlib' is not defined"

**3. Relevant Output:**  
The AI explained that Jupyter Notebook cells share memory, and because I ran the validation cell *before* running the large "Dependency Guard" cell located above it (where the `importlib`, `pandas`, and `os` libraries were actually imported), Python didn't know what those packages were. 

**4. Validation:**  
I validated this by following the AI's two suggested solutions. First, I manually added `import importlib` to the top of my failing cell, and it ran successfully. Then, I restarted the kernel and ran the cells in sequential order from top to bottom, which also prevented the error.

**5. Adaptations:**  
I chose the second solution (running cells in order) instead of modifying the code to add redundant imports, as this aligns better with how Jupyter notebooks are designed to be explicitly executed sequentially. 

**6. Final Decision:**  
*Used*. The AI's explanation helped me understand the stateful memory behavior of Jupyter notebooks, completely solving the error without requiring permanent code changes.