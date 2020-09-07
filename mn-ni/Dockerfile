FROM oracle/graalvm-ce:20.1.0-java11 as graalvm
RUN gu install native-image

COPY . /home/app/mn-ni
WORKDIR /home/app/mn-ni

RUN native-image --no-server -cp target/mn-ni-*.jar

FROM frolvlad/alpine-glibc
RUN apk update && apk add libstdc++
EXPOSE 8080
COPY --from=graalvm /home/app/mn-ni/mn-ni /app/mn-ni
ENTRYPOINT ["/app/mn-ni"]
