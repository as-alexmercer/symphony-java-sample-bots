# Symphony Sample Java Bots

[![Dependencies](https://www.versioneye.com/user/projects/577067cd6718940036449100/badge.svg?style=flat-square)](https://www.versioneye.com/user/projects/577067cd6718940036449100)
[![Build Status](https://travis-ci.org/symphonyoss/symphony-rss-bot.svg)](https://travis-ci.org/symphonyoss/symphony-rss-bot)
[![Validation Status](https://scan.coverity.com/projects/9269/badge.svg?flat=1)](https://scan.coverity.com/projects/symphonyoss-symphony-rss-bot)

A series of sample Java bots that use the [symphony-java-client](https://github.com/symphonyoss/symphony-java-client/) to interact with the Symphony platform.

## Hello World Bot
This bot says hello world to a given Symphony user (specified via `-Dreceiver.user.email`), then terminates.

## Echo Bot
This bot initiates a chat with a given Symphony user (specified via `-Dreceiver.user.email`), and echoes back every message in that chat.  Terminates automatically after 5 minutes.

## Stock Info Bot
This bot initiates a chat with a given Symphony user (specified via `-Dreceiver.user.email`), looks for cashtags in any messages in that chat, then responds with a message containing information on those stocks (obtained from the free [Yahoo Finance API](http://financequotes-api.com/), which is 20 minutes delayed).  Terminates automatically after 5 minutes.

## RSS Bot
This bot fetches feed items from given url (`-Drss.url`) and sends an X amount (`-Drss.limit`) of them to a given Symphony user (`-Dreceiver.user.email`); check the other parameters needed in the following example.

The java command runs and exit, there is no daemon running and waiting for incoming messages; for more complex bots, checkout the [symphony-java-client-examples](https://github.com/symphonyoss/symphony-java-client/tree/develop/symphony-client-examples)

## Example
```
export CERTS=~/certs

git clone https://github.com/symphonyoss/symphony-java-sample-bots.git
cd symphony-java-sample-bots
mvn clean package

java \
-Dkeystore.password=changeit \
-Dtruststore.password=changeit \
-Dsessionauth.url=https://foundation-api.symphony.com/sessionauth \
-Dkeyauth.url=https://foundation-api.symphony.com/keyauth \
-Dpod.url=https://foundation-api.symphony.com/pod \
-Dagent.url=https://foundation-api.symphony.com/agent \
-Drss.url=http://bit.ly/28T2riT \
-Drss.limit=10 \
-Dcerts.dir=$CERTS/ \
-Dtruststore.file=$CERTS/server.truststore \
-Dbot.user.name=bot.user1 \
-Dreceiver.user.email=user@symphony.foundation \
-Dbot.user.email=botuser1@symphony.foundation \
-jar target/symphony-java-sample-bots-1.0-SNAPSHOT-jar-with-dependencies.jar
```

## Libraries
- [Symphony Java Client](https://github.com/symphonyoss/symphony-java-client)
- [Rome](https://rometools.github.io/rome/) (a Java framework for RSS and Atom feeds)
- [Quotes API for Yahoo Finance](http://financequotes-api.com/)

## Roadmap
[ ] Separate out main() function and parameter handling from individual bot classes, and allow bot impl to be specified via command line arg - HIGH PRIORITY
[ ] Exception handling
[ ] Busy wait logic and command-based bot interaction (check symphony-java-client listeners)
