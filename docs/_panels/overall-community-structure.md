---
title: Overall Community Structure
description: overall view of a community grouping contributors by their activity.
author: Bitergia
screenshot: sigils/overall-community-structure.png
created_at: 2019-02-15
grimoirelab_version: 0.2.0
layout: panel
---

In order to analyze community structure we rely on 
[Onion model]({{ site.baseurl }}/common/onion_analysis). All panels
related to community structure are based on [the onion study included in
grimoirelab-elk project.](https://github.com/chaoss/grimoirelab-elk/blob/master/doc/studies.md#onion-study)


## Metrics

This panel shows the results of computing onion for all contributions in
a given data source.

* **Community Structure**: on the top right corner we find the evolution of
the different onion roles through time, divided by quarters. 
* **Contributions**: just below, another bar chart shows the
evolution of contributions in order to compare both to better
understand how groups evolve.
* **Authors**: on the left hand side, a table of authors shows the total
number of contributions of each one in the selected time frame together
with the number of quarters that author has been active in the community.
* **Roles**: below **Authors**, there is another table showing number of people and
contributions by role for the selected time frame.

In addition to Kibana filters and search box on top, filtering by `Data
Source` is allowed by using the top left corner widget. Notice the blue filter
on top used for showing only `Git` data. This filter can be modified by using
`Data Source` widget mentioned above.

### Use Notes
##### 1. Only one data source filter should be active at the same time

In Kibana/Kibiter, filters are combined by means of `AND` operators.
E.g. if we enable Git and GitHub filters, under the hood we get
an ElasticSearch query like:
```
data_source=git AND data_source=github
```
Thus, by selecting more than one data source filter at the same time,
we won't get any result, because data come from one data source or another,
but not several at the same time.

**`Data Source` widget automatically manages this for you**, so you just need
to select the desired data source in the drop down list and click on
`Apply changes`. **Data is meaningful only if one and only one data source** 
is selected for filtering.

### Files
To use this dashboard with your own GrimoireLab deployment you need to:
* Check [`all_onion` index][onion-schema] is available on your GrimoireLab instance
(see [how to configure grimoirelab-elk studies][elk-studies] and
[grimoirelab-sirmordred documentation][sirmordred] for details on how to deploy it).
* Import the following JSON files using [Kidash tool](https://github.com/chaoss/grimoirelab-kidash/).

| [![Index Pattern][ip-icon]][index-pattern] | | [![Dashboard][dash-icon]][dashboard] |
| :---------: | ---------- | :-------------: |
| **Index Pattern** | ----- | **Dashboard** |

<br />

#### Command line instructions
Once you have the data in place, if you need to manually upload the dashboard execute the
following commands:
```
kidash -e https://user:pass@localhost:443/data --import all_onion-index-pattern.json
kidash -e https://user:pass@localhost:443/data --import onion_overall.json
```

[onion-schema]: https://github.com/chaoss/grimoirelab-elk/blob/master/schema/onion.csv
[elk-studies]: https://github.com/chaoss/grimoirelab-elk/blob/master/doc/studies.md#running-studies-from-mordred 
[sirmordred]: https://github.com/chaoss/grimoirelab-sirmordred#sirmordred-
[dash-icon]: ../assets/images/icons/dashboard.png
[ip-icon]: ../assets/images/icons/file-ruled.png
[dashboard]: https://raw.githubusercontent.com/chaoss/grimoirelab-sigils/master/json/onion_overall.json
[index-pattern]: https://raw.githubusercontent.com/chaoss/grimoirelab-sigils/master/json/all_onion-index-pattern.json
