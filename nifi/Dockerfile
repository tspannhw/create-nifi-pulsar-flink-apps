FROM apache/nifi:1.19.0

# Set the working directory to /app
COPY --chown=nifi:nifi nifi-pulsar-client-service-nar-1.18.0.nar /opt/nifi/nifi-current/lib/
COPY --chown=nifi:nifi nifi-pulsar-nar-1.18.0.nar /opt/nifi/nifi-current/lib/
