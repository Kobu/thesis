---
id: tech-stack
aliases: []
tags: []
---

This section follow the decision process of selecting appropriate software components of the application.

### Frontend

#### Frontend Library and Language
The technology used on frontend was primary affected by my experience with these technologies. I currently have non-trivial technologies with React, hence I have chosen to write this application frontend
in it. This decision also solidifies Typescript as the language of choise. However one must also decide which react framework to use. We will go over the most popul react framework and pick one, which seems most appropriate.

We will discuss several criteria for the framework of choice:
- Bundling and Configuration
A bundler combines multiple files, in our case TypeScript, CSS and images, into a few optimized bundles to reduce load times and simplify browser requests. 
It handles dependency management, code minification, and asset processing. This should require minimal developer input, and ideally, should be taken care of automatically
- Routing
Routing is the process of displaying different content based on the URL. In web apps, it allows users to navigate between different pages or sections without reloading the page.
- Server Side Rendering (SSR)
SSR allow the application to construct html blocks, which are then sent to the browser upon a request. Browser does not need to run any javascript and can simply display the pre-rendered html.
SSR can help improve several metrics such as LCP and CLS, which were described in the first chapter
- Static Side Generation (SSG)
Many pages on a website have content that does not change. In this case it is wise to pre-render this content on the server, and just send the finished html. This ensures small FCP and provides
snappy feel to the webpage
- Caching
Caching is the process of storing a result of a computation, and when the computation is triggered again, no additional work is required, as the result is already saved and can be served to the client
- popularity
TODO
- documentation
It is crucial for the developer to have adequate documentation to the tools their using. 



##### No framework
The modern React version 19 provides all the required tools to build fast and reliable websites. The problem wit such approach is that React by itself does not solve problems, that frontend developers
usually stumble upon such as routing or caching. These problems usually require additional libraries to handle this.
##### Create React APP (CRA)
CRA is a modern setup tool to preconfigure react frontends. The aim of CRA is to configure the project such that all the painpoints are taken care of, without installing additional dependencies into the project.
This includes bundler, development server  and also built-in testing with the Jest library. However since CRA can be tought of as a "react template" it does not support SSR and routing needs to be configured
with an additional library. Morever CRA tries to abstract many of its configurations, making it difficult to tweak it slighty, without opting out of whole configurations.
##### Next.js
Next.js is an open source React framework developed by Vercel. Its aim is to provide all-in-one developer experience. It is one of the most popular frameworks and goes hand in hand with deploying on Vercel.
Next.js takes care of SSR - by marking components with a 'use client' or 'use server' directive, the developer decide whether it is a server or client side rendered component. SSG is also taken care of as Next
automatically recognizes webpages, which do not channge over time, and hence can be marked as static and pre-rendered. With the introduction of `app router`, routing is as simple as it gets. App router allows
the developer to define routes based on file system structure. The root of the `app` folder is treated as the root url. Every subdirectory which includes `page.js` or `page.ts` is considered as routable
![app-router.png](/images/app-router.png)
source: https:/nextjs.org/docs/app/building-your-application/routing/defining-routes
in the above case routes /, /dashboard, /dashbouard/settings are present, thanks to the presence of `page.js` in corresponding directories. This helps tremendoously and enables the developer to focus on more important
aspects of a website



| Framework     | No Framework  | CRA           | Next.js   |
| ------------- | ------------- | ------------- | --------- |
| Bundling      | Manual        | Automatic     | Automatic |
| Routing       | Manual        | Manual        | Automatic |
| SSG           | Not Supported | Not Supported | Automatic |
| SSR           | Not Supported | Not Supported | Supported |
| Caching       | Manual        | Manual        | Automatic |
| Documentation | Excellent     | Excellent     | Excellent |
| Popularity    | Excellent     | Excellent     | Excellent |


With Next.js dominating the market and having easy deployemnts thanks to Vercel, it will be used as the single framework for this frontend


#### Styling
There are two important decision a developer must make when it comes to styling. Component library and CSS

#### Components
A components is usually ment as a self-contained, reusable unit of the user interface
that encapsulates some logic, performed by javascript, structure, defined by html, and style, described by CSS. Components are ment to be reusable. This means that by creating a Button 
component for example, we should be able to use this Button anywhere on our webpage.

Not reinventing the wheel is even more fundamental when it comes to frontend components. A Button is too trivial of an example, but lets imagine an Accordion. Accordion is a component
with multiple entries, which can recursively nest-in.
![accordion.gif](/images/accordion.gif)
Implementing one is not an impossible task, however it is good idea to delegate this work to specialized frontend developers. These developers usually create so-called component libraries.
These libraries are a collection of most widely used, styled or unstyled components, that every website needs, usually installed as a package dependency. Example of such components are buttons, links, select menu, dropdown menu, sliders etc.
Usage of a library is highly recommended as it saves time by preveneting the developer the reinvent the wheel, and probably do a poorer job while doing so.

##### No Component Library
Not using a component library is definitely an option. It offers higher level of control over the components, however, as described in the previous section, the cons most likely overwheigh the pros.
##### MaterialUI
A very popular component library based on Google's Material Design. It is visually consitent, while still providing ways to configure and style the components. MaterialUI is a very mature
component library with over 50 components, that can be used in development of enterprise level applications and hobby projects alike. It is installed as a package dependency and might have some 
performence consequences, as some of the components are heavy-weight.
![material-ui.png](/images/material-ui.png)
##### Shadcn/ui
Shadcn/ui is a new, quickly rising component library. Compared to other popular alternatives, it is not installed as a package dependency. Rather the developer picks which components should be installed
and the code of these components gets copied to the project. This means the developer is the owner of these components and can bend the code to their will. While this assures extremely high customizablity,
it also allows the developer to just stick with the defaults, as shadcn/ui is production ready as is. Having copied only what is desired, this has no additional performence overhead. Shadcn/ui also
offers styling with TailwindCSS trough the use of `className` props. This styling does not break the components, it only extends them.
 ![shadcn.png](/images/shadcn.png)
Shadcn offers around 40 well-made components and is slowly adding more with charts being the newest addion shadcn is the clear winner for the components library.

#### CSS
When working with CSS, a developer has two popular options. Plain CSS or TailwindCSS. Plain CSS requires the developer to write additional .css files which hold the styles. This approach 
is a bit slower and may lead to overhead when it comes to managment of css files - more often than not, developers will create new css classes instead of searching trough the exisitng ones. 
This can cause duplicity and overall chaos in the .css files. 
An example:
```css
.my-button {
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.my-button:hover {
  background-color: #2980b9;
}
```
```jsx
<button className="my-button">
    Click Me
</button>
```

The second option is to use TailwindCSS. Tailwind is a utility-first CSS framework. It allows the developer the write predefined utility classes directly on JSX components. By doing so
there is no need to keep track of additional styling files, because the style is tightly tied with the JSX components. This offers faster developer speed at the cost of a bit steeper
learning curve, as one must learn all the utility classes.
Example:
```jsx
<button className="bg-blue-500 text-white py-2 px-4 text-lg rounded-lg hover:bg-blue-700 transition-colors">
  Click Me
</button>
```
As we can see by the provided examples, Tailwind offers more consise way of styling components and is generally favoured by developers, compared to plain CSS. Since our 
component library of choise also uses Tailwind, I have decided to use it in this work.


### Backend
Choosing backend technology stack is just as important as frontend, if not more. Solid backend tech stack will enable the developer to write consise, yet expressive code for handling
API requests and communicating with a database. 

#### Database
Database is the a integral component in most web application. This fact alone makes a selection of good database crucial. I will first shortly explain differences between SQL and No-SQL database,
based on the differences pick one that fits our usecase the most, and then compare different database systems of given type.

##### SQL vs No-SQL
The choice between SQL, often refered to as a relational databases, and NoSQL largely depends on the nature of the data, the application requirements and scaling needs.
SQL stores data in structured tables with pre-defined schema. This rigidity of schemas enforces data integrity and consitency. On the other hand, No-SQL is a catch-all term for all
databases that are not SQL. This includes, but is not limited to, document, key-value and graph databases. Document databases are the most common alternative for SQL databases so I will
mainly compare those. Document databases store date in document-like format. This format can be tought of json files without any predefined schema, so called schema-less databases. This is beneficial for
projects that must deal with frequent changes to the underlying data schemas, which the schemaless approach of document databases certainly handle well.

Based on the requirements stated in previous chapters, we can safely create a pre-defined schema, and thus it is logical to continue with an SQL database. Moreover we do not any added
flexibility of document databases, rather the data consitency and integrity provided by relational databases.

In the following section I will compare the most popular SQL database systems, and pick one based on our needs.
##### SQLite
SQLite is an open source, lightweight, embedded relation database that is stored in a single file. It is ideal for mobile apps for keeping the data within device. However due to the design, it lacks
scalability and advanced features such as concurrency and multi-user access. Where it shines is the simple setup with zero configuration and small overhead. For these reeasons SQLite is 
often used in development environments.
##### Oracle DB
Oracle DB is a closed-source, enteprise-level, commercial database system. It is developer by the Oracle Corporation, which also provides good customer support. Oracle DB is full of most advanced features
that enteprise-level applications require, however for our purposes this database might be too complex with too much overhead.
##### Postgres
Postgres is an open source, advanced database which offers high reliability and excellent performance. It has a strong community behind it, developing features, fixing bugs and creating
drivers for new languages.



| Database  | Self Host | Configuration  | Flexibility | Features |
| --------- | --------- | -------------- | ----------- | -------- |
| SQLite    | Yes       | Simple to None | Small       | Basic    |
| Oracle DB | No        | Complex        | Good        | Advanced |
| Postgres  | Yes       | Simple         | Good        | Advanced |

Based on the comparisons above, we will use Postgres as our database.

#### Language and libraries
In order to achieve excellent perfomance, we will use the Rust programming language. Rust is one of the newer languages
providing  zero-cost abstractions, awesome tooling, and, most imporantly, memory safety without compromising on performance. 
This is achieved by so called borrow checker, explanation of the borrow checker is, however, out of scope of this work.

Second step would be to choose database driver. We know we will use Postgres as our database, but we need a library, driver,
to interact with the database inside our codebase. There are several options when it comes to rust. 
TODO: ORM vs QueryBuilder
We will thefore use SQLx, which is an extremely thin wrapper around our SQL queries. This achieves minimal overhead and 
no perfomance degradation.

HTTP Server
There are two popular options in rust, `Actix` and `Axum`. The differences are minimal, both provide excellent developer experience,
without compomising on perfomance. The `Axum` server is maintained by the same team that develops and maintains the
tokio asynchronous runtime. This ensures perfect harmony between the runtime and the server itself. Due to minimal differences 
beteween the server libraries, this is the only reason while we will go with `Axum`.
