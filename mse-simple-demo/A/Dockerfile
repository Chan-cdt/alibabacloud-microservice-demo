FROM eclipse-temurin:8-jdk-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add --no-cache libstdc++

RUN mkdir /usr/local/async-profiler/ -p && \
    wget -O /usr/local/async-profiler/async-profiler.tar.gz \
    https://ghproxy.com/https://github.com/jvm-profiling-tools/async-profiler/releases/download/v2.8/async-profiler-2.8-linux-musl-x64.tar.gz && \
    cd /usr/local/async-profiler/ &&\
    tar -xvzf async-profiler.tar.gz &&\
    rm -f /usr/local/async-profiler/async-profiler.tar.gz

WORKDIR /app
COPY /target/A-1.0.0.jar /app

EXPOSE 20001
ENTRYPOINT ["sh", "-c"]
CMD ["java -agentpath:/usr/local/async-profiler/async-profiler-2.8-linux-musl-x64/build/libasyncProfiler.so=start,event=cpu,file=profile.html -jar /app/A-1.0.0.jar"]