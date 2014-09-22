MyBatis CDI Extension
=====================

[![Build Status](https://travis-ci.org/mybatis/cdi.svg?branch=master)](https://travis-ci.org/mybatis/cdi)
[![Maven central](https://maven-badges.herokuapp.com/maven-central/org.mybatis/mybatis-cdi/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.mybatis/mybatis-cdi)

![mybatis-cdi](http://mybatis.github.io/images/mybatis-logo.png)

MyBatis-CDI extension takes care of the lifecycle of MyBatis mappers and SqlSessions. MyBatis components are directly injected into your
CDI beans ready to be used, there is no need to create or destroy them. It also provides local and JTA transaction support based on the
@Transactional annotation.

Essentials
----------

* [See the docs](http://mybatis.github.io/cdi/)

