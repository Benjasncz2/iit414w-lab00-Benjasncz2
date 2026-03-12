# Reproducibility Runbook - Lab 0

**(a) Header**
- **Full Name:** Benjamín Fernando Sánchez Torres
- **GitHub Username:** Benjasncz2
- **Course Code:** IIT414W
- **Date:** 11 March 2026

---

**(b) System Info**
- **Operating System:** Windows 10
- **Python Version:** 3.11.9
- **Conda/Pip Version:** Pip 24.0

---

**(c) Setup Instructions**

To recreate the exact environment used to run these notebooks, please follow these steps using your terminal (Command Prompt or PowerShell):

1. **Clone the repository and navigate to the project directory:**
   ```bash
   git clone [(https://github.com/Benjasncz2/iit414w-lab00-Benjasncz2.git)]
   cd iit414w-lab00-Benjasncz2
   ```

2. **If using Conda (Recommended):**
   Run the following command to create the environment using the provided `environment.yml` file:
   ```bash
   conda env create -f environment.yml
   ```
   *Note: This will download and install all the pinned dependencies (like Pandas, Scikit-learn, and FastF1).*

3. **Activate the environment:**
   ```bash
   conda activate iit414w
   ```

4. **Launch Jupyter Lab:**
   ```bash
   jupyter lab
   ```

*(Alternative using purely standard python venv)*
1. `python -m venv iit414ww_env`
2. `iit414ww_env\Scripts\activate`
3. `pip install -r requirements.txt` (If a requirements.txt was translated from the provided environment.yml)
4. `jupyter lab`

---

**(d) How to run**
The notebooks should be executed in a Jupyter Lab or VSCode interface using the activated `iit414w` kernel.

There is no strict sequential requirement between the original files, but it is highly recommended to run **`setup_check.ipynb`** first to validate the cache permissions and test the connection to the APIs.

Execute every cell in order from top to bottom (Kernel -> Restart & Run All). Do not skip the "Dependency Guard" cells.

---

**(e) Problems encountered**

Here are two real problems I encountered during the setup and execution, and how I fixed them:

1. **PermissionError [WinError 5] when enabling FastF1 Cache:**
   - **Problem:** When running `fastf1.Cache.enable_cache(cache_path)`, Windows threw an "Access Denied" error because the script was trying to navigate `..` (up one level) and create a folder in a protected `C:\Users\` root directory.
   - **Solution:** I updated the `os.path.join` logic to create the cache folder directly in the current working directory (`os.getcwd()`) instead of navigating up the directory tree.

2. **NameError: name 'importlib' is not defined:**
   - **Problem:** When running the Python version validation cell, it failed because `importlib` and `pandas` were missing.
   - **Solution:** I realized Jupyter cells share state and I had skipped executing the large "Dependency Guard" block above it. I restarted the kernel and ran all cells sequentially to ensure all libraries were properly loaded into memory before use.

---

**(f) Expected outputs**
When a successful run is achieved, you should see:
- The Environment Verification section printing a neatly formatted 6-row package table displaying the exact pinned versions for `numpy (2.4)`, `pandas (2.3)`, etc.
- No `ModuleNotFoundError` during the dependency check sequence.
- A FastF1 summary successfully displaying the DataFrame shapes (20 rows in `session.results`) for the loaded 2024 Bahrain session.
- A Jolpica API successfully connecting (returning HTTP Status 200) and listing the correct JSON data points for the top 3 drivers.

