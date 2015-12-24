```
# build static binary for linux arch
CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .
```
