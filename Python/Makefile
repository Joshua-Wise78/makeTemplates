# Python Interp
PYTHON ?= python3

# Default file and virtual env
MAIN_FILE ?= main.py
VENV_DIR ?= venv

# - - - Linter Specs for reqs.txt - - - #
# flake8, pylint, etc...
LINTER ?= flake8

# - - - Find All Python Files - - - #
SRC_FILES = $(shell find . -name "*.py" -not -path "./$(VENV_DIR)/*")

# - - - Force make to have args - - - #
.DEFAULT_GOAL := help

.PHONY: all run install lint test clean help

# - - - Command Targs - - - #
all: install lint test

# - - - Run the Main File - - - #
run:
	@echo "Running the main file.."
	@. $(VENV_DIR)/bin/activate; $(PYTHON) $(MAIN_FILE)

install: $(VENV_DIR)/bin/activate
$(VENV_DIR)/bin/activate: requirements.txt
	@echo "Creating virtual environment in $(VENV_DIR)..."
	$(PYTHON) -m venv $(VENV_DIR)
	@echo "Upgrading pip and installing dependencies from requirements.txt..."
	@. $(VENV_DIR)/bin/activate; pip install --upgrade pip; pip install -r requirements.txt
	@touch $(VENV_DIR)/bin/activate

# - - - Lint Python Files - - - #
lint:
	@echo "Lint source files w/ $(LINTER)..."
	@. $(VENV_DIR)/bin/activate; $(LINTER) $(SRC_FILES)

# - - - Python testing - - - #
test:
	@echo "Python tests running..."
	@. $(VENV_DIR)/bin/activate; pytest

# - - - Clean Project Dir - - - #
clean:
	@echo "Cleaning up files..."
	@rm -rf $(VENV_DIR)
	@find . -type d -name "__pycache__" -exec rm -rf {} +
	@find . -type f -name "*.pyc" -delete
	@rm -rf .pytest_cache .coverage

# - - - Help command - - - #
help:
	@echo "Makefile for Python Projects"
	@echo ""
	@echo "Usage: make [target]"
	@echo ""
	@echo "Available targets:"
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "  \033[36m%-15s\033[0m %s\n", $$1, $$2}'
