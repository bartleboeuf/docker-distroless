FROM alpine as builder
RUN apk -U add curl upx && upx /usr/bin/curl
RUN echo "dummy:x:999:999::/tmp:/bin/false" > /tmp/passwd
FROM scratch
USER dummy
COPY --from=builder /tmp/passwd /etc/passwd
#COPY --from=builder /bin/false /bin/false
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /lib/ld-musl-x86_64.so.1 /lib/ld-musl-x86_64.so.1
COPY --from=builder /usr/lib/libbrotli* /usr/lib/
COPY --from=builder /usr/lib/libnghttp2.so.* /usr/lib/
COPY --from=builder /usr/lib/libcurl.so.* /usr/lib/
COPY --from=builder /lib/libz.so.* /usr/lib/
COPY --from=builder /lib/libssl.so.* /lib/
COPY --from=builder /lib/libcrypto.so.* /lib/
COPY --from=builder /usr/bin/curl /usr/bin/curl
ENTRYPOINT ["/usr/bin/curl"]
CMD ["--version"]
