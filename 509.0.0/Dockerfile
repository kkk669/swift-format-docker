ARG SWIFT_FORMAT_VERSION=509.0.0
ARG SWIFT_TAG=5.9-jammy

FROM swift:${SWIFT_TAG} as build
ARG SWIFT_FORMAT_VERSION
WORKDIR /root
RUN git clone --depth 1 --branch ${SWIFT_FORMAT_VERSION} https://github.com/apple/swift-format.git \
  && cd swift-format \
  && swift build --product swift-format -c release -Xswiftc -static-stdlib \
  && strip .build/release/swift-format

FROM debian:bookworm-slim
COPY --from=build /root/swift-format/.build/release/swift-format /usr/bin/swift-format
ENTRYPOINT ["/usr/bin/swift-format"]
CMD ["--help"]
