ENV USER developer
# ^ TODO Implement this

ARG VARIANT=3.9
FROM python:${VARIANT}

# For installs without user interaction
ENV DEBIAN_FRONTEND noninteractive
# Prevents Python from writing pyc files to disc (equivalent to python -B)
# ENV PYTHONDONTWRITEBYTECODE 1
# # Prevents Python from buffering stdout and stderr (equivalent to python -u)
# ENV PYTHONUNBUFFERED 1

# Configure the timezone
ENV TZ=Australia/Sydney

# Install core system utilities
RUN apt-get update \
    && apt-get install -y \
    curl apt-utils apt-transport-https debconf-utils gcc build-essential

# Install necessary locales
RUN apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen

# Install other useful tools
RUN apt-get install -y vim htop less sudo net-tools telnet

# Create user account with sudo rights
RUN useradd -u 1001 -m -d /home/developer -s /bin/bash developer \
    && echo "developer ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Create the docker group
# RUN groupadd docker

# # Add your user to the docker group.
# RUN usermod -aG docker ${USER}

# # Refresh group membership
# RUN su -s ${USER}

# Switch to user account
USER developer

# Install Poetry
RUN pip install --upgrade pip
RUN curl -sSL https://install.python-poetry.org | python -
ENV POETRY_CONFIG_VIRTUALENVS_IN_PROJECT true
# RUN poetry completions bash > /etc/bash_completion.d/poetry
