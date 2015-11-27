##########################################################################################
# ClassicDriver PostgreSQL Docker Image for JIRA
##########################################################################################
FROM postgres:9.4

MAINTAINER Team Nitrous <nitrous@classicdriver.com>

# Extending the official postgres image as documented here
# https://github.com/docker-library/docs/tree/master/postgres#how-to-extend-this-image
COPY scripts /docker-entrypoint-initdb.d
