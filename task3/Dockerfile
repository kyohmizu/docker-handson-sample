FROM alpine

RUN apt install -y iputils-ping

# TARGETPATH には初期値として /test/ を設定したい
COPY ./text ${TARGETPATH}

CMD ["sh", "-c", "echo TARGETPATH=${TARGETPATH}; ping -c 4 8.8.8.8; tree ${TARGETPATH}"]
