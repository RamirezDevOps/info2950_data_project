# Phase 1: Dataset ideas

[Original proposal PDF](<Phase 1 Document.pdf>) · [Project workspace](https://github.com/RamirezDevOps/info2950_data_project)

The original proposal considered the following three sources for comparing election prediction markets, polling, and eventual outcomes. The PDF includes descriptions, availability, proposed collection methods, and trustworthiness discussions.

| Dataset idea | Proposed use | Sources and collection plan |
| --- | --- | --- |
| Kalshi election prediction markets | Track candidate market prices and implied probabilities over time, using the 2026 Texas Senate race as an example | [Example market](https://kalshi.com/markets/senatetx/texas-senate-race/senatetx-26?op_order_side=yes) and [historical data API documentation](https://docs.kalshi.com/getting_started/historical_data); proposed Python API collection |
| VoteHub polling | Compare election polling with prediction market forecasts | [VoteHub Polling API](https://votehub.com/polls/api/); proposed Python API collection |
| Associated Press 2026 election results | Compare forecasts with eventual election outcomes | [AP election results](https://apnews.com/projects/elections-2026/); proposed webpage collection after results are published |

These are the original proposal’s plans. Phase 2 uses Gallup and Brookings data for a different research topic.

## Questions for reviewers

From the original proposal:

1. Given that prediction markets often have an erratic profile (jolting upward and downward rapidly), is there a particular type of regression/mode of analysis that you recommend that we use to compare it with polling data?
2. Our Votehub dataset provides information on House and Senate races. Would analyzing polling trends across both U.S. Senate and House races add some useful variation to our project, or would analyzing both be too redundant?
3. The midterm general election data is relatively simple, but it will only be accessible on Nov. 3 after the midterm elections are decided. Are there any drawbacks or pitfalls that we must be aware of when dealing with data that only is accessible at a later date?
