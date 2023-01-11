 # Servlet
 ## Servlet 版本

 | 规范版本    | 发布时间     | Java平台  | 主要更新                                           |
 | ----------- | ------------ | --------- | -------------------------------------------------- |
 | Servlet 4.0 | 2017 年 9 月 | Java EE 8 | 支持 HTTP/2                                        |
 | Servlet 3.1 | 2013年5月    | Java EE 7 | 非阻塞 I/O、HTTP 协议更新机制（WebSocket）         |
 | Servlet 3.0 | 2009年12月   | Java EE 6 | 可插拔、简化部署、异步 Servlet、安全、文件上传     |
 | Servlet 2.5 | 2005年9月    | Java EE 5 | Annotation支持                                     |
 | Servlet 2.4 | 2003年11月   | J2EE 1.4  | web.xml 支持 XML Scheme                            |
 | Servlet 2.3 | 2001年8月    | J2EE 1.3  | 新增 Filter、事件/监听器、Wrapper                  |
 | Servlet 2.2 | 1999年8月    | J2EE 1.2  | 作为 J2EE 的一部分， 以 .war 文件作为独立 web 应用 |


 ## Servlet 组件注册

 | 注册方式       | 传统方式                                        | 注解方式       | 编程方式                     |
 | -------------- | ----------------------------------------------- | -------------- | ---------------------------- |
 | Servlet 注册   | `web.xml` 部署`<servlet>` + `<servlet-mapping>` | `@WebServlet`  | `ServletContext#addServlet`  |
 | Filter注册     | `web.xml`部署`<filter>` + `<filter-mapping>`    | `@WebFilter`   | `ServletContext#addFilter`   |
 | *Listener 注册 | `web.xml` 部署`<listener>`                      | `@WebListener` | `ServletContext#addListener` |

 ```xml
 <?xml version="1.0" encoding="UTF-8"?
 <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
 	xmlns="http://java.sun.com/xml/ns/javaee"
 	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
 		http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
 	metadata-complete="true" version="2.5">
 	<context-param>
 		<description>
 			<!-- Spring 配置文件路径参数,该参数值将被 --
 			org.springframework.web.context.ContextLoaderListener 使用
 		</description>
 		<param-namecontextConfigLocation</param-name
 		<param-value>
 			classpath*:/META-INF/spring/spring-context.xml
 		</param-value>
 	</context-param>
 	<listener>
 		<description>
 			org.springframework.web.context.ContextLoaderListener 为可选申明Listener
 		</description>
 		<listener-class>
 			org.springframework.web.context.ContextLoaderListener
 		</listener-class>
 	</listener>
 </web-app>
 ```
 # Spring Servlet Web
 ## Servlet 生命周期
 - 初始化: `init(ServletConfig)`
 - 服务: `service(ServletRequest, ServletResponse)`
 - 销毁: `destroy()`
```mermaid
sequenceDiagram
title: MarkDown 画sequence图
HttpServlet.init()-HttpServletBean.init(): Servlet 初始化生命周期调用
HttpServletBean.init() - FrameworkServlet.initServletBean(): 将ServletConfig 参数绑定到 Servlet 字段
FrameworkServlet.initServletBean() - FrameworkServlet.initWebApplicationContext(): 初始化Servlet 关联的 WebApplicationContext
FrameworkServlet.initWebApplicationContext() - DispatcherServlet.onRefresh(): 触发 DispatcherServlet onRefresh
DispatcherServlet.onRefresh() - DispatcherServlet.initStrategies(): 初始化 DispatcherServlet 各种组件
```
 ## Filter 生命周期
 - 初始化: `init(FilterConfig)`
 - 服务: `doFilter(ServletRequest, ServletResponse, FilterChain)`
 - 销毁: `destroy()`
 ## ServletContext 生命周期
 - 初始化: `contextInitialized(ServletContextEvent)`
 - 销毁: `contextDestroyed(ServletContextEvent)`