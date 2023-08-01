## Overview for: `scenarios/fed-v1-constant-vus-over-time`


This scenario runs 4 subgraphs and a GraphQL gateway with Federation v1 spec, and runs a heavy query. It's being executed with a constant amount of VUs over a fixed amount of time. It measure things like memory usage, CPU usage, average RPS. It also includes a summary of the entire execution, and metrics information about HTTP execution times.


This scenario was running 100 VUs over 60s


### Comparison


| Gateway                             | RPS ⬇️ |       Requests        |         Duration         |
| :---------------------------------- | :----: | :-------------------: | :----------------------: |
| wundergraph                         |  690   | 41498 total, 0 failed |  avg: 143ms, p95: 227ms  |
| apollo-router                       |   94   | 5711 total, 0 failed  | avg: 1056ms, p95: 1451ms |
| stitching-federation-with-yoga-bun  |   90   | 5491 total, 0 failed  | avg: 1096ms, p95: 1568ms |
| mesh                                |   67   | 4126 total, 0 failed  | avg: 1466ms, p95: 2241ms |
| mercurius                           |   66   | 3989 total, 0 failed  | avg: 1508ms, p95: 1985ms |
| stitching-federation-with-yoga-deno |   66   | 4026 total, 0 failed  | avg: 1502ms, p95: 2098ms |
| stitching-federation-with-yoga-uws  |   60   | 3693 total, 0 failed  | avg: 1642ms, p95: 2358ms |
| apollo-server                       |   55   | 3395 total, 0 failed  | avg: 1785ms, p95: 2181ms |
| mesh-supergraph                     |   55   | 3368 total, 0 failed  | avg: 1798ms, p95: 3000ms |
| apollo-gateway-with-yoga            |   51   | 3117 total, 0 failed  | avg: 1946ms, p95: 2250ms |
| apollo-gateway-with-yoga-uws        |   49   | 3044 total, 0 failed  | avg: 1989ms, p95: 2685ms |
| stitching-federation-with-yoga      |   45   | 2796 total, 0 failed  | avg: 2171ms, p95: 3042ms |



<details>
  <summary>Summary for: `wundergraph`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 124494     ✗ 0    
     data_received..................: 207 MB  3.4 MB/s
     data_sent......................: 49 MB   820 kB/s
     http_req_blocked...............: avg=7.45µs   min=800ns   med=1.8µs    max=9.29ms   p(90)=2.8µs    p(95)=3.4µs   
     http_req_connecting............: avg=3.66µs   min=0s      med=0s       max=4.85ms   p(90)=0s       p(95)=0s      
     http_req_duration..............: avg=143.04ms min=21.65ms med=136.36ms max=485.07ms p(90)=202.41ms p(95)=227.01ms
       { expected_response:true }...: avg=143.04ms min=21.65ms med=136.36ms max=485.07ms p(90)=202.41ms p(95)=227.01ms
   ✓ http_req_failed................: 0.00%   ✓ 0          ✗ 41498
     http_req_receiving.............: avg=1.07ms   min=13.8µs  med=30.7µs   max=161.32ms p(90)=183.49µs p(95)=1.5ms   
     http_req_sending...............: avg=317.4µs  min=5.4µs   med=10.2µs   max=165.57ms p(90)=20.7µs   p(95)=95.9µs  
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s       max=0s       p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=141.65ms min=21.57ms med=135.3ms  max=485.03ms p(90)=199.9ms  p(95)=223.63ms
     http_reqs......................: 41498   690.477016/s
     iteration_duration.............: avg=144.7ms  min=22.47ms med=137.9ms  max=523.97ms p(90)=204.28ms p(95)=229.31ms
     iterations.....................: 41498   690.477016/s
     vus............................: 100     min=100      max=100
     vus_max........................: 100     min=100      max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/bdce6284-7755-4792-615e-aeaf11e01000/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/e048dd1c-bdaa-458a-f56b-79e7ebc0a100/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-router`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 5705 / ✗ 6
     ✗ valid response structure
      ↳  99% — ✓ 5705 / ✗ 6

     checks.........................: 99.92% ✓ 17121     ✗ 12   
     data_received..................: 28 MB  470 kB/s
     data_sent......................: 6.8 MB 112 kB/s
     http_req_blocked...............: avg=111.81µs min=1.4µs    med=3.2µs    max=14.21ms p(90)=4.5µs  p(95)=8.9µs  
     http_req_connecting............: avg=106.35µs min=0s       med=0s       max=14.11ms p(90)=0s     p(95)=0s     
     http_req_duration..............: avg=1.05s    min=356.46ms med=996.09ms max=5.82s   p(90)=1.32s  p(95)=1.45s  
       { expected_response:true }...: avg=1.05s    min=356.46ms med=996.09ms max=5.82s   p(90)=1.32s  p(95)=1.45s  
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 5711 
     http_req_receiving.............: avg=74.65µs  min=24.9µs   med=67.5µs   max=10.8ms  p(90)=90.2µs p(95)=96.55µs
     http_req_sending...............: avg=53.74µs  min=7.5µs    med=19µs     max=13.26ms p(90)=35.5µs p(95)=45.2µs 
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s       max=0s      p(90)=0s     p(95)=0s     
     http_req_waiting...............: avg=1.05s    min=356.35ms med=995.97ms max=5.82s   p(90)=1.32s  p(95)=1.45s  
     http_reqs......................: 5711   94.280098/s
     iteration_duration.............: avg=1.05s    min=357.32ms med=996.86ms max=5.83s   p(90)=1.32s  p(95)=1.45s  
     iterations.....................: 5711   94.280098/s
     vus............................: 100    min=100     max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/b31a0c54-4a57-4690-ff9d-dd5003257700/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/3faaa4c7-9969-468d-d40a-c44371bd1700/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga-bun`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 16473     ✗ 0    
     data_received..................: 27 MB   453 kB/s
     data_sent......................: 6.5 MB  108 kB/s
     http_req_blocked...............: avg=137.62µs min=1.3µs    med=2.4µs  max=16.25ms p(90)=4µs    p(95)=13.1µs  
     http_req_connecting............: avg=132.02µs min=0s       med=0s     max=16.06ms p(90)=0s     p(95)=0s      
     http_req_duration..............: avg=1.09s    min=348.18ms med=1.02s  max=2.75s   p(90)=1.36s  p(95)=1.56s   
       { expected_response:true }...: avg=1.09s    min=348.18ms med=1.02s  max=2.75s   p(90)=1.36s  p(95)=1.56s   
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 5491 
     http_req_receiving.............: avg=98.78µs  min=19.9µs   med=51.4µs max=18.73ms p(90)=76.9µs p(95)=101µs   
     http_req_sending...............: avg=170.23µs min=8µs      med=14.1µs max=25.85ms p(90)=32.5µs p(95)=158.46µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s     p(95)=0s      
     http_req_waiting...............: avg=1.09s    min=347.85ms med=1.02s  max=2.75s   p(90)=1.36s  p(95)=1.56s   
     http_reqs......................: 5491    90.962539/s
     iteration_duration.............: avg=1.09s    min=356.41ms med=1.02s  max=2.75s   p(90)=1.37s  p(95)=1.56s   
     iterations.....................: 5491    90.962539/s
     vus............................: 100     min=100     max=100
     vus_max........................: 100     min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/cde223de-240a-4aaa-9b58-b5fff38b3e00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/d245df8c-8b99-41d8-29dd-5b22bf197100/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mesh`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 4122 / ✗ 4
     ✗ valid response structure
      ↳  99% — ✓ 4122 / ✗ 4

     checks.........................: 99.93% ✓ 12370     ✗ 8    
     data_received..................: 21 MB  339 kB/s
     data_sent......................: 4.9 MB 81 kB/s
     http_req_blocked...............: avg=181.14µs min=1.6µs    med=2.9µs   max=16.65ms p(90)=4.4µs  p(95)=9.85µs 
     http_req_connecting............: avg=174.18µs min=0s       med=0s      max=16.38ms p(90)=0s     p(95)=0s     
     http_req_duration..............: avg=1.46s    min=790.74ms med=1.37s   max=3.56s   p(90)=1.88s  p(95)=2.24s  
       { expected_response:true }...: avg=1.46s    min=790.74ms med=1.37s   max=3.56s   p(90)=1.88s  p(95)=2.24s  
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 4126 
     http_req_receiving.............: avg=84.98µs  min=25µs     med=63.25µs max=21.22ms p(90)=89.8µs p(95)=98.2µs 
     http_req_sending...............: avg=115.76µs min=8.9µs    med=16.7µs  max=14.88ms p(90)=32.3µs p(95)=44.05µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s      max=0s      p(90)=0s     p(95)=0s     
     http_req_waiting...............: avg=1.46s    min=790.61ms med=1.37s   max=3.56s   p(90)=1.88s  p(95)=2.24s  
     http_reqs......................: 4126   67.882639/s
     iteration_duration.............: avg=1.46s    min=791.4ms  med=1.37s   max=3.56s   p(90)=1.88s  p(95)=2.24s  
     iterations.....................: 4126   67.882639/s
     vus............................: 100    min=100     max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/68925a95-aaac-48b6-afa6-f62318e91400/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/477ca80d-d9ae-4be2-d129-bd9f33a4f000/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mercurius`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 11967     ✗ 0    
     data_received..................: 20 MB   332 kB/s
     data_sent......................: 4.7 MB  78 kB/s
     http_req_blocked...............: avg=242.58µs min=1.5µs    med=3.3µs  max=24.85ms p(90)=4.89µs p(95)=18.6µs
     http_req_connecting............: avg=230.37µs min=0s       med=0s     max=24.81ms p(90)=0s     p(95)=0s    
     http_req_duration..............: avg=1.5s     min=396.48ms med=1.42s  max=5.92s   p(90)=1.71s  p(95)=1.98s 
       { expected_response:true }...: avg=1.5s     min=396.48ms med=1.42s  max=5.92s   p(90)=1.71s  p(95)=1.98s 
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 3989 
     http_req_receiving.............: avg=74.66µs  min=24.6µs   med=68µs   max=8.64ms  p(90)=90.6µs p(95)=97.4µs
     http_req_sending...............: avg=47.86µs  min=8.4µs    med=18.1µs max=9.85ms  p(90)=35.6µs p(95)=99.4µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s     p(95)=0s    
     http_req_waiting...............: avg=1.5s     min=396.43ms med=1.42s  max=5.92s   p(90)=1.71s  p(95)=1.98s 
     http_reqs......................: 3989    66.043593/s
     iteration_duration.............: avg=1.5s     min=397.11ms med=1.42s  max=5.93s   p(90)=1.71s  p(95)=1.98s 
     iterations.....................: 3989    66.043593/s
     vus............................: 100     min=100     max=100
     vus_max........................: 100     min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/0c72c858-ce0a-4058-c477-71e77da71e00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/cba7fa79-e2c2-4bad-0ace-fb79cb5f7500/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga-deno`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 4020 / ✗ 6
     ✗ valid response structure
      ↳  99% — ✓ 4020 / ✗ 6

     checks.........................: 99.90% ✓ 12066     ✗ 12   
     data_received..................: 20 MB  335 kB/s
     data_sent......................: 4.8 MB 79 kB/s
     http_req_blocked...............: avg=200.52µs min=1.2µs    med=2.6µs  max=17.41ms p(90)=4.2µs  p(95)=10.52µs 
     http_req_connecting............: avg=194.44µs min=0s       med=0s     max=17.28ms p(90)=0s     p(95)=0s      
     http_req_duration..............: avg=1.5s     min=797.97ms med=1.44s  max=2.71s   p(90)=1.82s  p(95)=2.09s   
       { expected_response:true }...: avg=1.5s     min=797.97ms med=1.44s  max=2.71s   p(90)=1.82s  p(95)=2.09s   
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 4026 
     http_req_receiving.............: avg=137.87µs min=19.8µs   med=41.3µs max=26.3ms  p(90)=90.9µs p(95)=133.2µs 
     http_req_sending...............: avg=127.19µs min=7.5µs    med=15.1µs max=22.63ms p(90)=39µs   p(95)=149.18µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s     p(95)=0s      
     http_req_waiting...............: avg=1.5s     min=797.81ms med=1.44s  max=2.71s   p(90)=1.82s  p(95)=2.09s   
     http_reqs......................: 4026   66.237349/s
     iteration_duration.............: avg=1.5s     min=798.66ms med=1.44s  max=2.71s   p(90)=1.82s  p(95)=2.09s   
     iterations.....................: 4026   66.237349/s
     vus............................: 100    min=100     max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/6786222d-f332-4c15-4469-73eaf585de00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/e7d37aea-c18c-4a6f-5b89-535f50d4d300/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga-uws`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 3682 / ✗ 11
     ✗ valid response structure
      ↳  99% — ✓ 3682 / ✗ 11

     checks.........................: 99.80% ✓ 11057     ✗ 22   
     data_received..................: 19 MB  303 kB/s
     data_sent......................: 4.4 MB 72 kB/s
     http_req_blocked...............: avg=400.74µs min=1.6µs    med=2.6µs  max=31.59ms p(90)=4.1µs  p(95)=17.78µs 
     http_req_connecting............: avg=384.76µs min=0s       med=0s     max=31.33ms p(90)=0s     p(95)=0s      
     http_req_duration..............: avg=1.64s    min=975.89ms med=1.53s  max=3.31s   p(90)=2.02s  p(95)=2.35s   
       { expected_response:true }...: avg=1.64s    min=975.89ms med=1.53s  max=3.31s   p(90)=2.02s  p(95)=2.35s   
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 3693 
     http_req_receiving.............: avg=67.14µs  min=23.9µs   med=55.6µs max=5.88ms  p(90)=81.3µs p(95)=95.84µs 
     http_req_sending...............: avg=110.06µs min=8.3µs    med=15µs   max=17.69ms p(90)=34.9µs p(95)=146.36µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s     p(95)=0s      
     http_req_waiting...............: avg=1.64s    min=975.8ms  med=1.53s  max=3.31s   p(90)=2.02s  p(95)=2.35s   
     http_reqs......................: 3693   60.532762/s
     iteration_duration.............: avg=1.64s    min=976.76ms med=1.54s  max=3.31s   p(90)=2.02s  p(95)=2.35s   
     iterations.....................: 3693   60.532762/s
     vus............................: 17     min=17      max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/53e4a598-59e0-49ee-5c97-4d968096bc00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/ec5a7884-ce33-4033-1100-b7c1f78f3000/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-server`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 3371 / ✗ 24
     ✗ valid response structure
      ↳  99% — ✓ 3371 / ✗ 24

     checks.........................: 99.52% ✓ 10137     ✗ 48   
     data_received..................: 18 MB  286 kB/s
     data_sent......................: 4.0 MB 66 kB/s
     http_req_blocked...............: avg=123.26µs min=1.5µs    med=2.8µs  max=14.64ms p(90)=4.59µs p(95)=12.92µs
     http_req_connecting............: avg=114.46µs min=0s       med=0s     max=10.08ms p(90)=0s     p(95)=0s     
     http_req_duration..............: avg=1.78s    min=609.59ms med=1.62s  max=20.04s  p(90)=1.94s  p(95)=2.18s  
       { expected_response:true }...: avg=1.78s    min=609.59ms med=1.62s  max=20.04s  p(90)=1.94s  p(95)=2.18s  
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 3395 
     http_req_receiving.............: avg=67.38µs  min=24.3µs   med=63.8µs max=2.63ms  p(90)=89.5µs p(95)=99.13µs
     http_req_sending...............: avg=57.57µs  min=9.79µs   med=16.4µs max=13.9ms  p(90)=30.9µs p(95)=45.26µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s     p(95)=0s     
     http_req_waiting...............: avg=1.78s    min=609.41ms med=1.62s  max=20.04s  p(90)=1.94s  p(95)=2.18s  
     http_reqs......................: 3395   55.689125/s
     iteration_duration.............: avg=1.78s    min=610.63ms med=1.62s  max=20.04s  p(90)=1.94s  p(95)=2.18s  
     iterations.....................: 3395   55.689125/s
     vus............................: 13     min=13      max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/358f80cd-254d-42d5-4ee2-36ae15516500/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/17cbd6e4-0403-40e6-2124-9a5eb5c02400/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mesh-supergraph`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✗ valid response structure
      ↳  0% — ✓ 0 / ✗ 3368

     checks.........................: 66.66% ✓ 6736      ✗ 3368 
     data_received..................: 17 MB  278 kB/s
     data_sent......................: 4.0 MB 66 kB/s
     http_req_blocked...............: avg=570.71µs min=1.7µs    med=3µs     max=36.02ms p(90)=5µs     p(95)=23.65µs 
     http_req_connecting............: avg=544.22µs min=0s       med=0s      max=31.68ms p(90)=0s      p(95)=0s      
     http_req_duration..............: avg=1.79s    min=649.37ms med=1.72s   max=5.47s   p(90)=2.58s   p(95)=2.99s   
       { expected_response:true }...: avg=1.79s    min=649.37ms med=1.72s   max=5.47s   p(90)=2.58s   p(95)=2.99s   
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 3368 
     http_req_receiving.............: avg=87.61µs  min=31.2µs   med=71.59µs max=11.56ms p(90)=128.3µs p(95)=163.26µs
     http_req_sending...............: avg=71.99µs  min=13.1µs   med=18.8µs  max=14.89ms p(90)=50.56µs p(95)=116.32µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s      max=0s      p(90)=0s      p(95)=0s      
     http_req_waiting...............: avg=1.79s    min=649.26ms med=1.72s   max=5.47s   p(90)=2.58s   p(95)=2.99s   
     http_reqs......................: 3368   55.208615/s
     iteration_duration.............: avg=1.79s    min=649.92ms med=1.72s   max=5.5s    p(90)=2.59s   p(95)=3s      
     iterations.....................: 3368   55.208615/s
     vus............................: 24     min=24      max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/801d9e06-d682-4e34-83de-1083d85a7c00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/43e8ceaf-9c61-414e-b9a7-b8d0e022ea00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-gateway-with-yoga`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 3112 / ✗ 5
     ✗ valid response structure
      ↳  99% — ✓ 3112 / ✗ 5

     checks.........................: 99.89% ✓ 9341      ✗ 10   
     data_received..................: 16 MB  257 kB/s
     data_sent......................: 3.7 MB 61 kB/s
     http_req_blocked...............: avg=190.44µs min=1.5µs    med=2.5µs  max=15.13ms p(90)=4µs     p(95)=21.3µs 
     http_req_connecting............: avg=184.78µs min=0s       med=0s     max=14.98ms p(90)=0s      p(95)=0s     
     http_req_duration..............: avg=1.94s    min=944.56ms med=1.79s  max=20.3s   p(90)=2.08s   p(95)=2.25s  
       { expected_response:true }...: avg=1.94s    min=944.56ms med=1.79s  max=20.3s   p(90)=2.08s   p(95)=2.25s  
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 3117 
     http_req_receiving.............: avg=67.91µs  min=25.5µs   med=51.8µs max=14.18ms p(90)=83.3µs  p(95)=96.5µs 
     http_req_sending...............: avg=59.73µs  min=10.1µs   med=14.5µs max=7.43ms  p(90)=36.64µs p(95)=90.21µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s      p(95)=0s     
     http_req_waiting...............: avg=1.94s    min=944.31ms med=1.79s  max=20.3s   p(90)=2.08s   p(95)=2.25s  
     http_reqs......................: 3117   51.010001/s
     iteration_duration.............: avg=1.94s    min=945.22ms med=1.79s  max=20.31s  p(90)=2.09s   p(95)=2.25s  
     iterations.....................: 3117   51.010001/s
     vus............................: 34     min=34      max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/1104a1ce-c4d5-4980-e742-03303bc3ab00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/9961689d-110f-44c2-0512-cc7be2508100/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-gateway-with-yoga-uws`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 3021 / ✗ 23
     ✗ valid response structure
      ↳  99% — ✓ 3021 / ✗ 23

     checks.........................: 99.49% ✓ 9086      ✗ 46   
     data_received..................: 15 MB  250 kB/s
     data_sent......................: 3.6 MB 59 kB/s
     http_req_blocked...............: avg=136.34µs min=1.8µs    med=3µs     max=17.08ms p(90)=4.7µs   p(95)=18.68µs 
     http_req_connecting............: avg=129.64µs min=0s       med=0s      max=16.94ms p(90)=0s      p(95)=0s      
     http_req_duration..............: avg=1.98s    min=949.61ms med=1.88s   max=4.22s   p(90)=2.39s   p(95)=2.68s   
       { expected_response:true }...: avg=1.98s    min=949.61ms med=1.88s   max=4.22s   p(90)=2.39s   p(95)=2.68s   
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 3044 
     http_req_receiving.............: avg=67.88µs  min=22.8µs   med=62.15µs max=2.82ms  p(90)=91.57µs p(95)=101.57µs
     http_req_sending...............: avg=71.22µs  min=7.9µs    med=17.2µs  max=9.82ms  p(90)=37.6µs  p(95)=121.76µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s      max=0s      p(90)=0s      p(95)=0s      
     http_req_waiting...............: avg=1.98s    min=949.56ms med=1.88s   max=4.22s   p(90)=2.39s   p(95)=2.68s   
     http_reqs......................: 3044   49.941161/s
     iteration_duration.............: avg=1.98s    min=950.63ms med=1.89s   max=4.22s   p(90)=2.39s   p(95)=2.68s   
     iterations.....................: 3044   49.941161/s
     vus............................: 5      min=5       max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/0f4869d5-d23f-423d-f194-895da61cd600/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/87c0ec78-5a48-41a2-4613-fe168a712800/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 2781 / ✗ 15
     ✗ valid response structure
      ↳  99% — ✓ 2781 / ✗ 15

     checks.........................: 99.64% ✓ 8358      ✗ 30   
     data_received..................: 14 MB  232 kB/s
     data_sent......................: 3.3 MB 54 kB/s
     http_req_blocked...............: avg=1.02ms   min=2.2µs    med=3.6µs  max=56.09ms p(90)=5.3µs    p(95)=24.7µs  
     http_req_connecting............: avg=985.86µs min=0s       med=0s     max=47.61ms p(90)=0s       p(95)=0s      
     http_req_duration..............: avg=2.17s    min=355.37ms med=1.89s  max=29.46s  p(90)=2.32s    p(95)=3.04s   
       { expected_response:true }...: avg=2.17s    min=355.37ms med=1.89s  max=29.46s  p(90)=2.32s    p(95)=3.04s   
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 2796 
     http_req_receiving.............: avg=88.52µs  min=29.3µs   med=78.4µs max=5.26ms  p(90)=112.25µs p(95)=126.62µs
     http_req_sending...............: avg=108.31µs min=12.9µs   med=22.1µs max=33.72ms p(90)=44.5µs   p(95)=86.2µs  
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=2.17s    min=355.23ms med=1.89s  max=29.46s  p(90)=2.32s    p(95)=3.04s   
     http_reqs......................: 2796   45.629295/s
     iteration_duration.............: avg=2.17s    min=356.34ms med=1.89s  max=29.46s  p(90)=2.32s    p(95)=3.04s   
     iterations.....................: 2796   45.629295/s
     vus............................: 53     min=53      max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/fca7c4d7-2d68-435b-5a68-f5e0d9c80b00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/f1f6cd29-2552-4d78-5177-49f2e52f6d00/public" alt="HTTP Overview" />


  </details>