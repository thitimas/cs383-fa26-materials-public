# Using JupyterHub for CS383

CS383 runs on a JupyterHub hosted through **NAIRR Pilot / CloudBank**, built and operated by 2i2c. You don't need to install Python, Jupyter, or any packages on your own computer — everything runs in your browser, on a server assigned to you.

**Our hub:** [york.cloudbank.2i2c.cloud](https://york.cloudbank.2i2c.cloud)

---

## Access the Hub

1. Go to **[york.cloudbank.2i2c.cloud](https://york.cloudbank.2i2c.cloud)**.
2. Click **Log in to continue**, and sign in with the credentials your instructor gave you access with.
3. The first time you log in, your personal server needs to start up — this can take a minute or two. You'll land in the **JupyterLab** interface once it's ready: a file browser on the left, and a Launcher tab in the middle.

You only need to do this once per session. Your files persist between logins — you don't need to re-upload anything you've already saved.

---

## Create a Blank Notebook

From the Launcher tab, under **Notebook**, click the **Python 3** tile.

(If the Launcher isn't open, click the **File** menu → **New** → **Notebook**, then choose the Python 3 kernel when prompted.)

You'll get a blank notebook with one empty cell. A notebook is made of **cells** — a cell is either:

- a **code** cell, which runs Python, or
- a **markdown** cell, which holds formatted text (headers, bullet points, bold/italic, links, etc.)

Rename your notebook by clicking its title at the top of the tab (it starts as "Untitled").

---

## Add a New Cell

Click the **+** button in the notebook's toolbar to insert a new cell below the one you have selected.

To change a cell's type, use the dropdown in the notebook toolbar — it shows **Code** by default. Click it and choose **Markdown** instead if you want to write formatted text rather than run Python.

Code is typed in directly. Markdown cells need to be run (like code cells) before the formatting actually renders — until then, you'll just see the raw text with `#` symbols and asterisks.

---

## Run Code

- **Shift + Enter** runs the selected cell and moves to the next one — this is the fastest way to work.
- The **▶ Run** button in the toolbar runs just the current cell.
- To run every cell in the notebook from top to bottom, use the **Run** menu → **Run All Cells**, or the **Kernel** menu → **Restart Kernel and Run All Cells** (this also clears out any old variables first — good habit before you submit anything).

A few things that catch people off guard:

- Code you run in one cell stays available to every other cell in the notebook — variables don't reset between cells.
- If you go back and change an earlier cell, cells below it don't automatically re-run. You need to re-run them yourself, in order, or your notebook can end up in a state that only works because of the order you happened to click things in.
- Before you submit any assignment, always do a **Restart Kernel and Run All Cells** and confirm it runs top to bottom with no errors — a notebook that only works out of order will not be graded as passing.

---

## Download Notebooks

To save a copy of your notebook to your own computer:

**File** menu → **Save and Export Notebook As...** → **Notebook (.ipynb)**

This downloads the standard `.ipynb` file — the same format you'll submit for assignments. The same menu lets you export to other formats (HTML, PDF, Markdown, etc.) if you ever need a shareable, non-interactive version.

---

## Getting Course Notebooks

For most lectures and assignments, your instructor will share a **link** that automatically pulls the notebook from our course GitHub repository straight into your JupyterHub workspace — you won't need to download anything manually or find files yourself. Just click the link, log in if prompted, and the notebook will open ready to go.

If you ever need to grab a notebook manually instead, our course materials live at:
**[github.com/thitimas/cs383-fa26-materials-public](https://github.com/thitimas/cs383-fa26-materials-public)**

---

## Additional Resources

- [2i2c Pilot Hubs Documentation](https://2i2c.org/pilot) — background on the infrastructure our hub runs on.
- [Jupyter Notebook basics (official docs)](https://docs.jupyter.org/en/latest/) — a deeper reference if you want more than this quick-start guide covers.

*Questions or something not working? Email Dr. Thitima Srivatanakul at tsrivatanakul@york.cuny.edu.*
