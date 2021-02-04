---
layout: default
title: InfluxDB Documentation
lang: en_US
pluginId: influxdb
---

# Description

Plugin to connect to InfluxDB. It allows to easily send information by simply selecting the corresponding commands in a list. This allow to externalize the history which can then be consulted via Grafana for example.

# Installation

In order to use the plugin, you must download, install and activate it like any Jeedom plugin.

# Plugin configuration

There is not specific configuration to do, the plugin might use a cron, depending devices configuration, to send measurements.

# Devices

A Jeedom device correspond to one InfluxDB connection

Each connector will connect and send data to one and only one influxDB instance, but you can have as many connectors as you need.
The plugin manages InfluxDB v1 and v2, the basic principle between the two remains the same but the way to connect changes between the two.

## InfluxDB v1

For each connector, you have to configure the IP address of InfluxDB server, a user, a password and the database name.
You have the option to enable or not https.

![InfluxDB v1](../images/influxV1.png "InfluxDB v1")

## InfluxDB v2

For v2, you must configure the URL in the form `https://server.my`, the access token, the organization and the destination bucket (see influxDB documentation)

![InfluxDB v2](../images/influxV2.png "InfluxDB v2")

> **Tip**
> influxDB has a free cloud offer for v2 that is very easy to set up for testing or even definitively if it suits you (limited to a single organization, rate and history retention), more info: <https: //www.influxdata.com/influxdb-cloud-pricing/>

## Sending mode

You can also choose how data must be sent, by default with auto-refresh. This configuration can be changed anytime without impact.

- Auto-refresh: the plugin will send all selected measurements at the selected schedule in one call, by default every minute.
This is the recommended way of working, it's the most optimal and do not add extra load on your Jeedom and at the same time it allows to have measurements every minute.
- Real time: the plugin will send measurement one by one each time there is a change of value, potentially several calls in the second for the same command (depending devices/commands). This mode might induce an important load on your installation depending your hardware and number of selected commands while most of the time an update by minute is more than enough to get useful statistics.

It is possible to have multiple connectors to the same database each configured with different mode and different commands if you want to have some commands send in real time while optimizing the load for others

## Commands selection

In the second tab all info commands of Jeedom are displayed in a table. It is possible to filter and sort each columns. You only have to select the commands that you want to send.

![Commands config](../images/commands.png "Commands config")

# Definitions

A **point** in InfluxDB represents a single data record that has 4 components: a **measurement**, **field** set, **tag** set and a **timestamp**.

Below the relation implemented by the plugin between InfluxDB concepts and Jeedom concepts:

Jeedom | InfluxDB | Description
- | - | -
Command name | Measurement | A measurement in InfluxDB is conceptually similar to a SQL table.
- | Timestamp | It's the timestamp of the data
Device name | Field(key) | A field key is similar to a column name in a SQL table.
Command value | Field(value) | It is the value of the point.

## Tags

Tags in InfluxDB are optional additional information associated to points.
Tags can be used in queries to filter result.
The following tags can be associated with each point sent, they must be selected in the device configuration page.
This list can be amended if you need more:

Tag(key) | Tag(value)
- | -
Plugin | plugin name
Object | Object/room name in Jeedom or "None"
CommandName | command name
GenericType | generic type of command

# Changelog

[See the changelog](./changelog)

# Support

If despite this documentation and after having read the topics related to the plugin on [community]({{site.forum}}/tags/plugin-{{page.pluginId}}) you do not find an answer to your question, do not hesitate to create a new topic with the tag of the plugin ([plugin-{{page.pluginId}}]({{site.forum}}/tags/plugin-{{page.pluginId}})).
