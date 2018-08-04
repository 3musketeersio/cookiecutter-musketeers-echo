# DOCKER_RUN_ALPINE has been added for creating .env file because
#		- trying to run a docker-compose command will fail if .env is not there
#				as service musketeers requires it
#		- when TravisCI generates this example with cookiecutter, the file owner stays root
#				and running `cp -f $(ENVFILE) .env` will result a permission denied error
DOCKER_RUN_ALPINE = docker run -v $(PWD):/opt/app -w /opt/app alpine
COMPOSE_RUN_MUSKETEERS = docker-compose run --rm musketeers
# ENVFILE is .env.template by default but can be overwritten
ENVFILE ?= .env.template

all:
	ENVFILE=.env.example $(MAKE) envfile echo clean
.PHONY: all

# envfile creates or overwrites .env with $(ENVFILE)
envfile:
	$(DOCKER_RUN_ALPINE) sh -c 'cp -f $(ENVFILE) .env'
.PHONY: envfile

removeEnvfile:
	$(DOCKER_RUN_ALPINE) sh -c 'rm -f .env'
.PHONY: removeEnvfile

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
	$(MAKE) removeEnvfile
.PHONY: clean

# _echo prints out ECHO_MESSAGE
_echo:
	echo $(ECHO_MESSAGE)
.PHONY: _echo