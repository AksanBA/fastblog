# Using Temporary Files in Python

So in most instances when working on a project, you would have access to read and write from the folders which you are working in? But what if you don't?
That's the dilemma I faced while using a certain data platform where I didn't have direct access to the underlying folder structure. What to do in this case when you need to write a file then? In particular, I was using matplotlib/plotly to create some visualizations and I needed to put the png/html files somewhere. Temporary files to the rescue!
```python
import tempfile
import datetime
now = datetime.datetime.now()
fd, path = tempfile.mkstemp(suffix='.png')
try:
#Write the info to the temporary file
plt.savefig(path)
with open(path) as f:
#Put the temporary file into the required folder
new_folder.write("Image"+now.strftime("%Y-%m-%d")+".png", f)
finally:
#Remove the temporary file
os.remove(path)
```
You can extend this to any file type you want and may prove to be useful whenever you're dealing with systems where you don't have direct access to folders but you can read/write to them via an API call. Just replace the pseudocode of new_folder.write() with whatever you need!
