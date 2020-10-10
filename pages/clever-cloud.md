---
layout: default
title: Deploying to Cloud
permalink: /clever-cloud/
redirect_from:
  - /clever-cloud.html
sitemap:
    priority: 0.7
    lastmod: 2020-10-09T00:00:00-00:00
---

# Deploying to Clever Cloud

You can deploy your JHipster application to [Clever cloud](https://www.clever-cloud.com/){:target="_blank" rel="noopener"}.

[![]({{ site.url }}/images/logo/logo_clever_cloud.png)](https://www.clever-cloud.com/){:target="_blank" rel="noopener"}

## Before you start

You must install the [Clever cloud CLI](https://www.clever-cloud.com/doc/clever-tools/getting_started/){:target="_blank" rel="noopener"}.

You must also [create a Clever Cloud account](https://api.clever-cloud.com/v2/sessions/signup){:target="_blank" rel="noopener"} and log in with the CLI by running the following command:

<pre>$ clever login
Opening https://console.clever-cloud.com/cli-oauth?cli_version=2.7.1&cli_token=XXX in your browser to log you in…
Login successful as ...
</pre>


## Create your Clever Cloud application

1. If you are using maven `clever create --type maven [your application name]` or using gradle `clever create --type gradle [your application name]`

2. Add a database addon to your application `clever addon create [addon provider] [your addon name] --link [your application name]`

[see supported addons](https://www.clever-cloud.com/doc/addons/clever-cloud-addons/#available-add-ons)

3. Optionnal, setup env var `clever env set [your env var name] [value]`

4. Enable dedicated build `clever scale --build-flavor M`
[see dedicated build](https://www.clever-cloud.com/doc/admin-console/apps-management/#dedicated-build)


## Configure your jhipster application
Update `/src/main/resources/config/application-prod.yml` for using predefined clever cloud addon env var

For PostgreSQL
<pre>
 url: jdbc:postgresql://${POSTGRESQL_ADDON_HOST}:${POSTGRESQL_ADDON_PORT}/${POSTGRESQL_ADDON_DB}?useUnicode=true&characterEncoding=utf8&useSSL=false
   username: ${POSTGRESQL_ADDON_USER}
   password: ${POSTGRESQL_ADDON_PASSWORD}
   hikari:
     maximumPoolSize: 2
</pre>

Add a `clevercloud/` folder in base directory

create `clevercloud/maven.json` file
<pre>
{
  "build": {
    "type": "maven",
    "goal": "-Pprod package -DskipTests"
  },
  "deploy": {
	"jarName": "./target/jhipster-0.0.0-SNAPSHOT.jar"
  }
}
</pre>

## Deploy your application
You must commit before deploy

`git commit -m "Clever deploy`

then run :

`clever deploy`

## Changing the Java version

You can select the Java version (Java 11 by default)
```
clever env set CC_JAVA_VERSION 14
```

## More information

*   [Clever Cloud documentation](https://www.clever-cloud.com/doc/)
*   [Clever Cloud Java maven deployment](https://www.clever-cloud.com/doc/java/java-maven/)
*   [Clever Cloud Java maven deployment](https://www.clever-cloud.com/doc/java/java-gradle/)