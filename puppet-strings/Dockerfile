# Start from the official Ruby 2.3 image
FROM ruby:2.3

LABEL \
  Description="This image is used to run puppet-strings on a module and post the results back to a given URL" \
  Vendor="Puppet, Inc." \
  Version="1.0"

# Install system-level dependencies
RUN apt-get update && apt-get install -y \
  jq

# TODO: install puppet, puppet-strings, and deps using bundler?

# Install puppet
RUN gem install puppet \
  --version 5.4.0 \
  --no-document \
  --silent

# Install rgen
RUN gem install rgen \
  --version 0.8.2 \
  --no-document \
  --silent

# Install puppet-strings
RUN gem install puppet-strings \
  --version 1.2.1 \
  --no-document \
  --silent

# Add a non-root user to run things as
RUN useradd -ms /bin/bash anubis

WORKDIR /home/anubis
USER anubis

# Add build context and set workdir
ADD puppet-strings /home/anubis
ADD shared/entrypoints /home/anubis/bin/shared

# Make a workspace folder
RUN mkdir workspace

# Set default entrypoint
ENTRYPOINT ["/home/anubis/bin/entrypoint"]
