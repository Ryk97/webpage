.DEFAULT_GOAL := help

VENV_NAME?=venv

.PHONY: help
help: ## Outputs the help
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

.PHONY: init
init: ## Creates a virtualenv and installs python requirements
	test -d $(VENV_NAME) || virtualenv -p python3 $(VENV_NAME)
	. $(VENV_NAME)/bin/activate; pip install -Ur requirements.txt
	touch $(VENV_NAME)/touchfile

.PHONY: episode-check
episode-check: ## Checks all Podcast Episodes if all player links (Spotify, etc.) are set
	venv/bin/python empty-player-urls.py

.PHONY: find-tags-that-need-descriptions
find-tags-that-need-descriptions: ## Checks all used tags that need SEO descriptions
	venv/bin/python find-tags-that-need-descriptions.py