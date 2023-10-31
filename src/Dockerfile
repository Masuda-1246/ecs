# ビルドステージ
FROM golang:latest AS build

WORKDIR /src

COPY go.mod ./
COPY go.sum ./

RUN go mod download

COPY . .

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