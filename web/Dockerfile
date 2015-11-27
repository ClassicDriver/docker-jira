##########################################################################################
# ClassicDriver Docker image with Jira installed
##########################################################################################
FROM classicdriver/debian-wheezy-java:1.8.60

MAINTAINER Team Nitrous <nitrous@classicdriver.com>

#############################################
# Jira installation
#############################################
RUN apt-get update -qq \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends xmlstarlet \
    && apt-get clean autoclean \
    && apt-get autoremove --yes \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV RUN_USER            jira
ENV RUN_GROUP           jira

ENV JIRA_HOME          /var/jira_home

# Jira is run with user `jira`, uid = 1000
# If you bind mount a volume from the host or a data container,
# ensure you use the same uid
RUN useradd -c "jira role account" -d "$JIRA_HOME" -u 1000 -m -s /bin/bash ${RUN_USER}

# Install Atlassian Jira Software to the following location
ENV JIRA_INSTALL_DIR   /opt/atlassian/jira

ENV JIRA_VERSION 7.0.2
ENV DOWNLOAD_URL        https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${JIRA_VERSION}-jira-${JIRA_VERSION}.tar.gz

ENV CONTEXT_PATH ${JIRA_INSTALL_DIR}

RUN set -x \
    && mkdir -p                          ${JIRA_INSTALL_DIR}                \
    && curl -L --silent                  ${DOWNLOAD_URL} | tar -xz --strip=1 -C "$JIRA_INSTALL_DIR" \
    && rm -rf                            atlassian-jira-software-${JIRA_VERSION}-jira-${JIRA_VERSION}.tar.gz  \
    && chmod -R 700                      ${JIRA_INSTALL_DIR}/logs           \
    && chmod -R 700                      ${JIRA_INSTALL_DIR}/temp           \
    && chmod -R 700                      ${JIRA_INSTALL_DIR}/work           \
    && chown -R ${RUN_USER}:${RUN_GROUP} ${JIRA_INSTALL_DIR}/               \
    && echo                              "jira.home = $JIRA_HOME" > "${JIRA_INSTALL_DIR}/atlassian-jira/WEB-INF/classes/jira-application.properties"

USER ${RUN_USER}:${RUN_GROUP}

VOLUME ["${JIRA_HOME}"]

# HTTP Port
EXPOSE 8080

WORKDIR $JIRA_INSTALL_DIR

# Run in foreground
CMD ["/opt/atlassian/jira/bin/start-jira.sh", "-fg"]
