FROM rockylinux/rockylinux:8.8

RUN \
  useradd exporter && \
  dnf update -y && \
  dnf install -y procps tree

CMD ["/home/exporter/node_exporter", "--web.listen-address", "127.0.0.1:8080"]
