FROM debian:bookworm-slim

# Install systemd and essential packages
RUN apt-get update && \
    apt-get install -y systemd curl openssh-server sudo && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Remove unnecessary systemd services
RUN rm -rf /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/basic.target.wants/* \
    /lib/systemd/system/anaconda.target.wants/*

# Create admin user with sudo privileges
RUN useradd -m -s /bin/bash admin && \
    echo "admin:1234" | chpasswd && \
    usermod -aG sudo admin && \
    echo "admin ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/admin && \
    chmod 440 /etc/sudoers.d/admin

# Configure SSH
RUN mkdir -p /var/run/sshd && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    systemctl enable ssh

# Expose cgroup volume and SSH port
VOLUME [ "/sys/fs/cgroup" ]
EXPOSE 22

# Default command
CMD ["/lib/systemd/systemd"]