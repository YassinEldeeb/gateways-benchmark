## Overview for: `fed-v1-ramping-vus`


This scenario runs 4 subgraphs and a GraphQL gateway with Federation v1 spec, and runs a heavy query. We are running a heavy load of concurrent VUs to measure response time and other stats, during stress. It measure things like memory usage, CPU usage, response times. It also includes a summary of the entire execution, and metrics information about HTTP execution times.


This scenario was trying to reach 1000 concurrent VUs over 60s


### Comparison


| Gateway                             | duration(p95)⬇️ |  RPS  |       Requests        |                       Durations                        |
| :---------------------------------- | :-------------: | :---: | :-------------------: | :----------------------------------------------------: |
| wundergraph                         |     1617ms      |  615  | 43072 total, 0 failed |    avg: 799ms, p95: 1618ms, max: 2331ms, med: 764ms    |
| mesh-supergraph                     |     9838ms      |  93   | 6537 total, 0 failed  |  avg: 5747ms, p95: 9838ms, max: 11751ms, med: 5886ms   |
| mesh                                |     9839ms      |  94   | 6605 total, 0 failed  |  avg: 5721ms, p95: 9840ms, max: 12433ms, med: 5787ms   |
| stitching-federation-with-yoga-bun  |     11427ms     |  120  | 8470 total, 0 failed  |  avg: 4560ms, p95: 11427ms, max: 17713ms, med: 4302ms  |
| mercurius                           |     12496ms     |  74   | 5181 total, 0 failed  |  avg: 7170ms, p95: 12496ms, max: 12842ms, med: 7375ms  |
| apollo-router                       |     13024ms     |  85   | 6340 total, 0 failed  |  avg: 6399ms, p95: 13024ms, max: 16991ms, med: 5659ms  |
| stitching-federation-with-yoga-deno |     13233ms     |  64   | 4579 total, 0 failed  |  avg: 8550ms, p95: 13234ms, max: 15604ms, med: 9439ms  |
| apollo-gateway-with-yoga-uws        |     28699ms     |  43   | 3291 total, 0 failed  | avg: 12498ms, p95: 28700ms, max: 35451ms, med: 10129ms |
| stitching-federation-with-yoga-uws  |     40381ms     |  37   | 3440 total, 0 failed  | avg: 14176ms, p95: 40382ms, max: 49900ms, med: 8925ms  |
| stitching-federation-with-yoga      |     44137ms     |  73   | 6235 total, 0 failed  |  avg: 7048ms, p95: 44137ms, max: 56760ms, med: 1914ms  |
| apollo-gateway-with-yoga            |     47066ms     |  61   | 5255 total, 0 failed  |  avg: 8477ms, p95: 47067ms, max: 57165ms, med: 2408ms  |
| apollo-server                       |     48797ms     |  57   | 4853 total, 0 failed  |  avg: 9294ms, p95: 48797ms, max: 57852ms, med: 2642ms  |



<details>
  <summary>Summary for: `wundergraph`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 129216     ✗ 0     
     data_received..................: 215 MB  3.1 MB/s
     data_sent......................: 51 MB   730 kB/s
     http_req_blocked...............: avg=1.84ms   min=1.1µs   med=2.4µs    max=714.86ms p(90)=4.2µs    p(95)=7.9µs   
     http_req_connecting............: avg=1.81ms   min=0s      med=0s       max=714.79ms p(90)=0s       p(95)=0s      
     http_req_duration..............: avg=799.1ms  min=7.1ms   med=763.82ms max=2.33s    p(90)=1.43s    p(95)=1.61s   
       { expected_response:true }...: avg=799.1ms  min=7.1ms   med=763.82ms max=2.33s    p(90)=1.43s    p(95)=1.61s   
     http_req_failed................: 0.00%   ✓ 0          ✗ 43072 
     http_req_receiving.............: avg=4.27ms   min=16.29µs med=39.3µs   max=534.47ms p(90)=202.89µs p(95)=781.8µs 
     http_req_sending...............: avg=1.98ms   min=7.4µs   med=12.6µs   max=628.66ms p(90)=45.3µs   p(95)=161.33µs
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s       max=0s       p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=792.84ms min=7ms     med=759.44ms max=2.33s    p(90)=1.41s    p(95)=1.6s    
     http_reqs......................: 43072   615.271322/s
     iteration_duration.............: avg=806.1ms  min=7.83ms  med=768.13ms max=2.36s    p(90)=1.44s    p(95)=1.63s   
     iterations.....................: 43072   615.271322/s
     vus............................: 8       min=8        max=998 
     vus_max........................: 1000    min=1000     max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/13b815ca-dc7e-4672-d113-8e9df15e6c00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/f79db69c-4402-44fd-dd8d-884cc391f800/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mesh-supergraph`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 6522 / ✗ 15
     ✗ valid response structure
      ↳  0% — ✓ 0 / ✗ 6537

     checks.........................: 66.59% ✓ 13059     ✗ 6552  
     data_received..................: 33 MB  473 kB/s
     data_sent......................: 7.8 MB 111 kB/s
     http_req_blocked...............: avg=132.68µs min=1.3µs   med=2.4µs  max=19.27ms p(90)=429.58µs p(95)=492.92µs
     http_req_connecting............: avg=118.75µs min=0s      med=0s     max=19.2ms  p(90)=360.32µs p(95)=422.42µs
     http_req_duration..............: avg=5.74s    min=12.33ms med=5.88s  max=11.75s  p(90)=9.29s    p(95)=9.83s   
       { expected_response:true }...: avg=5.74s    min=12.33ms med=5.88s  max=11.75s  p(90)=9.29s    p(95)=9.83s   
     http_req_failed................: 0.00%  ✓ 0         ✗ 6537  
     http_req_receiving.............: avg=61.66µs  min=22.1µs  med=55.8µs max=2.65ms  p(90)=82.84µs  p(95)=93.42µs 
     http_req_sending...............: avg=57.59µs  min=8.69µs  med=13.7µs max=13.8ms  p(90)=62.94µs  p(95)=78.4µs  
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s     max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=5.74s    min=12.25ms med=5.88s  max=11.75s  p(90)=9.29s    p(95)=9.83s   
     http_reqs......................: 6537   93.373322/s
     iteration_duration.............: avg=5.74s    min=12.69ms med=5.88s  max=11.75s  p(90)=9.29s    p(95)=9.83s   
     iterations.....................: 6537   93.373322/s
     vus............................: 8      min=8       max=1000
     vus_max........................: 1000   min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/5c2b5aaf-acb2-4409-f624-a8be2e869700/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/b0402e7a-f4d4-4c40-9bc5-379f7857ed00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mesh`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 19815    ✗ 0     
     data_received..................: 33 MB   472 kB/s
     data_sent......................: 7.8 MB  112 kB/s
     http_req_blocked...............: avg=332.91µs min=1.1µs   med=2.2µs   max=199.83ms p(90)=352.29µs p(95)=396.81µs
     http_req_connecting............: avg=320.08µs min=0s      med=0s      max=199.18ms p(90)=295.59µs p(95)=335.37µs
     http_req_duration..............: avg=5.72s    min=14.35ms med=5.78s   max=12.43s   p(90)=9.08s    p(95)=9.83s   
       { expected_response:true }...: avg=5.72s    min=14.35ms med=5.78s   max=12.43s   p(90)=9.08s    p(95)=9.83s   
     http_req_failed................: 0.00%   ✓ 0        ✗ 6605  
     http_req_receiving.............: avg=57.39µs  min=17.2µs  med=42.69µs max=10.7ms   p(90)=68.69µs  p(95)=77.59µs 
     http_req_sending...............: avg=75.81µs  min=6.5µs   med=12.8µs  max=94.12ms  p(90)=56.55µs  p(95)=73.19µs 
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s      max=0s       p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=5.72s    min=14.28ms med=5.78s   max=12.43s   p(90)=9.08s    p(95)=9.83s   
     http_reqs......................: 6605    94.33652/s
     iteration_duration.............: avg=5.72s    min=14.88ms med=5.78s   max=12.43s   p(90)=9.08s    p(95)=9.84s   
     iterations.....................: 6605    94.33652/s
     vus............................: 8       min=8      max=1000
     vus_max........................: 1000    min=1000   max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/4113786d-f808-4f56-de5e-e98983ab9300/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/fbcaf17c-bd36-4528-4567-bdcef9900900/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga-bun`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 25410      ✗ 0     
     data_received..................: 42 MB   603 kB/s
     data_sent......................: 10 MB   144 kB/s
     http_req_blocked...............: avg=269.47µs min=700ns   med=1.9µs  max=174.63ms p(90)=138.9µs p(95)=324.09µs
     http_req_connecting............: avg=255.53µs min=0s      med=0s     max=174.5ms  p(90)=86.2µs  p(95)=266.72µs
     http_req_duration..............: avg=4.55s    min=13.06ms med=4.3s   max=17.71s   p(90)=6.67s   p(95)=11.42s  
       { expected_response:true }...: avg=4.55s    min=13.06ms med=4.3s   max=17.71s   p(90)=6.67s   p(95)=11.42s  
     http_req_failed................: 0.00%   ✓ 0          ✗ 8470  
     http_req_receiving.............: avg=168.51µs min=16.2µs  med=29.1µs max=137.88ms p(90)=60.21µs p(95)=101.5µs 
     http_req_sending...............: avg=247.75µs min=5.7µs   med=10.9µs max=91.59ms  p(90)=56.11µs p(95)=94.45µs 
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s     max=0s       p(90)=0s      p(95)=0s      
     http_req_waiting...............: avg=4.55s    min=13ms    med=4.3s   max=17.71s   p(90)=6.67s   p(95)=11.42s  
     http_reqs......................: 8470    120.963019/s
     iteration_duration.............: avg=4.56s    min=13.69ms med=4.3s   max=17.71s   p(90)=6.67s   p(95)=11.42s  
     iterations.....................: 8470    120.963019/s
     vus............................: 7       min=7        max=1000
     vus_max........................: 1000    min=1000     max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/52e9a02b-782a-4a5c-9eb3-db9661942400/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/d9e84576-c66b-4ea0-4b84-5367f30be500/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mercurius`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 15543     ✗ 0     
     data_received..................: 26 MB   372 kB/s
     data_sent......................: 6.1 MB  88 kB/s
     http_req_blocked...............: avg=119.15µs min=1.4µs   med=3.4µs  max=16.24ms p(90)=437.7µs p(95)=481.7µs
     http_req_connecting............: avg=101.65µs min=0s      med=0s     max=16.17ms p(90)=364.5µs p(95)=403µs  
     http_req_duration..............: avg=7.17s    min=10.2ms  med=7.37s  max=12.84s  p(90)=11.9s   p(95)=12.49s 
       { expected_response:true }...: avg=7.17s    min=10.2ms  med=7.37s  max=12.84s  p(90)=11.9s   p(95)=12.49s 
     http_req_failed................: 0.00%   ✓ 0         ✗ 5181  
     http_req_receiving.............: avg=78.33µs  min=24.2µs  med=71.5µs max=9.71ms  p(90)=98.1µs  p(95)=111.4µs
     http_req_sending...............: avg=40.49µs  min=7.6µs   med=19.4µs max=3.9ms   p(90)=74.6µs  p(95)=90.9µs 
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s     max=0s      p(90)=0s      p(95)=0s     
     http_req_waiting...............: avg=7.17s    min=10.13ms med=7.37s  max=12.84s  p(90)=11.9s   p(95)=12.49s 
     http_reqs......................: 5181    74.010916/s
     iteration_duration.............: avg=7.17s    min=10.8ms  med=7.37s  max=12.84s  p(90)=11.9s   p(95)=12.49s 
     iterations.....................: 5181    74.010916/s
     vus............................: 6       min=6       max=1000
     vus_max........................: 1000    min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/83a6b5b6-9cdf-46bc-fd88-1bc6b2c1ef00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/6bf09642-9fcc-4410-f5b9-8951f0f39200/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-router`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 6322 / ✗ 18
     ✗ valid response structure
      ↳  99% — ✓ 6322 / ✗ 18

     checks.........................: 99.81% ✓ 18984     ✗ 36    
     data_received..................: 32 MB  427 kB/s
     data_sent......................: 7.5 MB 102 kB/s
     http_req_blocked...............: avg=332.68µs min=1.2µs    med=3.1µs  max=52.5ms  p(90)=421.15µs p(95)=496.52µs
     http_req_connecting............: avg=315.18µs min=0s       med=0s     max=52.06ms p(90)=346.84µs p(95)=415.71µs
     http_req_duration..............: avg=6.39s    min=148.75ms med=5.65s  max=16.99s  p(90)=11.08s   p(95)=13.02s  
       { expected_response:true }...: avg=6.39s    min=148.75ms med=5.65s  max=16.99s  p(90)=11.08s   p(95)=13.02s  
     http_req_failed................: 0.00%  ✓ 0         ✗ 6340  
     http_req_receiving.............: avg=107.68µs min=20.4µs   med=61.3µs max=30.65ms p(90)=98.81µs  p(95)=122.93µs
     http_req_sending...............: avg=63.99µs  min=8.2µs    med=17.2µs max=17ms    p(90)=71.41µs  p(95)=92.3µs  
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=6.39s    min=148.55ms med=5.65s  max=16.99s  p(90)=11.08s   p(95)=13.02s  
     http_reqs......................: 6340   85.673459/s
     iteration_duration.............: avg=6.4s     min=150.1ms  med=5.66s  max=17.1s   p(90)=11.08s   p(95)=13.02s  
     iterations.....................: 6340   85.673459/s
     vus............................: 130    min=53      max=1000
     vus_max........................: 1000   min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/7a6983e2-69ed-4f8d-08f7-68743639aa00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/4b1d3be7-42a4-44c1-42d7-f11db4d43f00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga-deno`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 4572 / ✗ 7
     ✗ valid response structure
      ↳  99% — ✓ 4572 / ✗ 7

     checks.........................: 99.89% ✓ 13723     ✗ 14    
     data_received..................: 23 MB  324 kB/s
     data_sent......................: 5.4 MB 77 kB/s
     http_req_blocked...............: avg=323.3µs  min=1.3µs  med=2.9µs   max=207.06ms p(90)=478.74µs p(95)=549.8µs 
     http_req_connecting............: avg=290.8µs  min=0s     med=0s      max=195.25ms p(90)=398.8µs  p(95)=462.15µs
     http_req_duration..............: avg=8.54s    min=1.09s  med=9.43s   max=15.6s    p(90)=13s      p(95)=13.23s  
       { expected_response:true }...: avg=8.54s    min=1.09s  med=9.43s   max=15.6s    p(90)=13s      p(95)=13.23s  
     http_req_failed................: 0.00%  ✓ 0         ✗ 4579  
     http_req_receiving.............: avg=184.91µs min=17.7µs med=46µs    max=89.67ms  p(90)=114µs    p(95)=229.01µs
     http_req_sending...............: avg=259.73µs min=7.5µs  med=17.89µs max=138.95ms p(90)=89µs     p(95)=120.75µs
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s      max=0s       p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=8.54s    min=1.09s  med=9.43s   max=15.6s    p(90)=13s      p(95)=13.23s  
     http_reqs......................: 4579   64.796538/s
     iteration_duration.............: avg=8.55s    min=1.09s  med=9.44s   max=15.6s    p(90)=13s      p(95)=13.23s  
     iterations.....................: 4579   64.796538/s
     vus............................: 142    min=53      max=1000
     vus_max........................: 1000   min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/25cce3af-9cc5-4614-3e3e-11dbb402eb00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/5a83deab-a97f-4487-b4b1-f91c38a37600/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-gateway-with-yoga-uws`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  61% — ✓ 2032 / ✗ 1259
     ✗ valid response structure
      ↳  61% — ✓ 2032 / ✗ 1259

     checks.........................: 74.49% ✓ 7355      ✗ 2518  
     data_received..................: 14 MB  191 kB/s
     data_sent......................: 3.9 MB 52 kB/s
     http_req_blocked...............: avg=359.11µs min=1.6µs    med=3.1µs  max=113ms    p(90)=634.4µs p(95)=820.01µs
     http_req_connecting............: avg=320.77µs min=0s       med=0s     max=112.66ms p(90)=530.6µs p(95)=699.7µs 
     http_req_duration..............: avg=12.49s   min=120.61ms med=10.12s max=35.45s   p(90)=25.56s  p(95)=28.69s  
       { expected_response:true }...: avg=12.49s   min=120.61ms med=10.12s max=35.45s   p(90)=25.56s  p(95)=28.69s  
     http_req_failed................: 0.00%  ✓ 0         ✗ 3291  
     http_req_receiving.............: avg=130.78µs min=22µs     med=69.9µs max=36.27ms  p(90)=131.6µs p(95)=174.8µs 
     http_req_sending...............: avg=138.47µs min=10.3µs   med=24.1µs max=29.16ms  p(90)=113.5µs p(95)=161.5µs 
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s     max=0s       p(90)=0s      p(95)=0s      
     http_req_waiting...............: avg=12.49s   min=120.43ms med=10.12s max=35.45s   p(90)=25.56s  p(95)=28.69s  
     http_reqs......................: 3291   43.905269/s
     iteration_duration.............: avg=12.49s   min=121.32ms med=10.13s max=35.45s   p(90)=25.56s  p(95)=28.7s   
     iterations.....................: 3291   43.905269/s
     vus............................: 218    min=0       max=1000
     vus_max........................: 1000   min=973     max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/b6cf8cbc-9091-4576-8883-9ef7c2b02600/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/5049eb01-0a25-4aa3-4ee1-8a50eb460900/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga-uws`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  63% — ✓ 2198 / ✗ 1242
     ✗ valid response structure
      ↳  63% — ✓ 2198 / ✗ 1242

     checks.........................: 75.93% ✓ 7836      ✗ 2484  
     data_received..................: 27 MB  299 kB/s
     data_sent......................: 4.1 MB 45 kB/s
     http_req_blocked...............: avg=629.79µs min=1.5µs    med=2.8µs   max=148.03ms p(90)=515.48µs p(95)=618.63µs
     http_req_connecting............: avg=597.28µs min=0s       med=0s      max=147.96ms p(90)=431.53µs p(95)=526.22µs
     http_req_duration..............: avg=14.17s   min=904.36ms med=8.92s   max=49.9s    p(90)=33.33s   p(95)=40.38s  
       { expected_response:true }...: avg=14.17s   min=904.36ms med=8.92s   max=49.9s    p(90)=33.33s   p(95)=40.38s  
     http_req_failed................: 0.00%  ✓ 0         ✗ 3440  
     http_req_receiving.............: avg=102.71µs min=27.79µs  med=70.2µs  max=25.78ms  p(90)=143.11µs p(95)=190.53µs
     http_req_sending...............: avg=113.55µs min=10.8µs   med=19.84µs max=31.83ms  p(90)=85.6µs   p(95)=117.72µs
     http_req_tls_handshaking.......: avg=0s       min=0s       med=0s      max=0s       p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=14.17s   min=904.19ms med=8.92s   max=49.89s   p(90)=33.33s   p(95)=40.38s  
     http_reqs......................: 3440   37.849238/s
     iteration_duration.............: avg=14.17s   min=905.67ms med=8.92s   max=49.9s    p(90)=33.33s   p(95)=40.38s  
     iterations.....................: 3440   37.849238/s
     vus............................: 41     min=41      max=1000
     vus_max........................: 1000   min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/74635952-3baf-45ae-c24f-15d4aa613d00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/6ce55ca3-c136-44bb-56a0-eb28138f1c00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `stitching-federation-with-yoga`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 6229 / ✗ 6
     ✗ valid response structure
      ↳  99% — ✓ 6229 / ✗ 6

     checks.........................: 99.93% ✓ 18693    ✗ 12    
     data_received..................: 31 MB  368 kB/s
     data_sent......................: 7.4 MB 87 kB/s
     http_req_blocked...............: avg=269.95µs min=1.2µs   med=2.2µs  max=84.58ms p(90)=323.75µs p(95)=405.74µs
     http_req_connecting............: avg=251.31µs min=0s      med=0s     max=84.36ms p(90)=258.2µs  p(95)=335.35µs
     http_req_duration..............: avg=7.04s    min=55.55ms med=1.91s  max=56.76s  p(90)=31.62s   p(95)=44.13s  
       { expected_response:true }...: avg=7.04s    min=55.55ms med=1.91s  max=56.76s  p(90)=31.62s   p(95)=44.13s  
     http_req_failed................: 0.00%  ✓ 0        ✗ 6235  
     http_req_receiving.............: avg=60.78µs  min=17.89µs med=43.6µs max=30.23ms p(90)=77.89µs  p(95)=86µs    
     http_req_sending...............: avg=92.98µs  min=6.8µs   med=13.2µs max=73.63ms p(90)=62.6µs   p(95)=76.2µs  
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s     max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=7.04s    min=55.49ms med=1.91s  max=56.75s  p(90)=31.62s   p(95)=44.13s  
     http_reqs......................: 6235   73.19485/s
     iteration_duration.............: avg=7.04s    min=56.23ms med=1.91s  max=56.76s  p(90)=31.62s   p(95)=44.13s  
     iterations.....................: 6235   73.19485/s
     vus............................: 3      min=3      max=1000
     vus_max........................: 1000   min=1000   max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/334fd394-eec4-49bb-6242-c7e777f77200/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/ccde1d09-3bc5-45fa-f338-9de3a7d9fa00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-gateway-with-yoga`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 5228 / ✗ 27
     ✗ valid response structure
      ↳  99% — ✓ 5228 / ✗ 27

     checks.........................: 99.65% ✓ 15711     ✗ 54    
     data_received..................: 26 MB  310 kB/s
     data_sent......................: 6.2 MB 73 kB/s
     http_req_blocked...............: avg=241.72µs min=1.1µs   med=2.8µs   max=28.49ms p(90)=366.85µs p(95)=420.22µs
     http_req_connecting............: avg=224.44µs min=0s      med=0s      max=28.28ms p(90)=303.19µs p(95)=348.95µs
     http_req_duration..............: avg=8.47s    min=88.1ms  med=2.4s    max=57.16s  p(90)=36.5s    p(95)=47.06s  
       { expected_response:true }...: avg=8.47s    min=88.1ms  med=2.4s    max=57.16s  p(90)=36.5s    p(95)=47.06s  
     http_req_failed................: 0.00%  ✓ 0         ✗ 5255  
     http_req_receiving.............: avg=65.82µs  min=19.3µs  med=60.39µs max=11.1ms  p(90)=87.8µs   p(95)=96.22µs 
     http_req_sending...............: avg=62.36µs  min=7.6µs   med=16.7µs  max=19.18ms p(90)=65.85µs  p(95)=80.03µs 
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s      max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=8.47s    min=88.01ms med=2.4s    max=57.16s  p(90)=36.5s    p(95)=47.06s  
     http_reqs......................: 5255   61.673652/s
     iteration_duration.............: avg=8.47s    min=88.73ms med=2.4s    max=57.16s  p(90)=36.5s    p(95)=47.06s  
     iterations.....................: 5255   61.673652/s
     vus............................: 4      min=4       max=1000
     vus_max........................: 1000   min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/21a5a8e1-b7ad-418f-4f2e-616b1a878800/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/0e32b5ca-d86a-48fa-1b39-32a147440100/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-server`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✗ no graphql errors
      ↳  99% — ✓ 4805 / ✗ 48
     ✗ valid response structure
      ↳  99% — ✓ 4805 / ✗ 48

     checks.........................: 99.34% ✓ 14463     ✗ 96    
     data_received..................: 25 MB  295 kB/s
     data_sent......................: 5.8 MB 68 kB/s
     http_req_blocked...............: avg=528.02µs min=1.4µs   med=2.7µs  max=49.09ms p(90)=387.02µs p(95)=446.62µs
     http_req_connecting............: avg=510.44µs min=0s      med=0s     max=48.37ms p(90)=316.78µs p(95)=375.04µs
     http_req_duration..............: avg=9.29s    min=96.92ms med=2.64s  max=57.85s  p(90)=38.57s   p(95)=48.79s  
       { expected_response:true }...: avg=9.29s    min=96.92ms med=2.64s  max=57.85s  p(90)=38.57s   p(95)=48.79s  
     http_req_failed................: 0.00%  ✓ 0         ✗ 4853  
     http_req_receiving.............: avg=70.73µs  min=27.4µs  med=63.4µs max=18.55ms p(90)=90.6µs   p(95)=99.5µs  
     http_req_sending...............: avg=55.77µs  min=9.7µs   med=15.3µs max=16.37ms p(90)=71µs     p(95)=85.02µs 
     http_req_tls_handshaking.......: avg=0s       min=0s      med=0s     max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=9.29s    min=96.83ms med=2.64s  max=57.85s  p(90)=38.57s   p(95)=48.79s  
     http_reqs......................: 4853   57.395613/s
     iteration_duration.............: avg=9.29s    min=97.51ms med=2.64s  max=57.85s  p(90)=38.57s   p(95)=48.79s  
     iterations.....................: 4853   57.395613/s
     vus............................: 2      min=2       max=1000
     vus_max........................: 1000   min=1000    max=1000
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/59252e25-153d-4abb-a5d2-06dca0108000/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/4354263b-2405-4c86-9082-e53a73be7f00/public" alt="HTTP Overview" />


  </details>