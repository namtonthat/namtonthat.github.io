---
title: "🤖 Automating Your Repositories with Makefiles"
date: 2023-07-01
showToc: true
tags: ["Makefile", "automation", "coding best practices", "repositories"]
---

## 🤖 The Power of Automation

Automation is one of the key factors that drive efficiency in the software development process. From continuous integration and deployment to script-based task execution, automation not only saves time but also reduces the chances of human errors and maintains consistency in your workflows.

One tool that shines in automating tasks is the Makefile. Primarily used for automating the build process of a software application, Makefiles can be repurposed to automate a variety of tasks in your repositories.

## 🎯 Makefiles for Repository Automation

By using Makefiles, you can automate tasks such as testing, deploying, and even verifying environments. Let's take a look at the following Makefile example, which gives a glimpse of how to automate your repositories:

```Makefile
default: help
export env?=dev
export region?=ap-southeast-2
export acc?=cdh

# Set the bash script to use and the account ID based on the account and environment variables
ifeq ($(acc),cdh)
  	infra_bash_script=infrastructure.sh
  	ifeq ($(env),prod)
    	aws_account_id=XXXXXXXXXXXX
  	else ifeq ($(env),dev)
    	aws_account_id=XXXXXXXXXXXX
  	endif
else ifeq ($(acc),hr)
  	infra_bash_script=infrastructure-hr-metrics.sh
  	ifeq ($(env),prod)
    	aws_account_id=XXXXXXXXXXXX
  	else ifeq ($(env),dev)
    	aws_account_id=XXXXXXXXXXXX
  	endif
endif

.PHONY: help
help: # Show help for each of the Makefile recipes.
	@grep -E '^[a-zA-Z0-9 -]+:.*#'  Makefile | sort | while read -r l; do printf "\033[1;32m$$(echo $$l | cut -f 1 -d':')\033[00m:$$(echo $$l | cut -f 2- -d'#')\n"; done

.PHONY: apply
apply: verify # Apply Gantry changes (uses verify to ensure correct account is being used).
	@./$(infra_bash_script) apply $(job) $(region) $(env)

verify: # Verify AWS account
	@echo "Verifying AWS account..."
	@account_id=`aws sts get-caller-identity --query Account --output text`;\
	if [ -z "$$account_id" ]; then \
		echo "Could not get AWS account ID. Please make sure you're authenticated with AWS."; \
		exit 1; \
	elif [ "$$account_id" != "$(aws_account_id)" ]; then \
		echo "AWS account mismatch. You are currently in $$account_id but expected to be in $(aws_account_id). Exiting."; \
		exit 1; \
	else \
		echo "Current AWS account ID matches expected account ID."; \
	fi


```

In this Makefile, the `apply` target is dependent on the `verify` target:
-  This means that before executing the command specified in the `apply` target, the `make` tool will first execute the `verify` target. 
- The `verify` target checks if the user is authenticated with the correct AWS account before proceeding with applying changes.
- The `help` target, as explained in previous posts, provides a user-friendly way to display all the Makefile's targets and their descriptions.

## 💡 Closing Thoughts
Makefiles are versatile and powerful tools that allow you to automate mundane tasks, enforce consistency, and speed up your workflow in your repositories. They provide a powerful way to automate common tasks, ensure everyone is using the same commands, and offer a self-documenting system that helps onboard new team members. The example given here is just the tip of the iceberg when it comes to what you can achieve with Makefiles. So don't hesitate to leverage them in your projects. Happy coding!


