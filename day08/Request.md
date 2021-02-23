# Request

## Request概述

代表HTTP请求的对象。

### 1. Request继承结构

```
ServletRequest

		|-HttpServletRequest
```

### 		1. ServletRequest

​						request的根接口，定义了请求相关的方法

### 		2. httpServletRquest

​						ServletRequest接口的实现类，在ServletRequest接口的基础上增加了很多和HTTP协议相关的方法

## Request功能详解

#### 		1. 获取客户机相关信息

| [StringBuffer](http://java.sun.com/j2se/1.5/docs/api/java/lang/StringBuffer.html) | [getRequestURL](#getRequestURL())()      Reconstructs the URL the client used to make the request.获取客户端访问的完整URL |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getRequestURI](#getRequestURI())()      Returns the part of this request's URL from the protocol name up to the query string in the first line of the HTTP request.获取客户端访问的资源路径 |
| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getQueryString](#getQueryString())()      Returns the query string that is contained in the request URL after the path.获取请求地址中的参数部分作为字符串返回 |
| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getRemoteAddr](#getRemoteAddr())()      Returns the Internet Protocol (IP) address of the client or last proxy that sent the request.获取客户机ip地址信息 |
| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getMethod](#getMethod())()      Returns the name of the HTTP method with which this request was made, for example, GET, POST, or PUT.获取请求方式 |
| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getContextPath](#getContextPath())()      Returns the portion of the request URI that indicates the context of the request.获取当前访问的应用名称 |

#### 		2. 获取请求头信息

| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getHeader](#getHeader(java.lang.String))([String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) name)      Returns the value of the specified request header as a String.获取指定请求头的值 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Enumeration](http://java.sun.com/j2se/1.5/docs/api/java/util/Enumeration.html) | [getHeaders](#getHeaders(java.lang.String))([String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) name)      Returns all the values of the specified request header as an Enumeration of String objects.获取指定请求头的值们 |
| [Enumeration](http://java.sun.com/j2se/1.5/docs/api/java/util/Enumeration.html) | [getHeaderNames](#getHeaderNames())()      Returns an enumeration of all the header names this request contains.获取所有请求头的名字们 |
| int                                                          | [getIntHeader](#getIntHeader(java.lang.String))([String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) name)      Returns the value of the specified request header as an int.以int类型获取指定请求头的值 |
| long                                                         | [getDateHeader](#getDateHeader(java.lang.String))([String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) name)      Returns the value of the specified request header as a long value that represents a Date object.以时间毫秒值获取请求头的值 |

#### 		3. 获取请求参数

| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) | [getParameter](#getParameter(java.lang.String))([String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) name)      Returns the value of a request parameter as a String, or null if the parameter does not exist.获取指定名称的请求参数的值 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html)[] | [getParameterValues](#getParameterValues(java.lang.String))([String](http://java.sun.com/j2se/1.5/docs/api/java/lang/String.html) name)      Returns an array of String objects containing all of the values the given request parameter has, or null if the parameter does not exist.获取指定名称请求参数的值的集合请求中可能包含多个同名请求参数，可以通过这个方法来获取（例如获取复选框内容） |
| [Enumeration](http://java.sun.com/j2se/1.5/docs/api/java/util/Enumeration.html) | [getParameterNames](#getParameterNames())()      Returns an Enumeration of String objects containing the names of the parameters contained in this request.获取所有请求参数名们 |
| [Map](http://java.sun.com/j2se/1.5/docs/api/java/util/Map.html) | [getParameterMap](#getParameterMap())()      Returns a java.util.Map of the parameters of this request.获取所有请求参数组成的Map<String,String[]>，其中键为请求参数名，值为请求参数值的数组 |

##### 					请求参数乱码原理

浏览器发送请求参数时采用的编码取决于表单页面的编码，如果没有表单页面，直接在地址栏上敲地址，则采用系统码。

服务器在解析请求参数时，解析用的编码如下：

| GET提交  | 请求参数在地址之后 | 看server.xml中连接器的配置Tomcat8默认为utf-8Tomcat7及以前的版本为iso8859-1 | ![](https://gitee.com/Cming852098505/img/raw/master/img/20210223115914.png) |
| -------- | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| POST提交 | 请求参数在实体内容 | 看request.setCharacterEncoding()默认为iso8859-1必须在任何获取请求参数操作之前设置 | ![](https://gitee.com/Cming852098505/img/raw/master/img/20210223115929.png) |

在产生请求参数乱码时，可以以上原理通过改变表单页面编码、tomcat连接器配置(GET乱码)、设置request.setCharacterEncoding(POST乱码)来解决。

#### 		4.实现请求转发

#### 		5.实现请求包含

#### 		6.作为域对象使用