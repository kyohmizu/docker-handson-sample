FROM alpine

RUN apt install -y iputils-ping

COPY ./text ${TARGETPATH}

CMD ["sh", "-c", "echo TARGETPATH=${TARGETPATH}; ping -c 4 8.8.8.8; tree ${TARGETPATH}"]
