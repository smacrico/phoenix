FROM node:18-bullseye

# Create a non-root user or use existing node user
USER node

# Install required dependencies
USER root
RUN apt-get update && apt-get install -y \
    git \
    python3 \
    build-essential \
    ca-certificates \
    curl \
    gnupg \
    && rm -rf /var/lib/apt/lists/*

# Set up npm global directory for node user
RUN mkdir -p /home/node/.npm-global
RUN chown -R node:node /home/node

# Switch to node user
USER node

# Configure npm to use custom global directory
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
ENV PATH=$PATH:/home/node/.npm-global/bin

# Install global npm packages needed for SPFx development
RUN npm install -g \
    @microsoft/generator-sharepoint@1.17.4 \
    gulp-cli@2.3.0 \
    yo@4.3.1 \
    @microsoft/rush@5.94.0

# Create and set working directory
WORKDIR /home/node/spfx-projects

# Set environment variables
ENV NODE_ENV=development

# Expose ports
EXPOSE 4321
EXPOSE 35729

CMD ["bash"]