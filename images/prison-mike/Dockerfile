FROM zot24/clawdbot-docker:latest

# Install gog (Google Workspace CLI - Gmail, Calendar, Drive, Contacts, Docs)
RUN git clone https://github.com/steipete/gogcli.git /tmp/gogcli && \
    cd /tmp/gogcli && \
    go build -o /usr/local/bin/gog . && \
    rm -rf /tmp/gogcli && \
    gog --help | head -1

# Install pyicloud (iCloud access - Reminders, Calendar, Notes, Photos, Contacts)
RUN pip install --no-cache-dir pyicloud keyring keyrings.alt && \
    icloud --help | head -1
