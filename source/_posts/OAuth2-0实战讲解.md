---
title: OAuth2.0实战讲解
date: 2020-08-15 16:27:54
tags: OAuth2.0
toc: true
categories: OAuth2.0
author: 仙人球
---

OAuth 2.0 什么？

1. OAuth 2.0的核心是授权许可，更进一步说就是令牌机制。也就是说，第三方软件只有拿到了开放平台颁发的访问令牌，也就是得到了授权许可，然后才可以**代表**用户访问他们的数据。

2. 互联网中所有的受保护资源，几乎都是以Web API的形式来提供访问的，比如微信App要获取用户的头像、昵称，我们说OAuth 2.0与安全相关，是用来保护Web API的。另外，第三方软件通过OAuth 2.0取得访问权限之后，用户便把这些权限**委托**给了第三方软件，我们说OAuth 2.0是一种委托协议，也没问题。

3. 第三方软件，每次都是用访问令牌而不是用户名和密码来请求用户的数据，才大大减少了安全风险上的“攻击面”。不然，我们试想一下，每次都带着用户名和密码来访问数量众多的Web API ，是不是增加了这个“攻击面”。因此，我们说OAuth 2.0的核心，就是颁发访问令牌和使用访问令牌。

   <!-- more -->

## 授权码许可获取流程

1. 授权码许可流程有两种通信方式。一种是前端通信，因为它通过浏览器促成了授权码的交互流程，比如京东商家开放平台的授权服务生成授权码发送到浏览器，第三方软件仙人球从浏览器获取授权码。**正因为获取授权码的时候仙人球软件和授权服务并没有发生直接的联系，也叫做间接通信**。另外一种是后端通信，在仙人球软件获取到授权码之后，**在后端服务直接发起换取访问令牌的请求，也叫做直接通信**。
2. 在OAuth 2.0中，访问令牌被要求有极高的安全保密性，因此我们不能让它暴露在浏览器上面，只能通过第三方软件（比如仙人球）的后端服务来获取和使用，以最大限度地保障访问令牌的安全性。正因为访问令牌的这种安全要求特性，当需要前端通信，比如浏览器上面的流转的时候，OAuth 2.0才又提供了一个临时的凭证：授权码。**通过授权码的方式，可以让用户小明在授权服务上给仙人球权之后，还能重新回到仙人球的操作页面上**。这样，在保障安全性的情况下，提升了小明在仙人球上的体验。

从授权码许可流程中就可以看出来，它完美地将OAuth 2.0 的4个角色组织了起来，并保证了它们之间的顺畅通信。**它提出的这种结构和思想都可以被迁移到其他环境或者协议上，比如在微信小程序中使用授权码许可。**

## 权码和访问令牌的颁发流程具体流程

1. 授权服务的核心就是，**先颁发授权码code值，再颁发访问令牌access_token值**。
2. 在颁发访问令牌的**同时还会颁发刷新令牌refresh_token值，这种机制可以在无须用户参与的情况下用于生成新的访问令牌**。正如我们讲到的小明使用仙人球的例子，当访问令牌过期的时候，刷新令牌的存在可以大大提高小明使用仙人球软件的体验。
3. 授权还要有授权范围，**不能让第三方软件获得比注册时权限范围还大的授权，也不能获得超出了用户授权的权限范围，始终确保最小权限安全原则。**比如，小明只为仙人球软件授予了获取当天订单的权限，那么仙人球软件就不能访问小明店铺里面的历史订单数据。

## OAuth 2.0中使用JWT结构化令牌

OAuth 2.0 的核心是授权服务，更进一步讲是令牌，**没有令牌就没有OAuth，**令牌表示的是授权行为之后的结果。

一般情况下令牌对第三方软件来说是一个随机的字符串，是不透明的。大部分情况下，我们提及的令牌，都是一个无意义的字符串。

但是，人们“不甘于”这样的满足，于是开始探索有没有其他生成令牌的方式，也就有了JWT令牌，这样一来既不需要通过共享数据库，也不需要通过授权服务提供接口的方式来做令牌校验了。这就相当于通过JWT这种结构化的方式，我们在做令牌校验的时候多了一种选择。

1. 我们有了新的令牌生成方式的选择，这就是JWT令牌。这是一种结构化、信息化令牌，**结构化可以组织用户的授权信息，信息化就是令牌本身包含了授权信息**。
2. 虽然我们这讲的重点是JWT令牌，但是呢，不论是结构化的令牌还是非结构化的令牌，对于第三方软件来讲，它都不关心，因为**令牌在OAuth 2.0系统中对于第三方软件都是不透明的**。需要关心令牌的，是授权服务和受保护资源服务。
3. 我们需要注意JWT令牌的失效问题。我们使用了JWT令牌之后，远程的服务端上面是不存储的，因为不再有这个必要，JWT令牌本身就包含了信息。那么，如何来控制它的有效性问题呢？本讲中，我给出了两种建议，**一种是建立一个秘钥管理系统，将生成秘钥的粒度缩小到用户级别，另外一种是直接将用户密码当作密钥。**

## 快速地接入OAuth2.0

1. 对于第三方软件，比如仙人球打单软件来讲，**它的主要目的就是获取访问令牌，使用访问令牌**，这当然也是整个OAuth 2.0的目的，就是让第三方软件来做这两件事。在这个过程中需要强调的是，第三方软件在使用访问令牌的时候有三种方式，我们建议在平台和第三方软件约定好的前提下，**优先采用Post表单提交的方式**。
2. 受保护资源系统，比如仙人球软件要访问开放平台的订单数据服务，它需要注意的是权限的问题，这个权限范围主要包括，**不同的权限会有不同的操作，不同的权限也会对应不同的数据，不同的用户也会对应不同的数据**。

## 除了授权码许可类型，OAuth2.0还支持的授权流程

![](\OAuth2-0实战讲解\3ee0ceff6c543157a51aae985756454d.jpg)

1. 所有的授权许可类型中，授权码许可类型的安全性是最高的。因此，只要具备使用授权码许可类型的条件，我们一定要首先授权码许可类型。
2. 所有的授权许可类型都是为了解决现实中的实际问题，因此我们还要结合实际的生产环境，在保障安全性的前提下选择最合适的授权许可类型，比如使用客户端凭据许可类型的仙人球软件就是一个案例。

## 在移动App中使用OAuth2.0

1. 我们使用OAuth 2.0协议的目的，就是要起到安全性的作用，但有些时候，因为使用不当反而会造成更大的安全问题，比如将app_secret放入App中的最基本错误。如果放弃了app_secret，又是如何让没有Server端的App安全地使用授权码许可协议呢？针对这种情况，我和你介绍了PKCE协议。它是一种在失去app_secret保护的时候，防止授权码失窃的解决方案。
2. 我们需要思考一下，我们的App真的不需要一个Server端吗？我建议你在开发移动App的时候，尽可能地都要搭建一个Server端，因为通过后端通信来传输访问令牌比通过前端通信传输要安全得多。我也举了微信的例子，很多官方的开放平台在提供OAuth 2.0服务的时候，都会建议开发者要有一个相应的Server端。



## 使用Auth2.0时，使用不当可能会导致哪些安全漏洞

1. 互联网场景的安全攻击类型比如CSRF、XSS等，在OAuth 2.0中一样要做防范，因为OAuth 2.0本身就是应用在互联网场景中。
2. 除了常见的互联网安全攻击，OAuth 2.0也有自身的安全风险问题，比如我们讲到的授权码失窃、重定向URI被篡改。
3. 这些安全问题，本身从攻击的“技术含量”上并不高，但导致这些安全风险的因素，往往就是开发人员的安全意识不够。比如，没有意识到水平越权中的数据归属逻辑判断，需要加入到代码逻辑中。

其实，OAuth 2.0 的规范里面对这些安全问题都有对应的规避方式，但都要求我们使用的时候一定要非常严谨。比如，重定向URI的校验方式，规范里面是允许模糊校验的，但在结合实际环境的时候，我们又必须做到精确匹配校验才可以保障OAuth 2.0流转的安全性。

![](\OAuth2-0实战讲解\479c2f3945d7a8e186f91f58b89db57f.jpg)

## 利用OAuth2.0实现一个OpenIDConnect用户身份认证协议

1. **OAuth 2.0 不是一个身份认证协议**，请一定要记住这点。身份认证强调的是“谁的问题”，而OAuth2.0强调的是授权，是“可不可以”的问题。但是，我们可以在OAuth2.0的基础上，通过增加ID令牌来获取用户的唯一标识，从而就能够去实现一个身份认证协议。
2. 有些App不想非常麻烦地自己设计一套注册和登录认证流程，就会寻求统一的解决方案，然后势必会出现一个平台来收揽所有类似的认证登录场景。我们再反过来理解也是成立的。如果有个拥有海量用户的、大流量的访问平台，来**提供一套统一的登录认证服务**，让其他第三方应用来对接，不就可以解决一个用户使用同一个账号来登录众多第三方App的问题了吗？而OIDC，就是这样的登录认证场景的开放解决方案。

### OIDC是什么？

OIDC其实就是一种用户身份认证的开放标准。使用微信账号登录极客时间的场景，就是这种开放标准的实践。

说到这里，你可能要发问了：“不对呀，使用微信登录第三方App用的不是OAuth 2.0开放协议吗，怎么又扯上OIDC了呢？”

没错，用微信登录某第三方软件，确实使用的是OAuth 2.0。但OAuth2.0是一种授权协议，而不是身份认证协议。OIDC才是身份认证协议，而且是基于OAuth 2.0来执行用户身份认证的互通协议。更概括地说，OIDC就是直接基于OAuth 2.0 构建的身份认证框架协议。

换种表述方式，**OIDC=授权协议+身份认证**，是OAuth 2.0的超集。为方便理解，我们可以把OAuth 2.0理解为面粉，把OIDC理解为面包。这下，你是不是就理解它们的关系了？因此，我们说“第三方App使用微信登录用到了OAuth 2.0”没有错，说“使用到了OIDC”更没有错。

考虑到单点登录、联合登录，都遵循的是OIDC的标准流程，因此今天我们就讲讲如何利用OAuth2.0来实现一个OIDC，“高屋建瓴” 地去看问题。掌握了这一点，我们再去做单点登录、联合登录的场景，以及其他更多关于身份认证的场景，就都不再是问题了。

### OIDC 和 OAuth 2.0 的角色对应关系

说到“如何利用 OAuth 2.0 来构建 OIDC 这样的认证协议”，我们可以想到一个切入点，这个切入点就是OAuth 2.0 的四种角色。

OAuth 2.0的授权码许可流程的运转，需要资源拥有者、第三方软件、授权服务、受保护资源这4个角色间的顺畅通信、配合才能够完成。如果我们要想在OAuth 2.0的授权码许可类型的基础上，来构建 OIDC 的话，这4个角色仍然要继续发挥 “它们的价值”。那么，这4个角色又是怎么对应到OIDC中的参与方的呢？

那么，我们就先想想一个关于身份认证的协议框架，应该有什么角色。你可能已经想出来了，它需要一个登录第三方软件的最终用户、一个第三方软件，以及一个认证服务来为这个用户提供身份证明的验证判断。

没错，这就是OIDC的三个主要角色了。在OIDC的官方标准框架中，这三个角色的名字是：

- EU（End User），代表最终用户。
- RP（Relying Party），代表认证服务的依赖方，就是上面我提到的第三方软件。
- OP（OpenID Provider），代表提供身份认证服务方。

EU、RP和OP这三个角色对于OIDC非常重要，我后面也会时常使用简称来描述，希望你能先记住。

现在很多App都接入了微信登录，那么微信登录就是一个大的身份认证服务（OP）。一旦我们有了微信账号，就可以登录所有接入了微信登录体系的App（RP），这就是我们常说的联合登录。

现在，我们就借助极客时间的例子，来看一下OAuth 2.0的4个角色和OIDC的3个角色之间的对应关系：

![](\OAuth2-0实战讲解\8f794280f949862af3ebdc61d69c5fe9.png)

### OIDC 和 OAuth 2.0 的关键区别

看到这张角色对应关系图，你是不是有点 “恍然大悟” 的感觉：要实现一个OIDC协议，不就是直接实现一个OAuth 2.0协议吗。没错，我在这一讲的开始也说了，OIDC就是基于OAuth 2.0来实现的一个身份认证协议框架。

我再继续给你画一张OIDC的通信流程图，你就更清楚OIDC和OAuth 2.0的关系了：

![](\OAuth2-0实战讲解\23ce63497f6734dbc6dc9c5b6399c54b.png)

可以发现，一个基于授权码流程的OIDC协议流程，跟OAuth 2.0中的授权码许可的流程几乎完全一致，唯一的区别就是多返回了一个**ID_TOKEN**，我们称之为**ID令牌**。这个令牌是身份认证的关键。所以，接下来我就着重和你讲一下这个令牌，而不再细讲OIDC的整个流程。