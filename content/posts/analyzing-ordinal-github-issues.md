+++
title = "Efficient Issue Analysis: Harnessing the Power of GPT-4 and GPT-3.5 for Github Repository Insights (Ordinal Github Issues analysis part 1)"
date = "2023-03-18T08:38:51+01:00"
cover = ""
tags = ["ai", "gpt", "ordinal"]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

# TL;DR

This post showcases a creative approach to analyzing issues in the Ordinal Github repository by leveraging the Github API, GPT-3.5, and GPT-4. The author demonstrates how to obtain the necessary data using the Github CLI, then uses GPT-4 to generate a prompt for GPT-3.5, which is then utilized to create an overview analysis of the repository's issues.

Some key takeaways from this analysis include:

Automating the process of collecting and analyzing issues and pull requests can save time and effort.
Utilizing AI models like GPT-4 and GPT-3.5 can help generate useful insights and overviews of the issues.
There are certain limitations to this approach, such as model availability and token limits. However, overall, the method proves to be efficient and cost-effective.
The author provides links to the source code and the raw output of the analysis, along with examples of how to filter the output using jq play. This solution offers a practical way to quickly gain an understanding of a large corpus of issues in a repository, making it easier to identify and prioritize tasks.

If you are still here, follow alongs.

# Why

The [SkyLight](https://sky-light-sl.com/) collective is actively building on Ordinals, as part of our research in the creation of our artworks we like to contribute.
Hence making our baby steps towards the reference implementation in to trying to understand where it is and where it goes.
When discovering a new project, the issues are usually a great places to start leaning in, as they are a source divers information related to the project.
So we went in the [Ordinal Github repository](https://github.com/casey/ord) to understand what @casey, Ordinals developers and common folks had to say about it.

At the time of writing (2021-03-18) there is 329 issues and 46 pull requests. As [lazy](https://en.wikipedia.org/wiki/Lazy_evaluation) developers we wanted to automate the process of getting the issues and pull requests in order to analyze them. We had to make it in such a way that we could easily update the issues and re-run the analysis if needed.

## Getting the data

Using the Github CLI we fetch ~1MB worth of data related to the Ordinal repository issues in the JSON format extracting the information we while feed to our AI using the following format:

```bash
gh issue list --json number,title,body,labels,updatedAt,comments,reactionGroups -L 400 > issues.json
```

![gh issue list --json number,title,body,labels,updatedAt,comments,reactionGroups -L 400 | pv > issues.json](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090742_1308x84_scrot.png)

The command is pretty simple, we used the GitHub Command Line Interface (gh cli) to get the issues and specified the flags to get the the issue number,title, body, comments,... in JSON format. The -L flag limits the number of issues to 400 and pv(screenshot) is used to get a progress bar, the output is then redirected to a file called issues.json.

## Analyzing the data

Example issue:
```json
  {
    "body": "For the very first time, it was successful to create one inscription, now transactions are not confirmed, I suspect because of the small fee rate\r\n\r\n<img width=\"557\" alt=\"Снимок экрана 2023-03-11 в 21 30 29\" src=\"https://user-images.githubusercontent.com/53757772/224508408-186dad47-3935-4ad7-8032-5985409a87ff.png\">\r\n\r\n<img width=\"804\" alt=\"Снимок экрана 2023-03-11 в 21 35 40\" src=\"https://user-images.githubusercontent.com/53757772/224508424-16d5f897-0e83-4a04-8c32-73930e2527fe.png\">\r\n\r\nThe balance is completely debited\r\n\r\n<img width=\"563\" alt=\"Снимок экрана 2023-03-11 в 21 36 35\" src=\"https://user-images.githubusercontent.com/53757772/224508755-b202f4e0-dd2e-40cc-bea2-cdd10522bbe8.png\">\r\n\r\n<img width=\"570\" alt=\"Снимок экрана 2023-03-11 в 21 37 04\" src=\"https://user-images.githubusercontent.com/53757772/224508790-e461a21c-8f2e-4a51-962f-cf6171d4b56e.png\">\r\n\r\nhttps://mempool.space/tx/b8d7cd6ba8e2c3387d6c1dfd33ef542ed82aa36425a9a7c2f903a803aaca7015\r\n\r\n\r\n\r\n\r\n\r\nHelp me )",
    "comments": [
      {
        "id": "IC_kwDOGhOAhc5XuYTN",
        "author": {
          "login": "ysw1011"
        },
        "authorAssociation": "NONE",
        "body": "你需要设置fee：./ord --wallet tord wallet inscribe 1.html --fee-rate 6，但是你没有，所以你只能等，有一个清除本地内存池交易的bitcoin cli命令，但是我不建议你用，因为会把你钱包里数据给搞丢。所以你只能等。或者创建一个新钱包，把当前钱包余额转过去 同来产生新的UTXO",
        "createdAt": "2023-03-16T11:26:11Z",
        "includesCreatedEdit": false,
        "isMinimized": false,
        "minimizedReason": "",
        "reactionGroups": [{
          "content": "THUMBS_UP",
          "users": {
            "totalCount": 1
          }}],
        "url": "https://github.com/casey/ord/issues/1917#issuecomment-1471775949",
        "viewerDidAuthor": false
      }
    ],
    "labels": [],
    "number": 1917,
    "title": "Transactions are not confirmed",
    "updatedAt": "2023-03-16T11:26:11Z"
  },
```

This is a good issue as it showcase multiple difficulties, it containes multiple language and title is not explicit about the issue which could be a challenge for the reviewer. More defined guidelines and issues templating could help make an easier pathway for users to interacts with the project.

# AI for the rescue

After learning a lot about prompt engineering over the last months we decided to write ourself the prompt to generate the overview analysis. But after fidling with [a few prompt](https://github.com/Magicking/awesome-chatgpt) for a while we were not able to get a decent result in the JSON output formating by GPT3. Instead we used GPT4 to generate the prompt to be use by GPT3 to produce the analysis, as unfortunatly, GPT4 is not available over the API yet.

Who no better to talk to a robot than another robot?

![Only robots can understand me.](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090255_1180x1594_scrot.png)

This gives a prompt that's quite effective at generating a usable JSON outputs.
With a few logics and a simple use of the OpenAI python package.
![simple openai api call](/img/posts/analyzing-ordinal-github-issues/2023-03-18-094526_1579x209_scrot.png)

We were able to generate a nice overview of the issues.
![](/img/posts/analyzing-ordinal-github-issues/2023-03-18-080232_3650x783_scrot.png)

And even get some insights about which issues are hot topics.
![](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090208_1272x258_scrot.png)

# Conclusion

It's a simple tool to help get an overview of the issues in a repository. It helps to get in the know before diving the details but there are some limitation to this simple example:
 - The limitation encountered was the model, the only one available is GPT3 which is the legacy one.
 - The number of tokens you can feed the model, even with a larger model there is a limitation therefor a compression on the body and comments could be applied when number of token feed is close to the model limitation or some kind of chunking.
 - The prompt is far from perfect, sometimes it's does not generate a valid JSON output, but it's a good start, the basic features are present.

 Was it worth it? Yes, leaning in a project is a time consuming activity and not that much productive in terms of deliverables.
 Here it took ~6 hours to get a deliverable, the software to produce it (another deliverable) while giving us a shareable quick overview of a large corpus of various issues in the repository. And the OPEX development cost was almost zero.

![cost](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090227_857x138_scrot.png)

# Links
  - [Source code](https://github.com/Magicking/openai-issues-analysis/)
  - [Raw output of the analysis](https://github.com/Magicking/openai-issues-analysis/blob/main/classifiedIssue.json), you can use [jq play](https://jqplay.org/s/6w5H0bE1uXi) to play with filtering to explore the data or your favorite JSON editor.