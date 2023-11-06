FROM golang:1.21 as build

WORKDIR /catgpt

COPY ./catgpt/go.mod ./catgpt/go.sum ./
RUN go mod download

COPY ./catgpt/*.png ./
COPY ./catgpt/tpl/index.html ./tpl/index.html
COPY ./catgpt/*.go ./


RUN CGO_ENABLED=0 go build -o app


FROM  gcr.io/distroless/static-debian12 as base

COPY --from=build /catgpt/app /catgpt/app 

EXPOSE 8080
EXPOSE 9090


ENTRYPOINT ["/catgpt/app"]
