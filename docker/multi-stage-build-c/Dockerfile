# Dockerfile
FROM ubuntu:18.04 as builder
RUN apt-get update -y
RUN apt-get install -y gcc

WORKDIR /tmp
COPY hello.c .
RUN gcc hello.c
RUN ls -l a.out

FROM ubuntu:20.04
WORKDIR /root
COPY --from=builder /tmp/a.out .
ENTRYPOINT [ "./a.out" ]

# docker build -t aout .
# docker run aout

