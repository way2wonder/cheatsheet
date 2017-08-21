```java
/*
* Access to properties using the point (.). Equivalent to calling property getters.
*/
${person.father.name}
/*
* Access to properties can also be made by using brackets ([]) and writing
* the name of the property as a variable or between single quotes.
*/
${person['father']['name']}
/*
* If the object is a map, both dot and bracket syntax will be equivalent to
* executing a call on its get(...) method.
*/
${countriesByCode.ES}
${personsByName['Stephen Zucchini'].age}
/*
* Indexed access to arrays or collections is also performed with brackets,
* writing the index without quotes.
*/
${personsArray[0].name}
/*
* Methods can be called, even with arguments.
*/
${person.createCompleteName()}
${person.createCompleteNameWithSeparator('-')}
```
OGNL objects
- `#ctx` : the context object.
- `#vars`: the context variables.
- `#locale` : the context locale.
- `#request` : (only in Web Contexts) the HttpServletRequest object.
- `#response` : (only in Web Contexts) the HttpServletResponse object.
- `#session` : (only in Web Contexts) the HttpSession object.
- `#servletContext` : (only in Web Contexts) the ServletContext object.

Expression Utility Objects

- #execInfo : information about the template being processed.
- #messages : methods for obtaining externalized messages inside variables expressions, in the same way as they
- would be obtained using #{…} syntax.
- #uris : methods for escaping parts of URLs/URIs
- #conversions : methods for executing the configured conversion service (if any).
- #dates : methods for java.util.Date objects: formatting, component extraction, etc.
- #calendars : analogous to #dates , but for java.util.Calendar objects.
- #numbers : methods for formatting numeric objects.
- #strings : methods for String objects: contains, startsWith, prepending/appending, etc.
- #objects : methods for objects in general.
- #bools : methods for boolean evaluation.
- #arrays : methods for arrays.
- #lists : methods for lists.
- #sets : methods for sets.
- #maps : methods for maps.
- #aggregates : methods for creating aggregates on arrays or collections.
- #ids : methods for dealing with id attributes that might be repeated (for example, as a result of an iteration).

```html
<div th:object="${session.user}">
<p>Name: <span th:text="${#object.firstName}">Sebastian</span>.</p>
<p>Surname: <span th:text="${session.user.lastName}">Pepper</span>.</p>
<p>Nationality: <span th:text="*{nationality}">Saturn</span>.</p>
</div>
```

URLs
Absolute URLs: http://www.thymeleaf.org
Relative URLs:
    - Page-relative: user/login.html
    - Context-relative: /itemdetails?id=3 (context name in server will be added automatically)
    - Server-relative: ~/billing/processInvoice (allows calling URLs in another context (= application) in the same server.
    - Protocol-relative URLs: //code.jquery.com/jquery-2.0.3.min.js   (协议相对路径)
```html
<!-- Will produce 'http://localhost:8080/gtvg/order/details?orderId=3' (plus rewriting) -->
<a href="details.html"
th:href="@{http://localhost:8080/gtvg/order/details(orderId=${o.id})}">view</a>
<!-- Will produce '/gtvg/order/details?orderId=3' (plus rewriting) -->
<a href="details.html" th:href="@{/order/details(orderId=${o.id})}">view</a>
<!-- Will produce '/gtvg/order/3/details' (plus rewriting) -->
<a href="details.html" th:href="@{/order/{orderId}/details(orderId=${o.id})}">view</a>
```
TIPS:
 +  `@{/order/process(execId=${execId},execType='FAST')}` 多个参数用,分隔
 + `@{/order/{orderId}/details(orderId=${orderId})}`  url路径中也允许变量

可以嵌套
```html
<a th:href="@{${url}(orderId=${o.id})}">view</a>
<a th:href="@{'/details/'+${user.login}(orderId=${o.id})}">view</a>
```

**Fragments**

### Literals
#### Text literals
Text literals are just character strings specified between single quotes.  可以是任何字符,但是'需要用转义\'

#### Boolean literals
true  or  false

#### Null literal
`<div th:if="${variable.something} == null"> `

####Literal tokens
由以下组成`A-Za-z0-9_[].-` 不包括其他符号,如空白符,逗号等等

#### Appending texts
`+`
#### Literal substitutions
|....|中只允许${} #{} *{},不允许其他'...',布尔/数字,条件表达式等等
```html
<span th:text="|Welcome to our application, ${user.name}!|">
<span th:text="'Welcome to our application, ' + ${user.name} + '!'">
<span th:text="${onevar} + ' ' + |${twovar}, ${threevar}|">
```
#### Comparators and Equality

```html
<div th:if="${prodStat.count} &gt; 1">
<span th:text="'Execution mode is ' + ( (${execMode} == 'dev')? 'Development' : 'Production')></span>
```

#### Conditional operators

- If-then: (if) ? (then)
- If-then-else: (if) ? (then) : (else)
- Default: (value) ?: (defaultvalue)    默认值

```html
<tr th:class="${row.even}? (${row.first}? 'first' : 'even') : 'odd'">
...
</tr>
```

#### No operation
`_`  下划线就代表啥都不做 
