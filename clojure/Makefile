# REQUIRED SECTION
ROOT_DIR:=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
include $(ROOT_DIR)/.mk-lib/common.mk
include dev.env
export $(shell sed 's/=.*//' dev.env) # reads the env file for user and service
# END OF REQUIRED SECTION

.PHONY: help dependencies up start stop restart status ps clean bounce shell recreate

dependencies: check-dependencies ## Check dependencies

up: ## Start all or c=<name> containers in foreground
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) up $(c)

start: ## Start all or c=<name> containers in background
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) up -d $(c)

stop: ## Stop all or c=<name> containers
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) stop $(c)

restart: ## Restart all or c=<name> containers
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) stop $(c)
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) up $(c) -d

status: ## Show status of containers
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) ps

ps: status ## Alias of status

clean:
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) down

recreate:
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) up -d --force-recreate

build:
	@$(DOCKER_COMPOSE) -f $(DOCKER_COMPOSE_FILE) build

bounce: clean build recreate shell

shell: ## Get a zsh shell
	@$(DOCKER_COMPOSE) exec $(SERVICE_NAME) zsh
