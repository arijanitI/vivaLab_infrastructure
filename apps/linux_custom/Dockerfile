FROM alpine:latest

# Update und Installation von nötigen Paketen
RUN apk update && \
    apk add --no-cache nmap openssh && \
    rm -rf /var/cache/apk/* && \
    echo "root:password" | chpasswd

# Konfiguriere den SSH-Dienst für den Zugriff
RUN sed -i 's/#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    mkdir /root/.ssh && \
    touch /root/.ssh/authorized_keys

# Füge einen Benutzer hinzu
RUN adduser -D customuser && \
    echo "customuser:password" | chpasswd

# Generiere Host-Schlüssel
RUN ssh-keygen -A

EXPOSE 22

# Starte den SSH-Dienst
CMD ["/usr/sbin/sshd", "-D", "-e"]

