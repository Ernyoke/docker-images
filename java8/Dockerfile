FROM ubuntu:20.04 AS builder

RUN apt-get update && \
    apt-get install curl -y  && \
    apt-get install python3-pip -y && \
    pip3 install gdown

RUN mkdir -p /home/java

RUN cd /home/java && \
    gdown https://drive.google.com/uc?id=1ir1iU6h3Aygn8KcIxaXWoBD9DQZS2IG0

FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN mkdir -p /home/java

WORKDIR /home/java

RUN apt-get update && \
    apt-get install git -y && \
    apt-get install unzip -y && \
    git clone https://github.com/chrishantha/install-java.git

COPY --from=builder /home/java/jdk-8u221-linux-x64.tar.gz .

RUN yes | ./install-java/install-java.sh -f jdk-8u221-linux-x64.tar.gz

RUN rm -rf *