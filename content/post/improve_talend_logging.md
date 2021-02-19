---
title: "Configuration Log4j2 Talend"
date: 2020-10-19T00:00:00+01:00
slug: "log4j-talend"
tags: [Talend]
categories: [TIL]
--- 

Aujourd'hui j'ai appris que l'on pouvait modifier le niveau de log d'un job Talend  
1. Configurer Log4J dans le menu *Fichier\Modifier* les propriétés du Projet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
    <Appenders>  
        <Console name="Console" target="SYSTEM_OUT">  
            <PatternLayout pattern="[%-5level] %d{HH:mm:ss} %logger{36}- %msg%n" />
        </Console>

        <RollingFile name="File"
                     fileName="${sys:log_path}/${sys:jobname}.log"
                     filePattern="${sys:log_path}/${sys:jobname}.%d{yyyy-MM-dd}.%i.log">
            <PatternLayout >
                <Pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n</Pattern>
            </PatternLayout>
            <Policies>
                <OnStartupTriggeringPolicy />
                <SizeBasedTriggeringPolicy size="10 MB" />
                <TimeBasedTriggeringPolicy interval="1"/>
            </Policies>
        </RollingFile>
    </Appenders>  
 
    <Loggers>  
        <Root level="INFO">
            <AppenderRef ref="Console" />
            <AppenderRef ref="File" />
        </Root>  
    </Loggers>  
</Configuration>
```

2. spécificier dans chaque job les paramètres avancés

![](https://res.cloudinary.com/dswia5bj3/image/upload/s--s6Upzuep--/q_auto/v1613735649/CV_Hugo_GitHub/talend_job_parameters.jpg)