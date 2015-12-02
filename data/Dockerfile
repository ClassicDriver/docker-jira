##########################################################################################
# ClassicDriver Bitbucket Data Volume Docker Image
##########################################################################################
FROM classicdriver/base

MAINTAINER Team Nitrous <nitrous@classicdriver.com>

# Jira User
ENV RUN_USER            jira

# Jira Home
ENV JIRA_HOME          /var/jira_home

RUN useradd -c "jira role account" -d "$JIRA_HOME" -u 1000 -m -s /bin/bash ${RUN_USER}

VOLUME ["${JIRA_HOME}"]

# Switching user to 'bitbucket' (since this is a data valume and will be used by the bitbucket application container user)
USER ${RUN_USER}

# Command runned once at startup
CMD ["echo", "Data Volume Container for JIRA"]
