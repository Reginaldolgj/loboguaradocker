FROM ubuntu:24.04

ARG REQ_PYTHON="python3 python3-pip python3-venv libpq-dev python3-dev"
ARG REQ_REDIS="redis-server"
ARG REQ_POSTGRES="postgresql-contrib"

RUN apt update \
    && DEBIAN_FRONTEND=noninteractive \
      apt install -y $REQ_PYTHON $REQ_REDIS $REQ_POSTGRES \
      net-tools \
      git \
      curl \
      build-essential \
      zip \
      wget \
      unzip \
      tzdata \
      sudo

RUN mkdir -p /opt/loboguara/bin/
RUN wget -O /tmp/google-chrome.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i /tmp/google-chrome.deb || apt-get install -f -y
RUN ln -sf /usr/bin/google-chrome /opt/loboguara/bin/google-chrome
RUN wget -O /tmp/chromedriver.zip https://edgedl.me.gvt1.com/edgedl/chrome/chrome-for-testing/131.0.6778.69/linux64/chromedriver-linux64.zip
RUN unzip /tmp/chromedriver.zip -d /tmp/
RUN mv /tmp/chromedriver-linux64/ /opt/loboguara/bin/chromedriver_dir
RUN chmod +x /opt/loboguara/bin/chromedriver_dir/chromedriver
RUN ln -sf /opt/loboguara/bin/chromedriver_dir/chromedriver /opt/loboguara/bin/chromedriver

RUN wget -O /tmp/subfinder.zip https://github.com/projectdiscovery/subfinder/releases/download/v2.6.6/subfinder_2.6.6_linux_amd64.zip && \
    unzip /tmp/subfinder.zip -d /tmp/ && \
    mv /tmp/subfinder /opt/loboguara/bin/ && \
    chmod +x /opt/loboguara/bin/subfinder

RUN wget -O /tmp/ffuf.tar.gz https://github.com/ffuf/ffuf/releases/download/v2.0.0/ffuf_2.0.0_linux_amd64.tar.gz && \
    tar -xvzf /tmp/ffuf.tar.gz -C /tmp/ && \
    mv /tmp/ffuf /opt/loboguara/bin/ && \
    chmod +x /opt/loboguara/bin/ffuf

WORKDIR /home/ubuntu/

RUN git clone https://github.com/olivsec/loboguara.git

WORKDIR /home/ubuntu/loboguara

COPY ./install.sh /home/ubuntu/loboguara/install.sh 

COPY ./config.py /home/ubuntu/loboguara/server/app/config.py

RUN rm -rf /tmp/*

RUN chmod +x /home/ubuntu/loboguara/install.sh

RUN apt clean \
    && rm -rf /var/lib/apt/lists/*

CMD ["sleep", "infinity"]