FROM java:8-jre

# Install base packages
RUN apt-get -y update \
 && apt-get install -y unzip wget gawk cron

# Install dockerize
ENV DOCKERIZE_VERSION v0.3.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Install embulk
RUN wget http://dl.embulk.org/embulk-latest.jar -O /usr/local/bin/embulk && chmod +x /usr/local/bin/embulk

RUN embulk gem install embulk-output-elasticsearch
RUN embulk gem install embulk-input-mysql

# Clean up APT when done.
RUN apt-get remove -y unzip \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


CMD ["/bin/run-cron.sh"]
