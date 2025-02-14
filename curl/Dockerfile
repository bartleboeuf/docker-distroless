FROM alpine AS builder
RUN apk update && apk upgrade && apk -U add curl upx ca-certificates && upx /usr/bin/curl
RUN echo "dummy:x:999:999::/tmp:/bin/false" > /tmp/passwd
RUN upx -9 /usr/lib/libcrypto.so.* /usr/lib/libunistring.so.*.* /usr/lib/libbrotlicommon.so.*.* /usr/lib/libbrotlidec.so.*.* /usr/lib/libbrotlienc.so.*.* /usr/lib/libz.so.*.* /usr/lib/libssl.so.* /usr/lib/libcurl.so.*.* /usr/lib/libnghttp2.so.*.* /usr/lib/libzstd.so.*.* /usr/lib/libcares.so.*.* /usr/lib/libidn2.so.*.* /usr/lib/libpsl.so.*.*
FROM scratch
USER 999:999
COPY --chown=999:999 --from=builder /tmp/passwd /etc/passwd
COPY --chown=999:999 --from=builder /etc/ssl/cert.pem /etc/ssl/cert.pem
COPY --chown=999:999 --from=builder /lib/ld-musl-x86_64.so.1 /lib/ld-musl-x86_64.so.1
COPY --chown=999:999 --from=builder /usr/lib/libbrotlicommon.so.1 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libbrotlidec.so.1 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libbrotlienc.so.1 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libcares.so.2 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libidn2.so.0 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libpsl.so.5 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libzstd.so.1 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libunistring.so.5 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libnghttp2.so.14 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libcurl.so.4 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libz.so.1 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libssl.so.3 /usr/lib/
COPY --chown=999:999 --from=builder /usr/lib/libcrypto.so.3 /usr/lib/
COPY --chown=999:999 --from=builder /usr/bin/curl /usr/bin/curl
ENTRYPOINT ["/usr/bin/curl"]
CMD ["--version"]
