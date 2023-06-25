
---
title: "🔨 Makefiles: The Secret Sauce Every Developer Should Leverage"
date: 2023-07-07
showToc: true
tags: ["Makefile", "development", "coding best practices", "automation"]
---

## 🎯 Efficiency Is Key
As developers, we always strive to make our workflow more efficient. The less time spent on repetitive tasks, the more time we can dedicate to solving complex problems. This is where Makefiles become a game-changer. Makefiles provide a straightforward way to automate our software's building process, making life easier for every developer on the team.

## 🔗 Makefiles and their Targets
In essence, a Makefile is a script containing a series of rules or 'targets' which dictate how to derive the file or class from other files. When a make command is invoked, it reads the Makefile in the current directory and follows the instructions to build your application.

Consider the simple Makefile example below:

```
.PHONY: build
build:
	gcc -o app main.c
```
In this example, build is the target, and `gcc -o app main.c` is the command the make tool will execute when we run make build.

## 🎩 The Power of Phony
You might be wondering about the `.PHONY` line in our previous example. This is a special target used to avoid a problem with file names that match the target. If there's a file named `build` in the directory, `make build` won't work as expected. By declaring build as a `phony` target, we ensure the command will run, regardless of any conflicting files.

Now that you know about targets and the `phony` directive, let's delve into a more complex Makefile example:

```
default: help
export env?=dev
export region?=ap-southeast-2
export acc?=cdh

# Set the bash script to use and the account ID based on the account and environment variables
ifeq ($(acc),cdh)
  	infra_bash_script=infra.sh
  	ifeq ($(env),prod)
    	aws_account_id=123456789
  	else ifeq ($(env),dev)
    	aws_account_id=123456788
  	endif
else ifeq ($(acc),hr)
  	infra_bash_script=infra-hr.sh
  	ifeq ($(env),prod)
    	aws_account_id=987654321
  	else ifeq ($(env),dev)
    	aws_account_id=987654322
  	endif
endif
```

This Makefile declares variables at the top and sets environment-specific values. Notice the `ifeq` directives used to conditionally define variables based on the environment and account.

## 🆘 The Default Help Makefile Action
Having a Makefile in your project is great, but ensuring it's user-friendly is even better. A common practice is to include a help target that displays a description of the other targets. It often serves as the default target, which is invoked when make is run without specifying a target.

Consider the example:
```
.PHONY: help
help: # Show help for each of the Makefile recipes.
	@grep -E '^[a-zA-Z0-9 -]+:.*#'  Makefile | sort | while read -r l; do printf "\033[1;32m$$(echo $$l | cut -f 1 -d':')\033[00m:$$(echo $$l | cut -f 2- -d'#')\n"; done
```

In this instance, `help` is a `phony` target, and it lists the descriptions of all the targets in the Makefile. These descriptions are extracted from comments starting with # right after each target. This way, new developers can quickly learn how to use the Makefile in their local development environment.

## 💡 Closing Thoughts
Makefiles bring a lot to the table when it comes to improving developer efficiency and enforcing consistent workflows. They provide a powerful way to automate common tasks, ensure everyone is using the same commands, and offer a self-documenting system that helps onboard new team members.
