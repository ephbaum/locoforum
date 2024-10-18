FROM mcr.microsoft.com/devcontainers/rust:1

SHELL ["/bin/bash", "-lc"]

ENV DEBIAN_FRONTEND=noninteractive
RUN apt update
RUN apt -y install --no-install-recommends postgresql-client curl git xdg-utils
RUN cargo install loco-cli sea-orm-cli cargo-insta
RUN chown -R vscode /usr/local/cargo

USER vscode

RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.1
RUN echo ". $HOME/.asdf/asdf.sh" >> $HOME/.bashrc

# Source asdf in each command
RUN . $HOME/.asdf/asdf.sh && asdf plugin-add nodejs
RUN . $HOME/.asdf/asdf.sh && asdf install nodejs latest
RUN . $HOME/.asdf/asdf.sh && asdf global nodejs latest

# Ensure corepack is installed
RUN . $HOME/.asdf/asdf.sh && npm install -g corepack

# Debugging commands
RUN . $HOME/.asdf/asdf.sh && asdf --version
RUN . $HOME/.asdf/asdf.sh && node -v
RUN . $HOME/.asdf/asdf.sh && echo $PATH
RUN . $HOME/.asdf/asdf.sh && which node
RUN . $HOME/.asdf/asdf.sh && which corepack

# Ensure pnpm is installed
RUN . $HOME/.asdf/asdf.sh && corepack enable
RUN . $HOME/.asdf/asdf.sh && corepack prepare pnpm@latest --activate

# Debugging commands for pnpm
RUN . $HOME/.asdf/asdf.sh && corepack --version
RUN . $HOME/.asdf/asdf.sh && pnpm --version

COPY .env /.env