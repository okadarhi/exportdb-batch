FROM amazonlinux:2
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN yum update -y
RUN yum install -y java-1.8.0-openjdk wget
RUN wget -q https://dl.embulk.org/embulk-latest.jar -O /bin/embulk \
  && chmod +x /bin/embulk
RUN embulk gem install embulk-input-mysql embulk-output-s3 embulk-formatter-jsonl
COPY config.yml.liquid /work/
WORKDIR /work
ENTRYPOINT ["java", "-jar", "/bin/embulk", "run", "config.yml.liquid"]
