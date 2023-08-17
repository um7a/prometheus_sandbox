FROM rockylinux/rockylinux:8.8

RUN \
  useradd prometheus && \
  dnf update -y && \
  dnf install -y procps tree

CMD ["/home/prometheus/prometheus", "--config.file=/home/prometheus/prometheus.yml"]
