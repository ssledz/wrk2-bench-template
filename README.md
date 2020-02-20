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
cat out.json | jq
```

```
{
  "duration_us": 1204017,
  "latency_us": {
    "max": 412160,
    "mean": 270568.33333333,
    "percentile": {
      "p99": 412415,
      "p90": 408063,
      "p99_999": 412415,
      "p75": 405247,
      "p50": 400895
    },
    "min": 595,
    "stdev": 189775.30407476
  },
  "requests": 13,
  "status": {
    "http_200": 12,
    "http_404": 1
  },
  "velocity_s": {
    "kbytes": 1.6124408957681,
    "requests": 10.797189740676
  },
  "bytes": 1988
}
```

* `xxx_us` - `xxx` in micro seconds
* `xxx_s` - `xxx` in seconds

## Resources

* [ssledz/wrk2-bench:latest](https://github.com/ssledz/dockerland/tree/master/wrk2-bench)
* [wrk](https://github.com/wg/wrk)
* [wrk2](https://github.com/giltene/wrk2)