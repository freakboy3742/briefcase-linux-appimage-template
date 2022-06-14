# Use a manylinux2014 base image
FROM quay.io/pypa/manylinux2014_{{ cookiecutter.arch }}

# Set the working directory
WORKDIR /app

# Set up Docker build arguments
ARG PY_VERSION
ARG SYSTEM_REQUIRES

RUN yum install -y git gcc ${SYSTEM_REQUIRES}

# Ensure Docker user UID:GID matches host user UID:GID (beeware/briefcase#403)
# Use --non-unique to avoid problems when the UID:GID of the host user
# collides with entries provided by the Docker container.
ARG HOST_UID
ARG HOST_GID
RUN groupadd --non-unique --gid $HOST_GID briefcase
RUN useradd --non-unique --uid $HOST_UID --gid $HOST_GID brutus --home /home/brutus

# Create the brutus home directory; ensure that it is owned by brutus.
RUN mkdir -p /home/brutus && chown brutus:briefcase /home/brutus

# Use the brutus user for operations in the container
USER brutus
