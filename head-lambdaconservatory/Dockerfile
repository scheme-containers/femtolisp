# -*- mode: dockerfile; coding: utf-8 -*-
FROM debian:buster-slim AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
      build-essential ca-certificates git \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /build
RUN git clone https://github.com/lambdaconservatory/femtolisp.git --depth 1
WORKDIR /build/femtolisp
RUN make
RUN cp -p flisp flisp.boot /usr/local/bin/

FROM debian:buster-slim
COPY --from=build /usr/local/ /usr/local/
RUN ln -s flisp /usr/local/bin/scheme-banner
CMD ["scheme-banner"]
