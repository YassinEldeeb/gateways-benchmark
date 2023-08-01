## Overview for: `scenarios/fed-v1-constants-vus-subgraphs-delay`


This scenario runs 4 subgraphs and a GraphQL gateway with Federation v1 spec, and runs a heavy query. All subgraphs have an intentional delay on replying, and this creates additional pressure on the gateway's memory. We are running a heavy load of concurrent VUs to measure response time and other stats, during stress. It measure things like memory usage, CPU usage, response times.


This scenario was running 100 VUs over 60s


### Comparison


| Gateway         | RPS ⬇️ |       Requests       |          Duration          |
| :-------------- | :----: | :------------------: | :------------------------: |
| mesh-supergraph |   57   | 3530 total, 0 failed |  avg: 1717ms, p95: 2395ms  |
| apollo-router   |   52   | 3230 total, 0 failed |  avg: 1882ms, p95: 2146ms  |
| apollo-server   |   50   | 3100 total, 0 failed |  avg: 1954ms, p95: 2536ms  |
| mesh            |   49   | 3044 total, 0 failed |  avg: 1993ms, p95: 2971ms  |
| wundergraph     |   23   | 1494 total, 0 failed |  avg: 4273ms, p95: 4455ms  |
| mercurius       |   4    | 300 total, 0 failed  | avg: 22951ms, p95: 26675ms |



<details>
  <summary>Summary for: `mesh-supergraph`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✗ valid response structure
      ↳  0% — ✓ 0 / ✗ 3530

     checks.........................: 66.66% ✓ 7060      ✗ 3530 
     data_received..................: 18 MB  289 kB/s
     data_sent......................: 4.2 MB 68 kB/s
     http_req_blocked...............: avg=235.98µs min=1.7µs  med=2.8µs   max=31.83ms p(90)=4.5µs   p(95)=20.3µs 
     http_req_connecting............: avg=216.32µs min=0s     med=0s      max=23.41ms p(90)=0s      p(95)=0s     
     http_req_duration..............: avg=1.71s    min=1.41s  med=1.6s    max=3.61s   p(90)=2.09s   p(95)=2.39s  
       { expected_response:true }...: avg=1.71s    min=1.41s  med=1.6s    max=3.61s   p(90)=2.09s   p(95)=2.39s  
   ✓ http_req_failed................: 0.00%  ✓ 0         ✗ 3530 
     http_req_receiving.............: avg=74.9µs   min=26.4µs med=66.95µs max=3.87ms  p(90)=102.8µs p(95)=118µs  
     http_req_sending...............: avg=59.46µs  min=11.3µs med=17.2µs  max=16.72ms p(90)=41.71µs p(95)=56.41µs
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s      max=0s      p(90)=0s      p(95)=0s     
     http_req_waiting...............: avg=1.71s    min=1.41s  med=1.6s    max=3.61s   p(90)=2.09s   p(95)=2.39s  
     http_reqs......................: 3530   57.478779/s
     iteration_duration.............: avg=1.71s    min=1.41s  med=1.6s    max=3.61s   p(90)=2.09s   p(95)=2.39s  
     iterations.....................: 3530   57.478779/s
     vus............................: 27     min=27      max=100
     vus_max........................: 100    min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/9f842740-a7ae-4be9-b487-3d2a8720a000/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/2f5c1bd9-8bc7-4b38-4800-02e79b751000/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-router`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 9690      ✗ 0    
     data_received..................: 16 MB   261 kB/s
     data_sent......................: 3.8 MB  62 kB/s
     http_req_blocked...............: avg=265.32µs min=1.6µs  med=3.1µs  max=18.4ms  p(90)=5µs      p(95)=21.88µs 
     http_req_connecting............: avg=253.95µs min=0s     med=0s     max=18.23ms p(90)=0s       p(95)=0s      
     http_req_duration..............: avg=1.88s    min=1.75s  med=1.8s   max=3.46s   p(90)=1.99s    p(95)=2.14s   
       { expected_response:true }...: avg=1.88s    min=1.75s  med=1.8s   max=3.46s   p(90)=1.99s    p(95)=2.14s   
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 3230 
     http_req_receiving.............: avg=87.82µs  min=29.1µs med=69.3µs max=24.18ms p(90)=111.91µs p(95)=132.65µs
     http_req_sending...............: avg=118.48µs min=9.9µs  med=19.2µs max=14.81ms p(90)=44.1µs   p(95)=132.03µs
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s     max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=1.88s    min=1.75s  med=1.8s   max=3.46s   p(90)=1.99s    p(95)=2.14s   
     http_reqs......................: 3230    52.302746/s
     iteration_duration.............: avg=1.88s    min=1.75s  med=1.81s  max=3.47s   p(90)=1.99s    p(95)=2.14s   
     iterations.....................: 3230    52.302746/s
     vus............................: 30      min=30      max=100
     vus_max........................: 100     min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/343c49d1-b981-4f86-73a2-ec79758a5300/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/390ea729-babb-455a-8de9-c45abe6cfd00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `apollo-server`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 9300      ✗ 0    
     data_received..................: 16 MB   261 kB/s
     data_sent......................: 3.7 MB  60 kB/s
     http_req_blocked...............: avg=118.07µs min=1.5µs  med=2.29µs max=10.53ms p(90)=3.6µs  p(95)=15.9µs 
     http_req_connecting............: avg=113.86µs min=0s     med=0s     max=10.41ms p(90)=0s     p(95)=0s     
     http_req_duration..............: avg=1.95s    min=1.75s  med=1.85s  max=3.77s   p(90)=2.15s  p(95)=2.53s  
       { expected_response:true }...: avg=1.95s    min=1.75s  med=1.85s  max=3.77s   p(90)=2.15s  p(95)=2.53s  
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 3100 
     http_req_receiving.............: avg=59.6µs   min=27.7µs med=53.5µs max=3.87ms  p(90)=74.8µs p(95)=82.4µs 
     http_req_sending...............: avg=42.88µs  min=9.9µs  med=13.7µs max=7.61ms  p(90)=28µs   p(95)=33.82µs
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s     max=0s      p(90)=0s     p(95)=0s     
     http_req_waiting...............: avg=1.95s    min=1.75s  med=1.85s  max=3.77s   p(90)=2.15s  p(95)=2.53s  
     http_reqs......................: 3100    50.720272/s
     iteration_duration.............: avg=1.95s    min=1.75s  med=1.85s  max=3.77s   p(90)=2.15s  p(95)=2.53s  
     iterations.....................: 3100    50.720272/s
     vus............................: 12      min=12      max=100
     vus_max........................: 100     min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/217c9b82-2687-4cd5-aaba-3ae3b8b23700/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/a99f0388-bd0c-4bd5-eb2a-904fd58d7f00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mesh`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 9132      ✗ 0    
     data_received..................: 15 MB   248 kB/s
     data_sent......................: 3.6 MB  59 kB/s
     http_req_blocked...............: avg=404.48µs min=2.1µs  med=3.4µs   max=28.31ms p(90)=5.3µs   p(95)=24.76µs 
     http_req_connecting............: avg=387.08µs min=0s     med=0s      max=27.97ms p(90)=0s      p(95)=0s      
     http_req_duration..............: avg=1.99s    min=1.38s  med=1.86s   max=4.12s   p(90)=2.49s   p(95)=2.97s   
       { expected_response:true }...: avg=1.99s    min=1.38s  med=1.86s   max=4.12s   p(90)=2.49s   p(95)=2.97s   
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 3044 
     http_req_receiving.............: avg=93.68µs  min=26.9µs med=76.44µs max=12.48ms p(90)=116.7µs p(95)=140.88µs
     http_req_sending...............: avg=62.46µs  min=13.2µs med=21µs    max=8.6ms   p(90)=47.49µs p(95)=80.47µs 
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s      max=0s      p(90)=0s      p(95)=0s      
     http_req_waiting...............: avg=1.99s    min=1.38s  med=1.86s   max=4.12s   p(90)=2.49s   p(95)=2.97s   
     http_reqs......................: 3044    49.555638/s
     iteration_duration.............: avg=1.99s    min=1.38s  med=1.86s   max=4.13s   p(90)=2.49s   p(95)=2.97s   
     iterations.....................: 3044    49.555638/s
     vus............................: 43      min=43      max=100
     vus_max........................: 100     min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/bc473fde-b709-4637-eb3e-4f5e23836d00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/4ba19448-c452-4f6c-78e0-d8362b244a00/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `wundergraph`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 4482      ✗ 0    
     data_received..................: 7.4 MB  116 kB/s
     data_sent......................: 1.8 MB  28 kB/s
     http_req_blocked...............: avg=3.19ms   min=1.9µs  med=3µs    max=119.31ms p(90)=10.74µs  p(95)=37.18ms 
     http_req_connecting............: avg=3.1ms    min=0s     med=0s     max=89.28ms  p(90)=0s       p(95)=37.13ms 
     http_req_duration..............: avg=4.27s    min=4.08s  med=4.26s  max=4.62s    p(90)=4.35s    p(95)=4.45s   
       { expected_response:true }...: avg=4.27s    min=4.08s  med=4.26s  max=4.62s    p(90)=4.35s    p(95)=4.45s   
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 1494 
     http_req_receiving.............: avg=862.88µs min=24.2µs med=57.6µs max=121.49ms p(90)=384.21µs p(95)=672.47µs
     http_req_sending...............: avg=1.86ms   min=10.3µs med=17µs   max=131.65ms p(90)=1.34ms   p(95)=7.54ms  
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s     max=0s       p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=4.27s    min=4.08s  med=4.26s  max=4.61s    p(90)=4.35s    p(95)=4.44s   
     http_reqs......................: 1494    23.264998/s
     iteration_duration.............: avg=4.27s    min=4.1s   med=4.26s  max=4.66s    p(90)=4.36s    p(95)=4.5s    
     iterations.....................: 1494    23.264998/s
     vus............................: 94      min=94      max=100
     vus_max........................: 100     min=100     max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/648e13f1-9b82-433b-193a-35cb9c1fdf00/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/e2284fde-56c4-49e3-9259-4e8596e04900/public" alt="HTTP Overview" />


  </details>

<details>
  <summary>Summary for: `mercurius`</summary>

  **K6 Output**




```
     ✓ response code was 200
     ✓ no graphql errors
     ✓ valid response structure

     checks.........................: 100.00% ✓ 900     ✗ 0    
     data_received..................: 1.5 MB  20 kB/s
     data_sent......................: 356 kB  4.8 kB/s
     http_req_blocked...............: avg=1.99ms   min=1.9µs  med=3.7µs   max=32.15ms p(90)=6.56ms   p(95)=11.36ms 
     http_req_connecting............: avg=1.97ms   min=0s     med=0s      max=32.12ms p(90)=6.53ms   p(95)=11.33ms 
     http_req_duration..............: avg=22.95s   min=18.87s med=22.6s   max=28.94s  p(90)=26.23s   p(95)=26.67s  
       { expected_response:true }...: avg=22.95s   min=18.87s med=22.6s   max=28.94s  p(90)=26.23s   p(95)=26.67s  
   ✓ http_req_failed................: 0.00%   ✓ 0       ✗ 300  
     http_req_receiving.............: avg=94.27µs  min=28µs   med=85.85µs max=670.1µs p(90)=133.11µs p(95)=146.73µs
     http_req_sending...............: avg=103.92µs min=11.3µs med=27.74µs max=561µs   p(90)=313.85µs p(95)=389.57µs
     http_req_tls_handshaking.......: avg=0s       min=0s     med=0s      max=0s      p(90)=0s       p(95)=0s      
     http_req_waiting...............: avg=22.95s   min=18.87s med=22.6s   max=28.94s  p(90)=26.23s   p(95)=26.67s  
     http_reqs......................: 300     4.06178/s
     iteration_duration.............: avg=22.95s   min=18.87s med=22.6s   max=28.94s  p(90)=26.23s   p(95)=26.67s  
     iterations.....................: 300     4.06178/s
     vus............................: 20      min=20    max=100
     vus_max........................: 100     min=100   max=100
```


**Performance Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/7e4747fa-c44f-40ae-9e48-5dd7a5c03700/public" alt="Performance Overview" />


**HTTP Overview**


<img src="https://imagedelivery.net/KYe9TScr4TldYHA48pczVg/23fe49e3-8bfb-4c30-3c1e-0b250c27b700/public" alt="HTTP Overview" />


  </details>