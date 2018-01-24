# 爬取数据说明

我们爬取了2017年6月18日至8月28日期间新浪微博、知乎、微信公众号、今日头条这四大主流社交媒体平台上与“中印边境事件”相关的的数据，数据分类及条数见下表：

| 数据分类 |  数据条数  | 数据分类 |  数据条数  |
| :--: | :----: | :----: |:----: |
|  微博  | 63837  | 知乎评论 | 20033  |
| 微博评论 | 535050 | 知乎用户 | 30667  |
| 微博转发 | 322383 | 微信文章 |  557   |
| 微博用户 | 459301 | 头条文章 |  161   |
| 知乎提问 |  100   | 头条评论 | 43118  |
| 知乎回答 |  2439  | 头条回复 |  5171  |
| 知乎专栏 |   38   | 头条用户 | 39885  |

> 每一条数据都有独一无二的 id 字段，相关数据之间通过外键关联在一起，保持了数据之间的关联结构。

下面是对所有爬取数据文件的具体说明。

## 微博数据

微博用户 `weibo_user.csv`

|       字段        |         说明         |
| :-------------: | :----------------: |
|       id        |       用户 id        |
|       url       |      用户主页url       |
|      name       |        用户昵称        |
|     gender      | 用户性别，1～男，0～女，-1～未知 |
|    location     |       用户所在地        |
|   description   |        用户简介        |
| verified_reason |   认证信息，为空表示没有认证    |
|  follow_count   |        关注人数        |
| follower_count  |        粉丝数         |
|  status_count   |       发表的微博数       |



微博 `weibo_post.csv`

|       字段       |         说明         |
| :------------: | :----------------: |
|       id       |       微博 id        |
|      url       |       微博 url       |
|    content     |        微博内容        |
|      time      | 微博发布时间，用 UTC 时间戳表示 |
|     author     |   发表这篇微博的用户的 id    |
| comments_count |       微博评论数        |
| reposts_count  |        微博转发        |
|  likes_count   |       微博点赞数        |



微博评论 `weibo_comment.csv`

|     字段      |                    说明                    |
| :---------: | :--------------------------------------: |
|     id      |                  评论 id                   |
|   content   |                   评论内容                   |
|    user     |               发表评论的用户的 id                |
|    time     |            评论发表时间，用 UTC 时间戳表示            |
|    like     |                   点赞数                    |
| target_type | 评论对象的类型，一种是 "weibo_post"，表示针对原微博的评论，一种是 "weibo_comment"，表示回复某一个评论的评论 |
|  target_id  | 如果 target_type 是 "weibo_post"，则表示微博 id，如果 target_type 是 "weibo_comment"，则表示评论 id |



微博转发 `weibo_repost.csv`

|     字段      |        说明        |
| :---------: | :--------------: |
|     id      |      转发 id       |
|   content   |     转发时发表的内容     |
|    like     |       点赞数        |
|    user     |   转发微博的用户的 id    |
|    time     | 转发时间，用 UTC 时间戳表示 |
| origin_post |     原微博的 id      |



## 知乎数据



知乎用户 `zhihu_user.csv`

|       字段        |         说明         |
| :-------------: | :----------------: |
|       id        |       用户 id        |
|    url_token    |   可以唯一标识用户的一个字符串   |
|       url       |      用户主页 url      |
|      name       |        用户名         |
|     gender      | 用户性别，1～男，0～女，-1～未知 |
|    locations    |       用户所在地        |
|   educations    |       用户教育经历       |
|   employments   |       用户职业经历       |
|    headline     |       用户个性签名       |
|  answer_count   |        回答数         |
| articles_count  |        文章数         |
| question_count  |        提问数         |
|  columns_count  |        专栏数         |
|   logs_count    |      参与公共编辑次数      |
|  voteup_count   |      用户获得的赞同数      |
|  thanked_count  |     用户获得的感谢次数      |
|  follower_cont  |        粉丝数         |
| following_count |       关注的人数        |
| favorite_count  |        收藏数         |
| favorited_count |        被收藏数        |



知乎专栏 `zhihu_zhuanlan.csv`

|   字段    |         说明         |
| :-----: | :----------------: |
|   id    |       专栏 id        |
| author  |   作者的 url_token    |
|  title  |        专栏标题        |
| content |        专栏内容        |
|   url   |       专栏 url       |
|  time   | 专栏发表时间，用 UTC 时间戳表示 |
|  like   |        点赞数         |



知乎提问 `zhihu_question.csv`

|   字段    |        说明        |
| :-----: | :--------------: |
|   id    |      问题 id       |
| author  |  提问者的 url_token  |
|  title  |       问题标题       |
| content |       问题详细       |
|  time   | 提问时间，用 UTC 时间戳表示 |



知乎回答 `zhihu_answer.csv`

|     字段      |                    说明                    |
| :---------: | :--------------------------------------: |
|     id      |                  用户 id                   |
|     url     |                  回答 url                  |
|   author    |              回答者的 url_token              |
|   content   |                   回答内容                   |
|    time     |             回答时间，用 UTC 时间戳表示             |
|   upvote    |                   赞同数                    |
| target_type | 回答对象类型，"question" 表示对问题的回答，"answer" 表示对某个回答的回答 |
|  target_id  | 如果 target_type 是 "question" 则表示问题 id，如果 target_type 是 "answer" 则表示回答 id |



## 微信数据

公众号文章 `weixin_articles.csv`

|   字段    |   说明   |
| :-----: | :----: |
|   id    | 文章 id  |
| author  | 公众号名称  |
|   url   | 文章 url |
|  title  |  文章标题  |
| content |  文章内容  |
|  time   |  发表时间  |



## 头条数据



头条用户 `toutiao_users.csv`

|        字段        |  说明   |
| :--------------: | :---: |
|        id        | 用户 id |
|       name       |  用户名  |
| followers_count  |  粉丝数  |
| followings_count | 关注人数  |
|  verified_count  | 认证信息  |



头条文章 `toutiao_articles.csv`

|       字段       |  说明   |
| :------------: | :---: |
|       id       | 文章 id |
|   media_name   | 媒体名称  |
|     title      | 文章标题  |
|    content     | 文章内容  |
|    datetime    | 发表时间  |
| comments_count |  评论数  |
|   digg_count   |  点赞数  |
|   bury_count   |  踩数   |
| favorite_count |  收藏数  |



头条评论　`toutiao_comments.csv`


|     字段      |     说明     |
| :---------: | :--------: |
|     id      |   评论 id    |
| article_id  |   文章 id    |
|   user_id   | 发表评论的用户 id |
|  user_name  |  发表评论的用户名  |
|    text     |    评论内容    |
|    score    | 头条提供的影响力分数 |
| digg_count  |    点赞数     |
| bury_count  |     踩数     |
| reply_count |    回复数     |
| create_time |    评论时间    |



头条回复 `toutiao_replies.csv`

|     字段      |     说明     |
| :---------: | :--------: |
|     id      |   评论 id    |
|  reply_id   |   回复 id    |
|    text     |    回复内容    |
|    name     |  发表回复的用户名  |
|   user_id   | 发表回复的用户 id |
| digg_count  |    点赞数     |
| create_time |    回复时间    |



