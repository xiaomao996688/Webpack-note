## Concepts
At its core,webpack is a staic module bundler(module bundler模块打包器) for modern(现代的) JavaScript applications.When webpack processes(v.处理;加工;n.过程,进程) your application, it internally builds a dependency graph which maps every module your project needs and generates(生成) one or more bundles.
> Learn more about JavaScript modules and webpack modules here.
当webpack处理你的进程,它内部建立一个依赖关系图(映射到每一个模块你的项目需要和生成一个或多个bundle)
Since version 4.0.0,webpack does not require a configuration file to bundle your project. <br>
Nevertheless,it is incredibly configrable to better fit your needs.
<br>然而，他是难以配置更适合你的需求。
<br>
To get started you need to understand its Core Concepts:
- Entry
- Output
- Loaders
- Plugins
- Mode
- Browser Compatiblity
This document is intended(v.打算;计划;想要;意指adj.意欲达到;打算的;计划的;) to give a high-level overview(n.综述;概观) of these concepts,while providing links to detailed concept-specific use cases.<br>
For a better understanding of this ideas(理念) behind(在...后面的) module bundlers and how they work under the bood(n.头巾;覆盖;兜帽vt.罩上；以头巾覆盖),consult these resources;
为了一个更好的想法在模块打包和如何工作在幕后的理解,查阅这些资源：
- Manually(手动地) Bunding(打包) an Application
- Live Coding a Simple Module Bundler
在线的一个简单的模块打包器
- Detailed Explanation(解释说明) of a Simple Module Bundler
一个简单的模块打包器的详细说明。s