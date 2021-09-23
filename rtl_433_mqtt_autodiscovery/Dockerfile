ARG BUILD_FROM
FROM $BUILD_FROM

ENV LANG C.UTF-8

MAINTAINER daemongloom@gmail.com

# Install latest pip
RUN python3 -m ensurepip && \
    pip3 install --no-cache --upgrade pip

# Install rtl_433 mqtt bridge prereq
RUN pip3 install --no-cache paho-mqtt

# Clone rtl_433 repo and copy the latest tested version of the mqtt bridge script
# (latest as of 09/23/2021)
RUN curl -LO https://github.com/halfbakery/rtl_433/raw/f28d838af7706084df6a830186439e555d3387ba/examples/rtl_433_mqtt_hass.py && \
  chmod +x /rtl_433_mqtt_hass.py

# Run script
COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
