FROM ruby:2.3-onbuild

MAINTAINER your-name <your-email>

ENV RAILS_ENV production

RUN apt-get update -qq && \
    apt-get install -y build-essential libpq-dev nodejs imagemagick && \
    bundle exec rake assets:precompile

EXPOSE 3000
