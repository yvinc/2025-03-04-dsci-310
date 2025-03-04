# 2025-03-04-dsci-310-Make

- Last class we talked about pipeline. 
- Today we'll be putting everything together!

- Look at last class' class repo please because we'll be continuing on it.(02-27 https://github.com/chendaniely/2025-02-27-pipelines.git)
    - The most important part of a pipeline from last class is that:
        Every single step of a file from the file should be able to output a local file such that the next file down the pipeline would be able to use it (pass it down to the next file).

- Recall that git has difficulty tracking empty folder.
    - It is only if there is a file inside the new folder that git will be able to show it.

- Another thing we can set up in a project:
    - Consider: What are the original file that the very first script needs to take in?
        - For example: The **original** data set that the every subsequent data set will depend on.
    - In this course, we can create a subfolder `raw` within a `data` file, and it's within this `raw` folder where typically everything starts.
- Good to always first communicate with your mates in research that: Hey, this script pipeline is generally how our analysis looks like.
    -  Whatever kind of orginization of the scripts and folders works most conviniently IS the organization you should go by!
    - But note that too many deep / embedded folders would become a headache!!
- bash sees any file that starts with a dot '.' as a hidden file.
    - This can come in handy because if you're to pass down the project to other people, when we save some files that needs to be save into some specific folder.
    - This means that we can pre-create folder structure, and then we use those hidden `.__` file inside the folder so that git can track it, such as using `.gitkeep` file!
- Make sure all the scripts can be run top to bottom whenever you're updating the pipeline.

## Today: What makes `Make` special?
- As we have multiple inputs and multiple outputs, the code would be able to tell you where the code should go to clearly.
- For example, we likely don't want to risk any naming thing that will lead us to accidentally swap the training and the testing set.
- One thing to note is that:
    - Just like last week, instead of having speicific path in the script, we'll rather be passing those in the **command lines**!

- We can then start to create a `.qmd` quarto document.
- The reason we wanted to start this pipeline with Rscript by breaking down our qmd analysis is that we can now insert the resultant figure directly using markdown syntax! 
    - Which is a whole yaaay.
        - The benefit is that if we want to change other portion of the analysis, this won't have to recreate the entire analysis.
        - For example, when your model running requires 10 minutes (🥲 and we know that pain well!).
    - Allows you to run things in parallel without having to render the figure code.


- In our `.gitignore` file, we would want to ignore: data/clean folder because we no longer need to track the files that were saved into this clean folder.
- In general, when your code can re-create some saved output, the folder that saves those saved outputs can often be ignored.
    - but note that this is just the 'general' rule that allows for exceptions.
- But we can also always force add some ignored file, for example: we might want to force add a `.gitkeep` file so that git tracks that empty folder!

- Running `git status` should show you all the changes and we should expect everything in `.gitignore` to not be showing.
- `Make` is able to solve the problem where the model step within the pipeline takes, let's say 30 minutes to run.

    - see command histories for how to use `Make` and review the significance of `Make` timestamp.
    
- Dependency plot - file hierarchy—make figures out the most efficient hierarchy so that each scripts-run only runs files that have new changes. 
￼
- But if the dataset from the very beginning was changed, `Make` is also smart enough to know that it needs to go to the most root initial step and from there, run the entire analysis.

### Bash:

- When a lot of files coming from the code, make a target that delete those files.
- `rm -f` --given that the output folder exists ***even if*** it doesn't, delete it anyway.
- This helps to clean the make report!

### Github repo turned --> website!
- In Github, any repo has the ability to turn the repo into a website.
- For example, course textbooks is a repo (very similar url to the actual repo)
- The url typically has the user name and repo name assicated with it.
- Then how do we set this up?

- Go to `setting --> pages --> build` from`main` branch.
    - This leverages Github pages, turning repos into websites!
    - Our website here being specified starts from the `root` repo.

- Anytime we go to a url, it takes the human readable name and finds the IP address of the machine, then it reads the `index.html`.
- This is the default home page special file!
- We can take our quarto .qmd file and get a output file that reads `index.html`. in the **output** of the `makefile`.
    - `git add -f index.html` into the root repository.
    - We'll see a Github action thing working when we have pushed it!

- Then we can have a webview of our report!
