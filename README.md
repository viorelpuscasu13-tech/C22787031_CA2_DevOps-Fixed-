# Python Calculator ( Simple Code ) for CI/CD Project

## Overview

This project contains a simple Python calculator application designed to demonstrate Continuos Integration (CI) best practices using :

* GitHub - Source control, branching, pull requests, branch protection
* Python - The programming language used for the code, simple application logic with error handling
* Azure Pipelines - Automated builds, testing, linting, coverage enforcement
* Pytest + Coverage - Unit testing with ≥80% code coverage
* Pylint - Static code analysis

The focus of the project is to show the CI/CD implementation as part of the DevOps module. It was used a simple python code for the project.

## Technologies Used

| Technology      | Purpose                          |
| --------------- | -------------------------------- |
| Python 3.13     | Application logic and testing    |
| Pytest          | Unit testing                     |
| pytest-cov      | Coverage reporting + enforcement |
| Pylint          | Static code analysis             |
| GitHub          | Version control and PR workflow  |
| Azure Pipelines | CI automation                    |
| YAML            | Pipeline configuration           |

## Local Development Setup

To work on this project locally some steps needs to be followed:

1. Clone the repository
  - ```git clone https://github.com/viorelpuscasu13-tech/C22787031_CA2.git```
2. Go into the project directory
  - ```cd C22787031_CA2```
3. Set up Python environment

This project requires Python 3.13. To ensure that everything works coorectly:
  - Check if Python is installed:
```C:/Users/viore/AppData/Local/Programs/Python/Python313/python.exe --version```
- Set PATH environment variable

   Search bar - View Advanced system settings - Environment Variables - Path -Edit - New - ( Select the path of your Python file )
<img width="1566" height="513" alt="image" src="https://github.com/user-attachments/assets/e7584861-0114-4ec1-ae20-982159264df6" />

4. Install project dependencies
  - Install pytest and pytest-cov for running tests and measuring coverage:
  ```bash
      python -m pip install --upgrade pip
      python -m pip install pytest pytest-cov pylint
  ```
5. Verify installation
  - Run the foolowing command to check if everything works acordently: 
  ```bash
      python -m pytest --version
      python -m pylint calculator/
  ```
  - pytest: will confirm that tests can be exceuted.
  - pylint: runs static code analysis on the calculator folder.

6. Running application
  - The following python file was created to test the calculator interactively:
  ```bash
      python run_calculator.py
  ```
  - And the result is:
<img width="279" height="90" alt="image" src="https://github.com/user-attachments/assets/2e186e0b-b0cf-400f-8850-8b36b2cb3d5d" />

## Application Features

The calculator project includes four core mathematical operations:

  - Add function:
```bash
def add(a: float, b: float) -> float:
    """Return the sum of a and b."""
    return a + b
```
  - Divide function:
```bash
def divide(a: float, b: float) -> float:
    """Return the division of a by b. Raises ValueError if b is 0."""
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b
```
  - Multiply function:
```bash
def multiply(a: float, b: float) -> float:
    """Return the product of a and b."""
    return a * b
```
  - Deviation function ( With error handling ):
```bash
def deviation(numbers: list[float]) -> float:
    """Return the standard deviation of a list of numbers."""
    if not numbers:
        raise ValueError("List of numbers is empty")
    mean = sum(numbers) / len(numbers)
    variance = sum((x - mean) ** 2 for x in numbers) / len(numbers)
    return sqrt(variance)
 ```

### The code in Visual Studio
<img width="617" height="507" alt="image" src="https://github.com/user-attachments/assets/5c478c21-f8c3-4588-85a0-c43aae6f5f39" />

### Project Structure

<img width="183" height="271" alt="image" src="https://github.com/user-attachments/assets/f4dfdd05-2284-4f3a-ab85-95aaa61bcae7" />



## CI Pipeline Implementation

The CI pipeline is implemented using the Azure Pipelines with an YAML configuration file.

### The pipeline performs:

  - Install dependencies
  - Run pylint static analysis
  - Run pytest static analysis
  - Enforce 80% minimum coverage
  - Triger on main and development branches

azure-pipelines.yml File:
```bash
trigger:
  branches:
    include:
      - main
      - development

pool:
  vmImage: 'ubuntu-latest'

steps:
# -------------------------
# 1. Use Python and set it up
# -------------------------
- task: UsePythonVersion@0
  inputs:
    versionSpec: '3.x'
  displayName: 'Set up Python'

# -------------------------
# 2. Install dependencies like pip
# -------------------------
- script: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    pip install pytest pytest-cov pylint
  displayName: 'Install dependencies'

# -------------------------
# 3. Run Pylint 
# -------------------------
- script: |
    pylint calculator/
  displayName: 'Run Pylint static analysis'

# -------------------------
# 4. Run Unit Tests with Coverage
# -------------------------
- script: |
    pytest tests --cov=calculator --cov-fail-under=80
  displayName: 'Run unit tests with coverage (80% min)'
```

<img width="1335" height="926" alt="image" src="https://github.com/user-attachments/assets/7df569b8-dc51-484c-9d81-a74669bc6799" />




## Branch Policies and Protection

Branch protection rules are configured on GitHub to enforce good CI/CD practices. Branch protection ensures that nobody can accidentally break the main branch. It forces developers to follow a good CI practices.

  - main branch (protected)

### The following steps needs to be followed to create the new rule:

![rep1](https://github.com/user-attachments/assets/006b033f-7bed-4ea3-9ae4-26fab3adc440)
![Screenshot 2025-11-16 095439](https://github.com/user-attachments/assets/cb0a4c94-bc88-4963-b6d1-d1798c1dee35)

Direct push not allowed

PR required

Azure Pipeline must pass

Coverage ≥ 80% required

  - development branch

Active development branch

PR merge into main only after CI is successful

## Testing Strategy

Testing is done using:
  - pytest

For this the entire path was used in order for the pytest to work properly:
```bash
C:/Users/viore/AppData/Local/Programs/Python/Python313/python.exe -m pytest tests --cov=calculator --cov-fail-under=80
```
  <img width="940" height="662" alt="image" src="https://github.com/user-attachments/assets/e8f77a30-3530-40eb-a1da-3173e3119e91" />
  
  - pytest for functional unit tests
  - pytest-cov for coverage reporting
  - CI-enforced coverage threshold: 80% minimum

  - pylint

For this the entire path was used in order for the pytest to work properly:
```bash
C:/Users/viore/AppData/Local/Programs/Python/Python313/python.exe -m pylint calculator/
```
<img width="719" height="206" alt="image" src="https://github.com/user-attachments/assets/90fbf3ab-b7d6-47f5-a372-f54303695a65" />


Test cases include:

  - Valid calculations
  - Edge cases
  - Error conditions
  - Division by zero

Tests are located in the test/ folder.


## Troubleshooting Guide

  - python: command not fount

Solution: Add Python 3.13 installation directory to PATH ( Follow the steps provided earlier ).

  - pip: command not found
```bash
python -m pip install <package>
```

  -"ModuleNotFoundError"

Ocuurs when running test files directly:
```bash
python tests/test_operations.py
```

Fix: Run using pytest from project root:
```bash
pytest tests
```

  - Pylint low score

Sollution:
1. Adding docstrings
2. Improving function naming
3. Organizing imports

