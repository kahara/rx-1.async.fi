FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
ENV FREQUENCY=145000000
ENV GAIN=0
ENV SAMPLERATE=2400000

# https://www.rtl-sdr.com/v4/
RUN apt update \
    && apt install -y cmake git libusb-1.0-0-dev pkg-config

RUN git clone https://github.com/rtlsdrblog/rtl-sdr-blog \
    && cd rtl-sdr-blog \
    && mkdir build \
    && cd build \
    && cmake ../ -DINSTALL_UDEV_RULES=ON \
    && make \
    && make install \
    && cp ../rtl-sdr.rules /etc/udev/rules.d/ \
    && ldconfig -v

ENTRYPOINT ["/bin/bash", "-c", "rtl_tcp -a 0.0.0.0 -p 1173 -f ${FREQUENCY} -g ${GAIN} -s ${SAMPLERATE}"]
