# Discord Bot using Javascript

# - - - Default Target - - - #
.DEFAULT_GOAL := run

.PHONY: run clean update

# - - - Variable pathing - - - #
NODE := node
NPM := npm

# - - - Files - - - #
MAIN_FILE := index.js
DEPLOY_COMMANDS := deploy-commands.js

# - - - Targets - - - #

# Run command
run:
	@echo "Deploying commands.."
	$(NODE) $(DEPLOY_COMMANDS)
	@echo "Running bot.."
	$(NODE) $(MAIN_FILE)

# Clean command
clean:
	@echo "Cleaning up.."
	rm -rf node_modules package-lock.json
	@echo "Cleaning up completed."

# Update command
update:
	@echo "Updating dependencies.."
	$(NPM) install
	@echo "Dependencies updated."
