# Use Python 3.7 base image
FROM python:3.7

# Install dependencies and Google Chrome
RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    curl \
    xvfb \
    --no-install-recommends

# Add the Google Chrome repository
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'

# Update and install Google Chrome stable
RUN apt-get update && apt-get install -y \
    google-chrome-stable \
    --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# Install Chromedriver
RUN wget -O /tmp/chromedriver.zip http://chromedriver.storage.googleapis.com/$(curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE)/chromedriver_linux64.zip && \
    unzip /tmp/chromedriver.zip -d /usr/local/bin/ && \
    rm /tmp/chromedriver.zip

# Set display port to avoid crash
ENV DISPLAY=:99

# Upgrade pip and install Seleniumbase
RUN pip install --no-cache-dir --upgrade pip && \
    pip install seleniumbase==4.12.8

# Verify installations (Optional)
RUN python -m seleniumbase --version && \
    chromedriver --version && \
    google-chrome --version

# Default command
CMD ["python"]
