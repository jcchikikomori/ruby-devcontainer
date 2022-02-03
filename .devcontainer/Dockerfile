# [Choice] Ruby version (use -bullseye variants on local arm64/Apple Silicon): 3, 3.0, 2, 2.7, 2.6, 3-bullseye, 3.0-bullseye, 2-bullseye, 2.7-bullseye, 2.6-bullseye, 3-buster, 3.0-buster, 2-buster, 2.7-buster, 2.6-buster
ARG VARIANT=2-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/ruby:0-${VARIANT}

# Install RVM
ENV GEM_PATH="/usr/local/rvm/gems/default:/usr/local/rvm/gems/default@global" \
    GEM_HOME="/usr/local/rvm/gems/default" \
    MY_RUBY_HOME="/usr/local/rvm/rubies/default" \
    PATH="/usr/local/rvm/rubies/default/bin:/usr/local/rvm/gems/default@global/bin:/usr/local/rvm/rubies/default/bin:/usr/local/rvm/bin:${PATH}"
# COPY library-scripts/ruby-debian.sh /tmp/library-scripts/
# RUN apt-get update && bash /tmp/library-scripts/ruby-debian.sh

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="none"
RUN if [ "${NODE_VERSION}" != "none" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# Install Ruby 2.5.3
RUN rvm install 2.5.3 \
    && rvm alias create default 2.5.3

# [Optional] Uncomment this line to install additional gems.
# Install nokogiri manually since the latest version doesn't supports 2.5
RUN gem install nokogiri -v 1.12.5
RUN gem install rubocop solargraph

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1
RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g commitizen Bannerwise/cz-jira-smart-commit#master" 2>&1
RUN su vscode -c "echo '{ \"path\": \"cz-jira-smart-commit\" }' > /home/vscode/.czrc"

# Install Oh-My-Bash
RUN su vscode -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)" 2>&1

# Copy SSH files
COPY secrets/id_rsa_shared /home/vscode/.ssh/id_rsa
RUN chown -R vscode:vscode /home/vscode/.ssh

# Add to SSH Agent
# RUN ssh-add /home/vscode/.ssh/id_rsa_shared

# Copy Configs
COPY secrets/.env .env
COPY secrets/database.yml config/database.yml
# RUN cp config/database.example.yml config/database.yml

# Copy Configs (Global)
COPY secrets/.gitconfig /home/vscode/.gitconfig
