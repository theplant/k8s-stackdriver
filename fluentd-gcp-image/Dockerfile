# Copyright 2017 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# This Dockerfile will build an image that is configured
# to use Fluentd to collect all Docker container log files
# and then cause them to be ingested using the Google Cloud
# Logging API. This configuration assumes that the host performning
# the collection is a VM that has been created with a logging.write
# scope and that the Logging API has been enabled for the project
# in the Google Developer Console.

FROM ruby:2.6

COPY Gemfile* /

RUN echo 'gem: --no-document' >> /etc/gemrc && \
    gem install --file /Gemfile

# Copy the Fluentd configuration file for logging Docker container logs.
COPY fluent.conf /etc/fluent/fluent.conf
COPY run.sh /run.sh

# Expose prometheus metrics.
EXPOSE 80

# Start Fluentd to pick up our config that watches Docker container logs.
CMD /run.sh $FLUENTD_ARGS
