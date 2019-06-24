# jqplay - examples of using the `jq` JSON processor

#### Before we start

##### JSON Data Types

A note about JSON data types: https://restfulapi.net/json-data-types/

##### About `jq`

https://stedolan.github.io/jq/manual

4 things you can do:
* pull data out of JSON
* filtering
* reformat data back into your own JSON structure
* reformat data into a table, with help from the `column` command

#### Getting Started

Go to the RStudio Github web page:
https://github.com/rstudio/

We see there are over 200 repos
Using the Github API `/orgs/<organization>/repos` end point
https://developer.github.com/v3/repos/#list-organization-repositories

Note:
1. Structure of the response is a long list of info about the repo
2. More data can be pulled by using their pagination
3. Interesting info can be pulled:
    * name
    * language
    * forks_count
    * stargazers_count
    * open_issues_count

```
$ curl -s -i https://api.github.com/orgs/rstudio/repos
```

#### Pull data out of JSON

https://stedolan.github.io/jq/manual/#Array/ObjectValueIterator:.[]
https://stedolan.github.io/jq/manual/#ObjectIdentifier-Index:.foo,.foo.bar

```
$ curl -s https://api.github.com/orgs/rstudio/repos | jq '.[].name'

"rstudio"
"R-Websockets"
"ace"
"pdf.js"
"markdown"
"highlight.js"
"sundown"
"shiny"
"jslider"
"shiny-server"
"shiny-incubator"
"node-unixgroups"
"node-http-proxy"
"shiny_example"
"libuv"
"httpuv"
"faye-websocket-node"
"bootstrap-daterangepicker"
"ggvis"
"reactnb"
"d3heatmap"
"shiny-testapp"
"shinyapps"
"packrat"
"shiny-examples"
"node-client-sessions"
"giza"
"rscrypt"
"rstudioapi"
"rmarkdown"
```

#### Filtering

https://stedolan.github.io/jq/manual/#select(boolean_expression)

```
$ curl -s https://api.github.com/orgs/rstudio/repos |
      jq '.[] | select(.name=="shiny")'

{
  "id": 4729944,
  "node_id": "MDEwOlJlcG9zaXRvcnk0NzI5OTQ0",
  "name": "shiny",
  "full_name": "rstudio/shiny",
  "private": false,
  "owner": {
    "login": "rstudio",
    "id": 513560,
    "node_id": "MDEyOk9yZ2FuaXphdGlvbjUxMzU2MA==",
    "avatar_url": "https://avatars1.githubusercontent.com/u/513560?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/rstudio",
    "html_url": "https://github.com/rstudio",
    "followers_url": "https://api.github.com/users/rstudio/followers",
    "following_url": "https://api.github.com/users/rstudio/following{/other_user}",
    "gists_url": "https://api.github.com/users/rstudio/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/rstudio/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/rstudio/subscriptions",
    "organizations_url": "https://api.github.com/users/rstudio/orgs",
    "repos_url": "https://api.github.com/users/rstudio/repos",
    "events_url": "https://api.github.com/users/rstudio/events{/privacy}",
    "received_events_url": "https://api.github.com/users/rstudio/received_events",
    "type": "Organization",
    "site_admin": false
  },
  "html_url": "https://github.com/rstudio/shiny",
  "description": "Easy interactive web applications with R",
  "fork": false,
  "url": "https://api.github.com/repos/rstudio/shiny",
  "forks_url": "https://api.github.com/repos/rstudio/shiny/forks",
  "keys_url": "https://api.github.com/repos/rstudio/shiny/keys{/key_id}",
  "collaborators_url": "https://api.github.com/repos/rstudio/shiny/collaborators{/collaborator}",
  "teams_url": "https://api.github.com/repos/rstudio/shiny/teams",
  "hooks_url": "https://api.github.com/repos/rstudio/shiny/hooks",
  "issue_events_url": "https://api.github.com/repos/rstudio/shiny/issues/events{/number}",
  "events_url": "https://api.github.com/repos/rstudio/shiny/events",
  "assignees_url": "https://api.github.com/repos/rstudio/shiny/assignees{/user}",
  "branches_url": "https://api.github.com/repos/rstudio/shiny/branches{/branch}",
  "tags_url": "https://api.github.com/repos/rstudio/shiny/tags",
  "blobs_url": "https://api.github.com/repos/rstudio/shiny/git/blobs{/sha}",
  "git_tags_url": "https://api.github.com/repos/rstudio/shiny/git/tags{/sha}",
  "git_refs_url": "https://api.github.com/repos/rstudio/shiny/git/refs{/sha}",
  "trees_url": "https://api.github.com/repos/rstudio/shiny/git/trees{/sha}",
  "statuses_url": "https://api.github.com/repos/rstudio/shiny/statuses/{sha}",
  "languages_url": "https://api.github.com/repos/rstudio/shiny/languages",
  "stargazers_url": "https://api.github.com/repos/rstudio/shiny/stargazers",
  "contributors_url": "https://api.github.com/repos/rstudio/shiny/contributors",
  "subscribers_url": "https://api.github.com/repos/rstudio/shiny/subscribers",
  "subscription_url": "https://api.github.com/repos/rstudio/shiny/subscription",
  "commits_url": "https://api.github.com/repos/rstudio/shiny/commits{/sha}",
  "git_commits_url": "https://api.github.com/repos/rstudio/shiny/git/commits{/sha}",
  "comments_url": "https://api.github.com/repos/rstudio/shiny/comments{/number}",
  "issue_comment_url": "https://api.github.com/repos/rstudio/shiny/issues/comments{/number}",
  "contents_url": "https://api.github.com/repos/rstudio/shiny/contents/{+path}",
  "compare_url": "https://api.github.com/repos/rstudio/shiny/compare/{base}...{head}",
  "merges_url": "https://api.github.com/repos/rstudio/shiny/merges",
  "archive_url": "https://api.github.com/repos/rstudio/shiny/{archive_format}{/ref}",
  "downloads_url": "https://api.github.com/repos/rstudio/shiny/downloads",
  "issues_url": "https://api.github.com/repos/rstudio/shiny/issues{/number}",
  "pulls_url": "https://api.github.com/repos/rstudio/shiny/pulls{/number}",
  "milestones_url": "https://api.github.com/repos/rstudio/shiny/milestones{/number}",
  "notifications_url": "https://api.github.com/repos/rstudio/shiny/notifications{?since,all,participating}",
  "labels_url": "https://api.github.com/repos/rstudio/shiny/labels{/name}",
  "releases_url": "https://api.github.com/repos/rstudio/shiny/releases{/id}",
  "deployments_url": "https://api.github.com/repos/rstudio/shiny/deployments",
  "created_at": "2012-06-20T18:45:11Z",
  "updated_at": "2019-06-24T07:40:18Z",
  "pushed_at": "2019-06-20T17:04:16Z",
  "git_url": "git://github.com/rstudio/shiny.git",
  "ssh_url": "git@github.com:rstudio/shiny.git",
  "clone_url": "https://github.com/rstudio/shiny.git",
  "svn_url": "https://github.com/rstudio/shiny",
  "homepage": "http://shiny.rstudio.com",
  "size": 28105,
  "stargazers_count": 3438,
  "watchers_count": 3438,
  "language": "R",
  "has_issues": true,
  "has_projects": true,
  "has_downloads": true,
  "has_wiki": true,
  "has_pages": true,
  "forks_count": 1501,
  "mirror_url": null,
  "archived": false,
  "disabled": false,
  "open_issues_count": 432,
  "license": {
    "key": "other",
    "name": "Other",
    "spdx_id": "NOASSERTION",
    "url": null,
    "node_id": "MDc6TGljZW5zZTA="
  },
  "forks": 1501,
  "open_issues": 432,
  "watchers": 3438,
  "default_branch": "master",
  "permissions": {
    "admin": false,
    "push": false,
    "pull": true
  }
}
```

#### Reformat data back into JSON

https://stedolan.github.io/jq/manual/#ObjectConstruction:{}

```
$ curl -s https://api.github.com/orgs/rstudio/repos |
      jq '.[] |
          select(.name=="shiny") |
          {
            "name": .name,
            "language": .language,
            "forks": .forks_count,
            "stargazers": .stargazers_count,
            "open_issues": .open_issues_count
          }'

{
  "name": "shiny",
  "language": "R",
  "forks": 1501,
  "stargazers": 3438,
  "open_issues": 433
}

```

#### Reformat data into a table

```
$ curl -s https://api.github.com/orgs/rstudio/repos |
      jq '.[] |
          {
            "name": .name,
            "language": .language,
            "forks": .forks_count,
            "stargazers": .stargazers_count,
            "open_issues": .open_issues_count
          }'

{
  "name": "rstudio",
  "language": "Java",
  "forks": 687,
  "stargazers": 2801,
  "open_issues": 1248
}
{
  "name": "R-Websockets",
  "language": "R",
  "forks": 36,
  "stargazers": 66,
  "open_issues": 5
}
{
  "name": "ace",
  "language": "JavaScript",
  "forks": 2,
  "stargazers": 2,
  "open_issues": 0
}
…
```

Reformat the data as `%` delimited output

```
$ curl -s https://api.github.com/orgs/rstudio/repos |
      jq -r '.[] |
          "\(.name)%\(.language)%\(.forks_count)%\(.stargazers_count)%\(.open_issues_count)"'

rstudio%Java%687%2801%1248
R-Websockets%R%36%66%5
ace%JavaScript%2%2%0
pdf.js%JavaScript%6%5%0
markdown%C%67%54%13
highlight.js%JavaScript%1%2%0
sundown%C%3%1%0
shiny%R%1501%3438%433
jslider%JavaScript%2%4%0
shiny-server%JavaScript%265%548%137
shiny-incubator%JavaScript%33%55%4
node-unixgroups%C++%1%0%0
node-http-proxy%JavaScript%2%0%0
shiny_example%R%37%17%1
libuv%C%2%0%0
httpuv%C%53%145%24
faye-websocket-node%JavaScript%2%1%0
bootstrap-daterangepicker%JavaScript%2%1%0
ggvis%R%180%658%190
reactnb%JavaScript%1%7%0
d3heatmap%HTML%88%212%56
shiny-testapp%R%6%7%0
shinyapps%null%116%115%52
packrat%R%75%309%219
shiny-examples%JavaScript%3016%1198%39
node-client-sessions%JavaScript%2%0%0
giza%JavaScript%5%4%6
rscrypt%C%10%19%4
rstudioapi%R%21%84%54
rmarkdown%R%659%1541%100
```

Use `column` command to print the data as a table

https://www.howtoforge.com/linux-column-command/#q-how-to-columnate-a-delimited-output

```
$ curl -s https://api.github.com/orgs/rstudio/repos |
      jq -r '.[] |
          "\(.name)%\(.language)%\(.forks_count)%\(.stargazers_count)%\(.open_issues_count)"' |
      column -t -s '%'

rstudio                    Java        687   2801  1248
R-Websockets               R           36    66    5
ace                        JavaScript  2     2     0
pdf.js                     JavaScript  6     5     0
markdown                   C           67    54    13
highlight.js               JavaScript  1     2     0
sundown                    C           3     1     0
shiny                      R           1501  3438  433
jslider                    JavaScript  2     4     0
shiny-server               JavaScript  265   548   137
shiny-incubator            JavaScript  33    55    4
node-unixgroups            C++         1     0     0
node-http-proxy            JavaScript  2     0     0
shiny_example              R           37    17    1
libuv                      C           2     0     0
httpuv                     C           53    145   24
faye-websocket-node        JavaScript  2     1     0
bootstrap-daterangepicker  JavaScript  2     1     0
ggvis                      R           180   658   190
reactnb                    JavaScript  1     7     0
d3heatmap                  HTML        88    212   56
shiny-testapp              R           6     7     0
shinyapps                  null        116   115   52
packrat                    R           75    309   219
shiny-examples             JavaScript  3016  1198  39
node-client-sessions       JavaScript  2     0     0
giza                       JavaScript  5     4     6
rscrypt                    C           10    19    4
rstudioapi                 R           21    84    54
rmarkdown                  R           659   1541  100

```

Add a title by `echo`'ing the title line first, then `cat`'ing the rest of the data

```
$ curl -s https://api.github.com/orgs/rstudio/repos |
      jq -r '.[] |
          "\(.name)%\(.language)%\(.forks_count)%\(.stargazers_count)%\(.open_issues_count)"' |
      (echo "name%language%forks%stargazers%open_issues"; cat;) |
      column -t -s '%'

name                       language    forks  stargazers  open_issues
rstudio                    Java        687    2801        1248
R-Websockets               R           36     66          5
ace                        JavaScript  2      2           0
pdf.js                     JavaScript  6      5           0
markdown                   C           67     54          13
highlight.js               JavaScript  1      2           0
sundown                    C           3      1           0
shiny                      R           1501   3438        433
jslider                    JavaScript  2      4           0
shiny-server               JavaScript  265    548         137
shiny-incubator            JavaScript  33     55          4
node-unixgroups            C++         1      0           0
node-http-proxy            JavaScript  2      0           0
shiny_example              R           37     17          1
libuv                      C           2      0           0
httpuv                     C           53     145         24
faye-websocket-node        JavaScript  2      1           0
bootstrap-daterangepicker  JavaScript  2      1           0
ggvis                      R           180    658         190
reactnb                    JavaScript  1      7           0
d3heatmap                  HTML        88     212         56
shiny-testapp              R           6      7           0
shinyapps                  null        116    115         52
packrat                    R           75     309         219
shiny-examples             JavaScript  3016   1198        39
node-client-sessions       JavaScript  2      0           0
giza                       JavaScript  5      4           6
rscrypt                    C           10     19          4
rstudioapi                 R           21     84          54
rmarkdown                  R           659    1541        100
```

[//]: #  vim: syntax=markdown

