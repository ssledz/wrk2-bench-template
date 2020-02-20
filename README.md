## Example

Run web server
```bash
./dummy-web-server.py 8094
```

Do benchmark
```bash
./build.sh
docker run --network host --rm --name wrk -v $(pwd):/opt/wrk/test \
  simple-bench:latest wrk -d 1 -c 4 -t 4 -R 10 http://localhost:8094
```

Print results
```bash
cat out.json
```