FROM golang:1.18 AS builder

WORKDIR /app

COPY main.go .
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

RUN go mod init guestbook
RUN go mod tidy
RUN go build -o main main.go

FROM ubuntu:18.04

COPY --from=builder /app/main /app/guestbook
COPY --from=builder /app/public/index.html /app/public/index.html
COPY --from=builder /app/public/script.js /app/public/script.js
COPY --from=builder /app/public/style.css /app/public/style.css
COPY --from=builder /app/public/jquery.min.js /app/public/jquery.min.js

WORKDIR /app

CMD ["./guestbook"]

EXPOSE 3000
