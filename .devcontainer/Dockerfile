# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Use an official lightweight Python image.
# https://hub.docker.com/_/python
FROM python:3.11.1-slim-bullseye

ENV APP_HOME /app
WORKDIR $APP_HOME

# Removes output stream buffering, allowing for more efficient logging
ENV PYTHONUNBUFFERED 1
ENV GRPC_POLL_STRATEGY=epoll1
RUN apt-get update && apt-get install --fix-broken gcc redis-server supervisor libffi-dev libssl-dev python3-dev -y

# Install dependencies
COPY requirements.txt .
RUN pip install --upgrade pip wheel
# Needed to install clearbit
RUN pip install setuptools==57.5.0 --force-reinstall
# End of Needed to install clearbit
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
# Create the user
