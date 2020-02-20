## Example

Run web server
```bash
./dummy-web-server.py 8094
```

Prepare test input and save it to `in.json`

```bash
[
  {
    "url": "http://localhost:8094/user",
    "method": "post",
    "headers": [
      {
        "key": "Host",
        "value": "domain.io"
      },
      {
        "key": "User-Agent",
        "value": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:72.0) Gecko/20100101 Firefox/72.0"
      }
    ],
    "payload": {
      "username": "gabi",
      "age": 3
    }
  },
  {
    "url": "http://localhost:8094/user/1",
    "method": "put",
    "payload": {
      "username": "yuri",
      "age": 13
    }
  },
  {
    "url": "http://localhost:8094/user/1",
    "method": "get"
  },
  {
    "url": "http://localhost:8094/user/2"
  },
  {
    "url": "http://localhost:8094/home",
    "method": "head"
  }
]

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