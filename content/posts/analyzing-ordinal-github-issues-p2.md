+++
title = "Analyzing Ordinal GitHub issues"
date = "2023-03-23T04:19:55+01:00"
cover = ""
tags = ["ordinal", "gpt", "ai"]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

This article is a working draft; I will update it as I go.

If you have yet to read the first part of this series, you can find it [here](/posts/analyzing-ordinal-github-issues/).

We built a tool to help us analyze GitHub issues. Below is the result in action or a [page](/codes/analyzing-ordinal-github-issues-p2/issues-display.html).

<iframe width="600" height="600" frameborder="0" src="/codes/analyzing-ordinal-github-issues-p2/issues-display.html" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Regarding the output:
 - Titles are not passed through GPT, and they are raw user entries. Normalizing the title is a good next step.
 - The body is more evident than the title most of the time.
 - Red boxes are issues that need to be classified correctly.

Sampling over 31 issues "user-support" (10%) and doing this classification manually, assisted by
the AI tool, we make this classification:

```yaml
documentation: 1062,1575,1675,1709,1770,1816,1845,1924
new-feature: 1322,1071,1519,1764,1333
wallet: 1071,1519
api: 1322
user-support: 1379,1623,1672,1770,1774,1796,1837,1850,1915,1930,1932
packaging: 1379
frontend: 1437
mime-content: 1468,1438
naming: 1518,1709

to-be-closed: 1709,1779,1816,1925
```

We see that the classification could be better. The model is not able to classify issues accurately. We have only ~10 out of ~30 issues classified correctly over a sample of 10% in the « user-support » label. It does help to read quickly over an issue; direct integration of this kind of tool is to be expected soon.

The prompt of the model needs to be reworked to get the model to classify issues more accurately.

Recommendations:
 - Closure of old issues of non-contributor if there is no activity up to a determined amount of time.
   - A gitbot could help with this.
 - Labelling seems to be useful, at least for filtering.
 - Issues templating with different models with an example of what to include could fast-track issue triaging in the future.