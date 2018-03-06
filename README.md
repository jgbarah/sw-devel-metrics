# Discussion on software development metrics

When talking about software development metrics, there are several different aspects to consider. Among them:

* How metrics are computed
	- There is a need for an abstract description of the calculation that spans the specifics of an implementation tool
	- For each implementation, deviations from the formal definition of a metric must be noted. For example, not all source repositories or issue trackers contain the same data or structure their heirarchies the same. Making this information visible builds trust in the metrics themselves. 
	- The difference between metrics at the lowest level of measurement - commits, issues, issue comments, etc. - and metrics that are aimed at synthesizing composite insights from a combination of the lowest level metrics need to demonstrate a sort of "chain of custody". Deviations from repository to repository will compound as metrics are aggregated. Transparency in these matters is important. 
	- Metric utility is important to evaluate. There are indicators outside source code repositories that may signal the likelihood of uptake for a repository, or the nature of diversity and inclusion in the repository's encasing organization. Metrics that corresond with or follow these other measures are possibly more useful if such cases are proven or evaluated. 
* Which additional information is needed for drilling down
	- Making data that drives a particular metric transparent back to the source is essential for building trust
	- Aggregations of data are often used to produce metrics in the presentation layer. Making the aggregations provenance visible helps to build trust. 
* How to visualize them
	- Principles of visualization design include simple things in some cases. For example, showing the full length of a y-axis from zero oftentimes helps a person looking at a visualization to notice the variation is less than how it might appear if the y-axis is framed by the range of values in the data. The human centered aspects of design are important.
	- Project comparisons have value
	- Temporal comparisons have value and build user trust in their understanding of most metrics and their visualizations. 

For example, when you have a basic metric such as "count of commits", usually you want:

* To be precise on how "count of commits" is defined. For example: "count of unique commits (according to commit hash, in the case of git) touching at least one file (to avoid merge commits not touching files).
* To have some additional information on each of the commits, for drilling down on the metric, usually by "bucketing" (grouping by) before applying the metric. For example, you may want to know "commits per company per month", which means having for each commmit additional parameters (date of commit, affiliation of author), then bucketing (grouping by) months and companies, then calculating the metric for each bucket, or some aggregated metric for all buckets (such as number of months with at least five companies contributing).
* To decide on how to visualize the metrics, and how to facilitate the drill down. That can be done, in the previous example, by using a stacked bar char, with each bar corresponding to a month, and each bar split according to commits by company during that month. Or it can be a double entry table, with months in the X axis, companies in the Y axis, and commits per company per month in each cell. Both could be actionable (so that, for example, you select the collection of companies to consider, or the time frame, with a filter), or not (so that for example they are generated with a "static" SQL query).

This discussion has as a final aim to define, as much formally as possible, the different elements that compose metrics and how they are calculated and acted on (filtered, etc.), so that if possible from a formal description, the specific querying for different platforms (SQL queries, Elasticsearch queries as they are interpreted in Kibana, etc.) is produced.

To begin with, we will try to pick one of those metrics (commit count seems interesting enough), and play with it both in ghData and GrimoireLab, to find out what we can learn from trying to describe and implement it in both systems.

One possible venue for presenting results could be the [OSS Summit NA in Vancouver](https://events.linuxfoundation.org/events/open-source-summit-north-america-2018/), or the [OSS Summit EU in Edinburgh](https://events.linuxfoundation.org/events/open-source-summit-europe-2018/).
