# GitLab CI Tutorial
## Create a new GitLab Repo
- Create an Account [GitLabCI/Register](https://gitlab.com/users/sign_up)
- Click the `+` symbol > New Project
- Give it a name
- Set the visibility (private, internal, public)

## Click Setup CI/CD or Create a new file with the name `.gitlab-ci.yml`
GitLab will automatically detect this file with the specific name.

### We will define some stages
```
stages:
    - build
    - test
```

### Define the `build` stage
```
Build Stage:
    stage: build
```

### Make this stage run an inline script
```
Build Stage:
    stage: build
    script:
        - echo "Building"
        - mkdir build
        - touch build/info.txt
    artifacts:
        paths:
            - build/
```
What this did was define a script and its an inline script, echoing to the console, creating a new directory naemd build, and adding creating a new file named info.txt.

### Define the `test` stage
```
Test Stage: 
    stage: test
    script:
        - echo "Testing"
        - test -f "build/info.txt"
```
What this did was echo to the console, and use the unix function `test` to test the file `-f <file_path>` that it exists and is a regular file. The output of this command will set the $? either `1` for failure or `0` for succeed. you can check this yourself by running echo $?

### Looking good!
Inside `.gitlab-ci.yml`
```
stages:
    - build
    - test
Build Stage:
    stage: build
    script:
        - echo "Building"
        - mkdir build
        - touch build/info.txt
    artifacts:
        paths:
            - build/
Test Stage: 
    stage: test
    script:
        - echo "Testing"
        - test -f "build/info.txt"
```
Very simple!

### Save and or Commit and Push to GitLab
Check to make sure that the syntax is valid inside GitLab. If we look at GitLab we should actually see a pipeline running just because of this file

If you dont know where to look to see the pipelines running go to [gitlab](www.gitlab.com), and go to  `CI/CD` -> `Pipelines` in the left menu.


