---
layout: default
title: API
nav_order: 8
description: Documentation for developers
---

# API Documentation
{: .no_toc }

Documentation for developers is currently very sparse. Please feel free to help add to this page.

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}

---

# Adding GriefPrevention as a maven/gradle/etc. dependency

GriefPrevention will be added to maven central soon - in the meantime, there's this neat thing called [JitPack](https://jitpack.io/#GriefPrevention/GriefPrevention) that makes a public maven repo for public Github repos on the fly.
According to it, this is all you need to do to add to your pom.xml:
```xml
	<repositories>
		<repository>
		    <id>jitpack.io</id>
		    <url>https://jitpack.io</url>
		</repository>
	</repositories>
```


```xml
	<dependency>
	    <groupId>com.github.GriefPrevention</groupId>
	    <artifactId>GriefPrevention</artifactId>
	    <version>16.18.2</version>
            <scope>provided</scope>
	</dependency>
```

You can also add it to gradle/sbt/leiningen projects: https://jitpack.io/#GriefPrevention/GriefPrevention/

---
