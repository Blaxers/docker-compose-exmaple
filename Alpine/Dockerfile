FROM alpine:latest

RUN apk add --no-cache openssh-server && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    ssh-keygen -A
RUN echo 'root:password' | chpasswd
RUN mkdir /root/.ssh/
COPY ./key.pub /root/.ssh/authorized_keys

#instalation python 
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools
#open port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]