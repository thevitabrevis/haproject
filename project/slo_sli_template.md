# API Service

| Category     | SLI                                                                                    | SLO                                                                                                         |
|--------------|----------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Availability | Number of Successful Requests / total number of requests                               | 99%                                                                                                         |
| Latency      | Latency for 5 min period 90th percentile                                               | 90% of requests below 100ms                                                                                 |
| Error Budget | Err requests / Total Requests in budget period                                         | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | Total num of requests over time                                                        | 5 RPS indicates the application is functioning                                                              |