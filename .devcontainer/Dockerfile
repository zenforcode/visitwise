FROM mcr.microsoft.com/devcontainers/python:3.12

# Install system dependencies
RUN apt-get update && apt-get install -y \
    wget gnupg unzip curl \
    libnss3 libxss1 libasound2 libatk1.0-0 libatk-bridge2.0-0 libcups2 \
    libdbus-1-3 libgtk-3-0 libx11-xcb1 libxcomposite1 libxdamage1 libxrandr2 \
    libgbm1 xdg-utils fonts-liberation libappindicator3-1 \
    --no-install-recommends && rm -rf /var/lib/apt/lists/*

# Install Google Chrome
RUN curl -fsSL https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor -o /etc/apt/trusted.gpg.d/google-chrome.gpg && \
    sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list' && \
    apt-get update && apt-get install -y google-chrome-stable

# Install ChromeDriver (matching Chrome version)
RUN wget "https://storage.googleapis.com/chrome-for-testing-public/136.0.7103.94/linux64/chromedriver-linux64.zip"
RUN unzip chromedriver-linux64.zip && mv chromedriver-linux64/chromedriver /usr/local/bin && chmod +x /usr/local/bin/chromedriver

# Set display environment variable for headless Chrome
# Install uv (fast Python installer)

USER vscode
RUN curl -Ls https://astral.sh/uv/install.sh | bash 
ENV PATH="$PATH:/home/vscode/.local/bin"

ENV DISPLAY=:99
