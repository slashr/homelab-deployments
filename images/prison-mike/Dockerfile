FROM ghcr.io/zot24/clawdbot-docker:latest

# Install gog (Google Workspace CLI - Gmail, Calendar, Drive, Contacts, Docs)
WORKDIR /tmp/gogcli
RUN git clone https://github.com/steipete/gogcli.git . && \
    make && \
    cp bin/gog /usr/local/bin/gog && \
    rm -rf /tmp/gogcli && \
    gog --help | head -1

WORKDIR /root

# Install pyicloud (iCloud access - Reminders, Calendar, Notes, Photos, Contacts)
RUN pip install --no-cache-dir \
    pyicloud==2.2.0 \
    keyring==25.7.0 \
    keyrings.alt==5.0.2 && \
    icloud --help | head -1
