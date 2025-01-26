# Setting up a dev container for Go

* Primary author: [Ryan](https://github.com/rjacob6051)
* Reviewer: [Ryan Krasinski](https://github.com/RunXPS)

## Prerequisites
Before starting this tutorial, there are a couple of things you must have installed:

1. **Visual Studio Code**: [Download now](https://code.visualstudio.com/)
2. **Docker**: [Download now](https://www.docker.com/products/docker-desktop)
3. **VSCode Dev Container Extension**: [Download now](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

So why do we need these? Going from top to bottom, Visual Studio Code is a common choice for code editing, and the one we will be using to write our own Go code. Docker allows us to create *isolated development environments* through **containers**. Finally, the VSCode Dev Container extension will allow us to open out own project within a Docker container.

!!! Notice

    With docker installed, VS Code might prompt you to install the extension already. Otherwise, search for the Dev Container extension in the app or use the link above. 

## Step 1: Create a New Directory
``` bash
mkdir go-dev-container
cd go-dev-container
```
This will create a new directory, called go-dev-container, and change your current directory to the one you just created.

## Step 2: Initialize a Git Repository
``` bash
git init
```
This turns your directory into a git repository, to put it simply.

!!! Notice

    This does not sync your branch with a remote GitHub repository. Refer back to [this](https://comp423-25s.github.io/resources/git/ch4-git-remote-fetch-push-pull/) earlier lesson to set up a remote repository and save your code to GitHub.

## Step 3: Create a New Dev Container Configuration
For this step, you want to create a new folder called ".devcontainer", with a single file name "devcontainer.json". This is essentially setting up the programming environment that you will be doing your work in.
``` json
{
  "name": "Go Tutorial Dev Container",
  "image": "mcr.microsoft.com/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": [
        "golang.go"
      ]
    }
  }
}
```
While all of these commands are not too important for a beginner, some readers might want a quick explanation of what each line does:

 - name: Creates the name of the dev container
 - image: Makes the logo of the devcontainer the official Microsoft Go DevContainer image.
 - extensions: This installs the officail Go plugin for VSCode (the editor we are using)

## Step 4: Opening the Container in VSCode

1. Open the directory in VSCode using ```code .```
2. Press F1 (fn + F1 on Mac) to open a search bar, and look for **Dev Containers: Open Folder in Container...** and select your folder.
3. Wait for VSCode to set up your container (This might take a few minutes)
Once your Dev Container is up and running, your necessary Go extension will be installed automatically.

## Step 5: Verification
In a new VSCode terminal, run the following command to check the Go Version to ensure it successfully installed.
``` bash
go version
```
If you get an output like...
``` bash
go version go1.23.4 linux/arm64
```
... your Go has been installed correctly within your Dev Container! Congrats!

!!! Notice

    The version includes 'linux' instead of Windows or MacOS, which is what most likely not what you are using. This is because the version is referencing the OS of a Docker Devcontainer: Debian Linux 

## Step 6: Creating Your Program!
Create a new file called ```main.go```, and copy and paste the following contents
``` go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```

- ```package main``` tells go that this file is a part of the *main* program, which is the entry point.
- ```import "fmt"``` imports the fmt package, which is used for formatted I/O operations.
- ```func main() {}``` defines the main function. When a program is run, it will begin here.
- ```fmt.Println("Hello COMP423")``` should hopefully look similar to something you've seen before, with small differences. Specifically, this calls the ```Println``` functions from the ```fmt``` package, which allows you to print ```"Hello COMP423``` to the console.

## Step 7: Using Go Mod
Go modules are collections that are typically used for managing dependencies in numerous Go projects. To initialize one in your new directory, run the following:
``` bash
go mod init hello-comp423
```
This will create a ```go.mod``` file in your directory, which will, as stated, manage your dependencies.

## Step 8: Running the Program
To simply run the program, use
``` bash
go run main.go
```
If everything was done correctly, this should return
```
Hello COMP423
```
Essentially, the ```go run``` command compiles/executes the GO program *without* creating something called an **intermediate binary**, and is useful for quickly testing your code.

## Step 9: Building the Program
A step above run, you can use the ```build``` command as follows:
``` bash
go build main.go
```
This will create an *executable binary* call main.exe (main on mac) in your directory.

To run your binary, use the command:
``` bash
./main
```
which should also output:
```
Hello COMP423
```

### ```go run``` vs ```go build```
```go run``` compiles the program in a single step, as stated before, while ```go build``` compiles the program and then generates an intermediate binary, which can be used outside of Go. This is similar to gcc, which we used in COMP 211, where you can compile your code first into an object file, and then run that executable.

## Step 10: Congratulations!
You just made your first program using the Go language! Give yourself a pat on the back, and get ready to keep moving!