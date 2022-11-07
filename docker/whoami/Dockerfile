### example Dockerfile
FROM ubuntu
# runs as root at /
RUN apt-get update -y && apt-get upgrade -y

# switch to a non-root user
RUN useradd --create-home appuser
WORKDIR /home/appuser
USER appuser

# runs as non-root user
ENTRYPOINT ["whoami"]
###

