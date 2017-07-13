# Jupyter Notebook Conventions

## Manifesto
Notebooks are designed for easy reproducibility and code-sharing. Babysitting and debugging someone else's notebook sucks. Don't curse your friends with this burden!

When a user opens your notebook, they should be able to **run all cells _in order_** without any additional intervention.

Inputs that must be made to enable the code to run (e.g. password prompts, API tokens, etc) should be requested as soon as the notebook starts running.

Here's the TLDR:
> Check the top few cells and edit the file paths or API keys that need to be edited, if any. Press "Run All Cells." If ANY other input is needed, you have failed and need to read [Tips](#tips) again.

## Tips


### All imports at the top. 
I'll sometimes add a markdown note like "If you need to run X function, you'll also need to import blah" to handle the optional imports so that users don't need to import unnecessary libraries.

```python
import json
import requests
```
```markdown
> If you want to run the clustering, you'll need sklearn:
```
```python
# Optional:
from sklearn.cluster import DBSCAN
```

### All global variables at the top, together in one cell*
\* Unless they take a long time to instantiate (e.g. things with server round-trips, things that read large files off disk, etc.) These sorts of assignments should ALSO be at the top, but each in their own cell. 

For cells that take longer than a few seconds to execute, I'll typically add a printout of the elapsed time taken to run these cells:


```python
tic = time.now()
data = json.loads(open('raw.json', 'r').read())
print("Took {}s to execute.".format(time.now() - tic))
```
This lets users run that cell once and then benefit from those global variables without needing to rerun anything.


### All paths on disk are defined in one cell at the top.
```python
JSON_FILE = "~/data/raw.json"
PARAMS_FILE = "~/data/params.cfg"
```

### Long-running lines live in their own cell.
Often with a markdown cell above that says something like "This cell takes 10 minutes to run", or with a `tic` printout as per above.

### Utility functions live in one giant cell.
This should take zero seconds to run, since it's just defining functions.

### Demonstrate structure
Between the above and your analysis, add a markdown cell with a header that explains that you're now switching to analysis and the subsequent cells can run.

From then on, each cell should have a markdown cell above it to explain what's going on. If the cell cannot be easily explained in a few lines of text, break it apart. If it is too simple to be explained in a whole cell, use inline `#` comments instead and combine with neighboring cells that perform the same function.

### Outputs should go at the end
If useful, the last cell should allow the user to save off relevant data or byproducts to disk. Don't save to disk elsewhere in the notebook unless absolutely necessary; that way, users know when to expect new files on their hard-drive, and can opt out.

## Rules of Thumb
- Cells should never be longer than the height of the browser window
- The whole notebook should serve one purpose, and only do _one thing_.
- If you need to copy and paste cells from another notebook, you're using notebooks wrong; convert the common code into a standalone .py file and import it in both notebooks.
