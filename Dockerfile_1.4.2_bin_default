FROM armhfbuild/buildpack-deps:jessie-scm

# gcc for cgo
RUN apt-get update && apt-get install -y --no-install-recommends \
    g++ \
    gcc \
    libc6-dev \
    make \
  && rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION 1.4.2
ENV GOLANG_DOWNLOAD_URL http://dave.cheney.net/paste/go$GOLANG_VERSION.linux-arm~multiarch-armv7-1.tar.gz
ENV GOLANG_DOWNLOAD_SHA1 607573c55dc89d135c3c9c84bba6ba6095a37a1e

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
  && echo "$GOLANG_DOWNLOAD_SHA1  golang.tar.gz" | sha1sum -c - \
  && tar -C /usr/local -xzf golang.tar.gz \
  && rm golang.tar.gz

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/
