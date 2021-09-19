
PLATFORM := ${shell uname -o}
INVENV_PATH = ${shell which invenv}



ifeq (${VIRTUAL_ENV},)
  VENV_NAME = .venv
  ${info invenv: ${INVENV_PATH}}
  ifeq (${INVENV_PATH},)
    INVENV = export VIRTUAL_ENV="${VENV_NAME}"; export PATH="${VENV_BIN}:${PATH}"; unset PYTHON_HOME;
  else
    INVENV = invenv -C ${VENV_NAME}
  endif
else
  VENV_NAME = ${VIRTUAL_ENV}
  INVENV =
endif

${info Platform: ${PLATFORM}}
${info Using virtual environment: ${VENV_NAME}}

VENV_BIN = ${VENV_NAME}/bin



help:
	@echo "Available commands:"

venv: ${VENV_NAME}

install: venv ${VENV_NAME}/req.installed
install-dev: venv ${VENV_NAME}/req-dev.installed

${VENV_NAME}:
	test -d ${VENV_NAME} || python3 -m venv ${VENV_NAME}

# order of libs is meaningful. First, we install libs without internal dependencies that other libs depend on.

libs := crwd webapp
#libs := foundation auctions shipping db_infrastructure web_app_models auctions_infrastructure shipping_infrastructure customer_relationship payments processes main web_app

define install_dev
	. ${VENV_NAME}/bin/activate; cd $(1); poetry install

endef

.PHONY: dev
dev: venv
	# pip install --use-feature=2020-resolver -r requirements.txt -r requirements-dev.txt
	$(foreach lib,$(libs),$(call install_dev,$(lib)))

