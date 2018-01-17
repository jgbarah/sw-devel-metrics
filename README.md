# Discussion on software development metrics

When talking about software development metrics, there are several different aspects to consider. Among them:

* How metrics are computed
* Which additional information is needed for drilling down
* How to visualize them

For example, when you have a basic metric such as "count of commits", usually you want:

* To be precise on how "count of commits" is defined. For example: "count of unique commits (according to commit hash, in the case of git) touching at least one file (to avoid merge commits not touching files).
* To have some additional information on each of the commits, for drilling down on the metric, usually by "bucketing" (grouping by) before applying the metric. For example, you may want to know "commits per company per month", which means having for each commmit additional parameters (date of commit, affiliation of author), then bucketing (grouping by) months and companies, then calculating the metric for each bucket, or some aggregated metric for all buckets (such as number of months with at least five companies contributing).
* To decide on how to visualize the metrics, and how to facilitate the drill down. That can be done, in the previous example, by using a stacked bar char, with each bar corresponding to a month, and each bar split according to commits by company during that month. Or it can be a double entry table, with months in the X axis, companies in the Y axis, and commits per company per month in each cell. Both could be actionable (so that, for example, you select the collection of companies to consider, or the time frame, with a filter), or not (so that for example they are generated with a "static" SQL query).

This discussion has as a final aim to define, as much formally as possible, the different elements that compose metrics and how they are calculated and acted on (filtered, etc.), so that if possible from a formal description, the specific querying for different platforms (SQL queries, Elasticsearch queries as they are interpreted in Kibana, etc.) is produced.

To begin with, we will try to pick one of those metrics (commit count seems interesting enough), and play with it both in ghData and GrimoireLab, to find out what we can learn from trying to describe and implement it in both systems.

One possible venue for presenting results could be the [OSS Summit NA in Vancouver](https://events.linuxfoundation.org/events/open-source-summit-north-america-2018/), or the [OSS Summit EU in Edinburgh](https://events.linuxfoundation.org/events/open-source-summit-europe-2018/).
