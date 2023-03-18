+++
title = "Analyzing Ordinal Github Issues Part 1"
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

When discovering a new project in order to contribure, the issues are great places to start leaning in.
So I went in the [Ordinal Github repository](https://github.com/casey/ord) to understand what @casey and other ordinals developers as well as other folks ideas and where they wanted to go.

The list of issues is a bit long at the time of writing (2021-03-18) there is 329 issues and 46 pull requests. As a [lazy](https://en.wikipedia.org/wiki/Lazy_evaluation) sleep deprived developer I wanted to automate the process of getting the issues and pull requests and then analyze them. I also wanted to do it in a way that I could easily update the data and re-run the analysis. I decided to use the Github API to get the data and then use GPT-4 and GPT-3.5 to generate an overview analysis.

## Getting the data

Using the Github CLI I was able to get the 1MB of data in a json format. I used the following command:

![gh issue list --json number,title,body,labels,updatedAt,comments,reactionGroups -L 400 | pv > issues.json](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090742_1308x84_scrot.png)

The command is pretty simple, I used the GitHub Command Line Interface (GH CLI) to get the issues and then I used the json flag to get the data in json format. I also used the -L flag to limit the number of issues to 400. I then used pv to get a progress bar and then I redirected the output to a file called issues.json.

## Analyzing the data

Example issue:
```json
  {
    "body": "For the very first time, it was successful to create one inscription, now transactions are not confirmed, I suspect because of the small fee rate\r\n\r\n<img width=\"557\" alt=\"Снимок экрана 2023-03-11 в 21 30 29\" src=\"https://user-images.githubusercontent.com/53757772/224508408-186dad47-3935-4ad7-8032-5985409a87ff.png\">\r\n\r\n<img width=\"804\" alt=\"Снимок экрана 2023-03-11 в 21 35 40\" src=\"https://user-images.githubusercontent.com/53757772/224508424-16d5f897-0e83-4a04-8c32-73930e2527fe.png\">\r\n\r\nThe balance is completely debited\r\n\r\n<img width=\"563\" alt=\"Снимок экрана 2023-03-11 в 21 36 35\" src=\"https://user-images.githubusercontent.com/53757772/224508755-b202f4e0-dd2e-40cc-bea2-cdd10522bbe8.png\">\r\n\r\n<img width=\"570\" alt=\"Снимок экрана 2023-03-11 в 21 37 04\" src=\"https://user-images.githubusercontent.com/53757772/224508790-e461a21c-8f2e-4a51-962f-cf6171d4b56e.png\">\r\n\r\nhttps://mempool.space/tx/b8d7cd6ba8e2c3387d6c1dfd33ef542ed82aa36425a9a7c2f903a803aaca7015\r\n\r\n\r\n\r\n\r\n\r\nHelp me )",
    "comments": [
      {
        "id": "IC_kwDOGhOAhc5XuYTN",
        "author": {H
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

This is what look a typical issue in global FOSS repository, where there is no strict guidelines for contributing and users can open issues for anything. The content of the issue contains also multiple languages which could be a challenge for the reviewer.

# AI for the rescue

After learning a lot about prompt engineering over the last months I decided to write myself the prompt to generate the overview analysis. After fidling with a few prompt for a while I was not able to get a decent result. I then decided to use GPT4 to generate the prompt for GPT3 analysis as unfortunatly, GPT4, is not available over the API yet.
But who no better to talk to a robot than another robot?

![Only robots can understand me.](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090255_1180x1594_scrot.png)

This gives a prompt that's quite effective at generating a usable JSON outputs.
With a few logics and a simple use of the OpenAI python package.
![simple openai api call](/img/posts/analyzing-ordinal-github-issues/2023-03-18-094526_1579x209_scrot.png)

I was able to generate a nice overview of the issues.
![](/img/posts/analyzing-ordinal-github-issues/2023-03-18-080232_3650x783_scrot.png)

And even get some insights about which issues are hot topics.
![](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090208_1272x258_scrot.png)

# Conclusion

It's a simple tool to help get an overview of the issues in a repository. It helps to get in the know before diving the details but there are some limitation to this simple example:
 - The limitation encountered was the model, the only one available is GPT3 which is the legacy one
 - The number of tokens you can feed the model, even with a larger model there is a limitation therefor a compression on the body and comments could be applied when number of token feed is close to the model limitation
 - The prompt is not perfect, sometimes it's does not generate a valid JSON output, but it's a good start.

 Was it worth it? I think so, leaning in a project is a time consuming activity and not that much productive in terms of deliverables.
 Here it took me 6 hours to get a deliverable, the software to produce it while giving me a shareable quick overview of a large corpus of various issues in the repository. And the OPEX development cost was almost zero.

![cost](/img/posts/analyzing-ordinal-github-issues/2023-03-18-090227_857x138_scrot.png)

# Links
  - [Source code](https://github.com/Magicking/openai-issues-analysis/)
  - [Raw output of the analysis](https://github.com/Magicking/openai-issues-analysis/blob/main/classifiedIssue.json), you can use [jq](https://stedolan.github.io/jq/) to filter the output, see example below.
    ```
    .[] | select(.reactionGroups != {}) | "\(.number): \(.title): Reaction: \(.reactionGroups)"```)