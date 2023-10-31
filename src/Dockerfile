# ビルドステージ
FROM golang:latest AS build

WORKDIR /src

COPY . ./

RUN go mod init example

RUN go mod tidy

# バイナリをビルド
RUN CGO_ENABLED=0 go build -o main main.go

# 最終ステージ
FROM alpine:latest

# ビルドステージからバイナリのみをコピー
COPY --from=build /src/main /app/main

# コンテナ内の作業ディレクトリを設定
WORKDIR /app

# debug時はコメントアウト
CMD ["/app/main"]