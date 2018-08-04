COMPOSE_RUN_MUSKETEERS = docker-compose run --rm musketeers
# ENVFILE is .env.template by default but can be overwritten
ENVFILE ?= .env.template

all:
	ENVFILE=.env.example $(MAKE) envfile echo clean
.PHONY: all

# envfile creates or overwrites .env with $(ENVFILE)
envfile:
	touch .env
	cp -f $(ENVFILE) .env
.PHONY: envfile

# echo calls the target _echo with the musketeers image
echo:
	$(COMPOSE_RUN_MUSKETEERS) make _echo
.PHONY: echo

# shell allows you to enter a musketeers container
shell:
	$(COMPOSE_RUN_MUSKETEERS) sh -l
.PHONY: shell

# clean the repository and docker environment
clean:
	docker-compose down --remove-orphans
.PHONY: clean

# _echo prints out ECHO_MESSAGE
_echo:
	echo $(ECHO_MESSAGE)
.PHONY: _echo