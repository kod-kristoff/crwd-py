
PLATFORM := ${shell uname -o}



ifeq (${VIRTUAL_ENV},)
  VENV_NAME = .venv
  ifeq (${POETRY_VIRTUALVENVS_CREATE},0)
    ${info don't use venv}
    INVENV =
  else
    ${info use venv}
    INVENV = . ${VENV_NAME}/bin/activate;
  endif
else
  VENV_NAME = ${VIRTUAL_ENV}
  INVENV =
endif

${info Platform: ${PLATFORM}}
${info POETRY_VIRTUALVENVS_CREATE: ${POETRY_VIRTUALVENVS_CREATE}}
${info Using virtual environment: ${VENV_NAME}}

VENV_BIN = ${VENV_NAME}/bin



help:
	@echo "Available commands:"

venv: ${VENV_NAME}

install: venv ${VENV_NAME}/req.installed
install-dev: venv ${VENV_NAME}/req-dev.installed

${VENV_NAME}:
  #ifeq (${POETRY_VIRTUALVENVS_CREATE},0)
	test -d ${VENV_NAME} || python3 -m venv ${VENV_NAME}

# order of libs is meaningful. First, we install libs without internal dependencies that other libs depend on.

libs := crwd webapp
#libs := foundation auctions shipping db_infrastructure web_app_models auctions_infrastructure shipping_infrastructure customer_relationship payments processes main web_app

define install_dev
	${INVENV} cd $(1); poetry install

endef

.PHONY: dev
dev: venv
	# pip install --use-feature=2020-resolver -r requirements.txt -r requirements-dev.txt
	$(foreach lib,$(libs),$(call install_dev,$(lib)))

