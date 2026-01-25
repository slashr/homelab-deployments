FROM ghcr.io/zot24/clawdbot-docker:latest

# Install pyicloud (iCloud access - Reminders, Calendar, Notes, Photos, Contacts)
RUN pip install --no-cache-dir --break-system-packages \
    pyicloud==2.2.0 \
    keyring==25.7.0 \
    keyrings.alt==5.0.2 && \
    icloud --help | head -1
