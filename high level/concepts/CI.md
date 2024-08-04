# Theory

## What is it

**Continuous Integration** (CI) is A DevOps practice that automate parts of the software release process, where developers regularly integrate their code changes into a shared repository, preferably several times a day. Each integration is automatically verified by running tests and other verifications to detect integration errors as quickly as possible.

Even though this is an incredibly powerful practice, is best paired with [[CD]] 
## Why

- **Automated testing** and static analysis help maintain high code quality.
- By integrating regularly, **errors can be detected early**, making them easier and less costly to fix.
- Smaller, more **frequent integrations** reduce the risk of large-scale integration issues.
- CI supports **faster development cycles** by automating the build and test processes.
- CI encourages collaborative development and ensures that all team members are working with the latest codebase.

## Common Use Cases

- **Automated Testing**, Running unit tests, integration tests, and end-to-end tests.
- **Static Code Analysis**, Checking code for stylistic errors, potential bugs, and security vulnerabilities.
- Providing **immediate feedback** to developers on the status of the codebase.
- [[CD]]. Compiling code, creating binaries, packaging software.  Automatically deploying code to staging or production environments.

## parts
### Workflows
Workflows define the automated processes that are **triggered** by specific **events** in the **repository**, such as code pushes, pull requests, or scheduled times. They consist of one or more jobs that run in a specified order. These are normally written on a `.yaml` file 
### Runner
A runner is a server that runs the CI jobs. It can be self-hosted or provided by a CI service. Runners execute the steps defined in the workflow.
### Jobs
Jobs are units of work defined in the workflow. They run in parallel except they depends on each other, in that case they will run sequentially. Each job is executed in its own virtual environment.
### Steps
Steps are individual tasks performed within a job. These can include actions like checking out code, setting up dependencies, running tests, and deploying applications. Steps are executed in the order they are defined.
### Actions
Actions are reusable, standalone commands used in workflows. They can be written by the community or custom-made. Actions encapsulate specific tasks and can be shared across projects.

## common errors
### saving into file
```sh
run: echo ${{ secrets.APP_ENV }} > .env
```
this will **NOT** write the secret into the file.
```sh
run: echo "${{ secrets.APP_ENV }}" > .env
```
this **will**. notice the `""`
# Practice

## Github Actions
### when
```yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```

### where
```yaml
jobs:
  test:
    name: Test
    runs-on: ubuntu-latest
```
### what is needed
this one is Optional, you can set your dependencies using [[docker]]
```yaml
services:
      postgres:
        image: postgres:16
        ports:
          - 5432:5432
	  rabbit:
		image: rabbitmq
        
```
### steps
```yaml
    steps:
    - name: Set up Go 1.22
      uses: actions/setup-go@v2
      with:
        go-version: ^1.22
      id: go
    - name: Tidy go mod
      run: go mod tidy
	- name: Test
      run: make test
```
