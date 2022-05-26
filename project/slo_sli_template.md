# API Service

| Category     | SLI                                                                                    | SLO                                                                                                         |
|--------------|----------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Availability | Number of Successful Requests / total number of requests                               | 99%                                                                                                         |
| Latency      | Bucket of requests in a histogram showing the 95th percentile over the last 60 seconds | 90% of requests below 100ms                                                                                 |
| Error Budget | Successful requests / Total Request                                                    | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | Total Number of requests per second                                                    | 5 RPS indicates the application is functioning                                                              |
