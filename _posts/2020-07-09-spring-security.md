---
layout: post
title: Spring Security使用方法简单整理
date:   2020-07-09 13:41
description: Spring Security的使用方法
tags: 学习 Spring
toc: true
---

## 1. Spring Security

### 1. 配置安全策略

实现WebSecurityConfigurerAdapter类并Enable WebSecurity

### 2. 创建基础用户类型

实现UserDetails接口或其子接口，并实现getAuthorities()方法。

### 3. 编写鉴权实现类

编写AuthenticationProvider的子类，实现鉴权方法authenticate(Authentication auth)，其中参数auth为鉴权凭证[^1]，常用的凭证类型为UsernamePasswordAuthenticationToken，即为用户名密码登录token。

为实现鉴权操作，该类需要被spring托管，添加鉴权服务类即开发者自己提供的UserService。

实现supports(Class<?> authentication)，判断该方法用于多鉴权环境下区分鉴权策略，方法体为判断authentication类型。

### 4. 自定义安全策略

编写SecurityConfigurerAdapter<T, H>的子类。其中T为安全过滤链，通常情况下为DefaultSecurityFilterChain。H为安全策略类型，通常情况下为HttpSecurity。 安全策略的注入需要在总HttpSecurity中apply方法传入。

### 5. 其他句柄

- AuthenticationFailureHandler	认证失败
- LogoutHandler	登出
- WebResponseExceptionTranslator	认证异常统一处理
- AuthenticationSuccessHandler	认证成功

[^1]:	 AuthenticationToken
