---
title: Netlify CMSのEditorial Workflowを有効化する
date: 2018-08-31T06:15:44.409Z
description: >-
  Netlify CMSはデフォルトでは記事作成→即publishできるだけですが、Editorial
  Workflowを有効にすることで下書きの管理などが可能になります。
---
Netlify CMSはデフォルトでは記事作成→即publishできるだけですが、Editorial Workflowを有効にすることで、下書き→レビュー中→公開状態という3段階のワークフロー管理が利用可能になります。今の所、リポジトリとしてGitHubを使う場合しか利用できないようですが、その他のGitサービスにも対応予定とされています。

Editorial Workflowを有効にするには、Netlify CMSの設定ファイル(config.yml)に下記の記述を追加します。config.ymlは`/site/admin/config.yml`などにあるはずです。

```yaml:config.yml
publish_mode: editorial_workflow
```

また、公式のTemplateからNetlify CMSを利用開始した場合は、CMSバージョンが低くEditorial Workflowを利用できない場合があるようです。その場合は、CMSバージョンをアップデートします。方法はいくつかありますが、CDNを利用するのが手軽です。`/admin/index.html`を編集し、下記13行目のようにCDNからcms.jsを読み込むようにします。

```html:admin/index.html
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <title>Content Manager</title>
  <!-- Include the stylesheets from your site here -->
  <link rel="stylesheet" href="https://unpkg.com/netlify-cms@^1.0.0/dist/cms.css" />
  <script src="https://identity-js.netlify.com/v1/netlify-identity-widget.js"></script>
</head>
<body>
  <script src="https://unpkg.com/netlify-cms@^2.0.0/dist/cms.js"></script>
</body>
</html>
```

編集が終わったらファイルをGitHubにpushしてNetlifyにデプロイします。
デプロイ後にNetlify CMSのContent Managerを開くと、下記のようにWorkflowが利用可能となっています。

![Netlify CMSのEditorial Workflow](/img/ss-2018-08-31-15.39.45.png)
