# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

#
# If this scripted is run out of /usr/bin or some other system bin directory
# it should be linked to and not copied. Things like java jar files are found
# relative to the canonical path of this script.
#

FROM node:slim
LABEL maintainer="github@aadel.io"
LABEL description="The Banana project is a visualization platform for timeseries and non-timeseries data stored in Apache Solr."

RUN apt-get update \
  && apt-get install -y unzip git-core curl \
  && apt-get clean

# Add group
ENV BANANA_GROUP banana
RUN groupadd -r ${BANANA_GROUP}

# Add user
ENV BANANA_USER banana
ENV BANANA_UID 8080
RUN useradd -r -u ${BANANA_UID} -g ${BANANA_GROUP} ${BANANA_USER}

ENV INSTALL_DIR=/opt
RUN mkdir -p ${INSTALL_DIR}

# Install Banana
ENV BANANA_VERSION `cat version`
WORKDIR ${INSTALL_DIR}
RUN curl -L -o ${INSTALL_DIR}/banana-${BANANA_VERSION}.tar.gz http://d1gwqw8biulcc6.cloudfront.net/banana-${BANANA_VERSION}.tar.gz
RUN tar -xvf banana-${BANANA_VERSION}.tar.gz && rm ${INSTALL_DIR}/banana-${BANANA_VERSION}.tar.gz
ENV BANANA_PREFIX ${INSTALL_DIR}/banana-${BANANA_VERSION}
RUN mv dist banana-${BANANA_VERSION}
WORKDIR ${BANANA_PREFIX}
RUN npm -d install
RUN chown -R ${BANANA_USER}:${BANANA_GROUP} ${BANANA_PREFIX}

# Add start and stop script
ADD docker-run.sh /usr/local/bin/
ADD docker-stop.sh /usr/local/bin/

ENV BANANA_HTTP_PORT=9901

EXPOSE ${BANANA_HTTP_PORT}
USER ${BANANA_USER}

CMD ["/usr/local/bin/docker-run.sh"]
