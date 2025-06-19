# Java compiler and flags
JC = javac
JFLAGS = -g -d bin

# Dir Setup
BIN_DIR = bin
SRC_DIR = src

# --- Auto-discovery of Main Class ---
MAIN_FILE = $(shell grep -l "public static void main" $(SRC_DIR)/*.java | head -n 1)
MAIN_CLASS = $(notdir $(patsubst %.java,%,$(MAIN_FILE)))

# - - - Source and Class - - - #
SOURCES = $(wildcard $(SRC_DIR)/*.java)
CLASSES = $(SOURCES:$(SRC_DIR)/%.java=$(BIN_DIR)/%.class)

all: $(CLASSES)

$(BIN_DIR)/%.class: $(SRC_DIR)/%.java
	@echo "Compiling $<..."
	@mkdir -p $(BIN_DIR)
	$(JC) $(JFLAGS) $<

# - - - Code Run - - - #
run: all
	@if [ -z "$(MAIN_CLASS)" ]; then \
		echo "Error: No main class with 'public static void main' found."; \
		exit 1; \
	fi
	@echo "Running the application (Main Class: $(MAIN_CLASS))..."
	java -cp $(BIN_DIR) $(MAIN_CLASS)

# - - - Clean Target Proj Dir - - - #
clean:
	@echo "Cleaning up the project..."
	rm -rf $(BIN_DIR)

# Phony targets are not actual files, but commands
.PHONY: all run clean
