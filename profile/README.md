# What is Drumee

To the elders who still remember. To the youngs who never knew. Back to the 80-90's, there were VMS and Unix for expensive machines... and DOS for the cheapest. Can you imagine writing a program witout an Operating System? Yet, this what we are all doing now, in the 21th century, when developing a Web Application.

Drumee has been built to end this era of Wild Web Workaround. Open source with the AGPL licence, it's a kind of Operating System for Web Application development.

## The Problem: Reinventing the Wheel with Every new Project

Modern web development is fragmented and inefficient. Teams waste months:
    • Evaluating frameworks (React vs. Vue, Express vs. Django)
    • Rebuilding auth/file systems with inconsistent security
    • Handling rendering trade-offs (SSR vs. CSR performance pitfalls)
    • Setup infrastructure (SSL certificates, HTTP server configuration)
    • Setup database engine (application password, permission, security)

## The Solution: Drumee OS – A Comprehensive Web Development Environment

Drumee provides four integrated pillars that work like an OS:
1. Identity & Access Control (Built-In)
    - Automatic user-ID tagging for all requests
    - Role-based permissions enforced at micro service level
    - Etensible and flexibe rules
  
2. Secure Filesystem (Linux-Inspired)
    - Isolated volumes with POSIX-style permissions
    - Atomic API for uploads/downloads/move/delete/copy/update (no more multer hacks)
    - Prevents: Directory traversal, permission leaks
  
3. LETC Engine (JSON UI)
    - Zero HTML processing on the server-side
    - Define UIs as JSON trees (no HTML/CSS fragmentation)
    - Extend with custom widgets (e.g., "kind": "data-grid")

## The Ecosystem

Drumee Ecosystem is built upon two pilars

  - Unified SDK :
      - Prebuilt, resable and extensible widgets (drag-drop UI)
      - Namespaced styling (no CSS collisions)
      - Direct filesystem API integration
      - Micro-services API integration with customizable access rule for each
      - 
  - Blockchain Plugins Marketplace (Coming soon)
      - Developers sell/monetize Drumee plugins
      - Enterprises audit/verify code via smart contracts
      - Example: Purchase a "biometric-auth" plugin with crypto


# General Principles
## Technical Architecture
Drumee breakdown is a set of four main pilars
- Identity Management (access control)
- File system Management (fine grain privilege control)
- Pure client-side rendering engine (pure JSON based)
![Drumee Rendering Engine](https://github.com/drumee/.github/blob/main/profile/images/letc.png)

## Access control
Who are you and what do you want? Restful micro-service endpoint. Each service is assigned a required privilege (permission). The requested service shall be only executed if the user's privilege matchs the service permission requirement.

## File system Management
Unlike standard applications, Drumee doesn't rely on host file system management. In such a case, the whole host file system is directly exposed to threats that may passed through the application. MFS, for Meta File System Drumee, is an API set that makes file system handling much safer, easier, more flexible, scalable and powerful. 
![MFS principle](https://github.com/drumee/.github/blob/main/profile/images/mfs.png)

## User Interface Rendering Engine 
HTML makes user interface development easier, faster, portable, flexible and so on. But by design, HTML is a server-side language. How can we write user interface codes, which is a client-side program, with a language designed to run on a server? Well, we use frameworks that elevate some level of abstraction. But we always end up with :
* client-side codes are somehow generated/executed/processed by server, this means we have to add more server resources to do a job that may be done by the client. Furthermore, running a client code inside the server code may induce some risk of security beach.
* writing HTML code inside backend code. On my opinion, this approach ruins readability of code. A bad readability is the beginning of much ore messes. 
That's why Drumee runs its own User Interface Renderer called LETC, for Limitlessly Extensible Traversal Collection. [Discover LETC](https://drumee.com/-/#/sandbox)

# How does it work
## 1. Plug and play 
Drumee comes as a bundle (Docker image or Debian packages) with all servers required by modern Web Application (http server, database server, domain server, SSL certificate, WebSocket layer, video conferencing, etc.). With a handful of parameters, the bundle will install and automatically configure the whole infrastructure.
There no more time wasted for the same setup, the same trade-offs.

## 2. Fullstack DSK 
Drumee has been designed by security and for flexibility. It works like an Operating System. Drumee SDK provides extensibility on frontend and backend. Developers can focus on the functionalities that create value for their application.
Below example is a simple ERP designed to handle works ordered by customers over several constructions site. Obviously, permission on each action must be properly implemented. And we will see later how it is easy to do such a thing. 

### The frontend
Everything is widget, builtins widgets or custom widgets. All of then come to live within a JSON tree. 

- The first step is to numerate widgets you need in addition to the ones that already exist in Drumee SDK.

- Your widgets are mainly an assembly of already existing widgets from Drumee SDK. 

Below example is a sample of a real-life application, which is a small ERP for a small business dealing with several customers ordering several works on several construction site. Check the repository here for full implentation.

```
export {
    ...,
	search_results: import('./manager/widget/search-results'),
	site_form: import('./manager/widget/form/site'),
	site_item: import('./manager/widget/site-item'),
	window_customer_list: import('./manager/window/customer-list'),
	window_customer: import('./manager/window/customer'),
	window_finder: import('./manager/window/finder'),
	work_form: import('./manager/widget/form/work'),
	work_item: import('./manager/widget/work-item'),
	work_list: import('./manager/widget/work-list'),
    ...
};
```

#### A Frontend Widget
Let focused on the idget **work_form**. [Check full implentation here.](https://github.com/somanos/perdrix-ui/blob/main/src/manager/widget/form/work/index.js)


  **promptSite**(cmd) {
    this.loadWidget({
      kind: '**site_form**',
      source: this,
      id: `site-form-${this.mget('custId')}`,
      uiHandler: [this],
      **service**: "site-created"
    })
    this.ensurePart("entries-manual").then((p) => {
      p.el.dataset.state = 0;
    });
  }

  onDomRefresh() {
    this.feed(require('./skeleton')(this));
  }

  onUiEvent(cmd, args = {}) {
    let **service** = args.service || cmd.mget(_a.service);
    switch (**service**) {
…
          case "add-site":
            this.**promptSite**(cmd);
            break;
        }

  }

### The skeleton concept
Instead of using template with HTML/CSS elements, Drumee use pure JSON tree data to describe the User Interface. Below block is an example of Drumee Skeleton. 

To make the code more concise, readable and reusable, JSON data is generated by Drumee SDK like the ones below.

As the application UI start rendering, the JSON tree is parse to find every node containing an attribute name **kind**, which is a pointer to a widget, whether is a builtin or a custom one.

So a widget can have in its skelton, a tree of other widgets, and so on.

The function from the widget **this.feed(require('./skeleton')(this))** will load below structure into the User Interface Widget. [Check full implentation here.](https://github.com/somanos/perdrix-ui/blob/main/src/manager/widget/form/work/skeleton/index.js)

```
Skeletons.Box.Y({
    className: `${pfx}__main ${ui.fig.family}__main`,
    kids: [
      headerBox(ui, { title: "Create new work" }),
      customerHeader(ui),
      Skeletons.Box.Y({
        className: `${pfx}__container ${ui.fig.group}__container`,
        kids: [
          body,
        actionButtons(ui, [
        { content: "Add construction site", service: "add-site" },
        { content: "Create quotation", service: "create-quote" },
      ])
          dialogWrapper(ui)
        ]
      })
    ]
  });
```

### The events handler.
When a widget is declared with an attribute **service** and **uiHandler**, upon user action, it will trigger the method **onUiEvent** within the parent widget that has declared itself as the UI handler of the child widget.

Besides, the **ui.fig** options allow to create specific CSS class name related to the widget. This prevents style conflict, since the widget **kind** is unique in the application name space.

In this example, the service "**add-site**" shall load another widget (movable window) through the function **promptSite**, which has been designed to post the form to the server.

```
  createSite(cmd) {
    let args = this.getData();
    /** Check sanity… */
    
    if (insane) return;
    this.postService("perdrix.site_create", { args }).then((data) => {
      this.__content.feed(acknowledge(this, {
        message: `Le chantier a bien ete cree`,
        service: "site-created"
      }));
      this.mset(data)
    }).catch((e) => {
      this.__wrapperDialog.feed(acknowledge(this, {
        message: LOCALE.ERROR_SERVER,
        failed: 1,
        service: 'close-dialog',
      }))
    })
  }
```

### The REST API
In the above example, there is a method named **postService**. The first argument is the *micro service name*, remaining ones are data.


## The backend

Naturally, this method as been designed to make changes on the server side. Hence, it requires a write/modify permission, which shall be granted only to legitimate user.

### The access control mechanism

Implementing a service in Drumee Server does not require hard-coded routes. All developers have to do is to declare an ACL file (Access Control List) with the same name as the service module. 

In this example, the service name is **perdrix.site_create**. 

The module name of the service is the first word of the service name. *perdrix*.site_create. The second word of the service name is the method name within that module.

So, when the backend router receives the request to execute the service **perdrix.site_create**, it will look into for the ACL file. No ACL, no execution.

Once the ACL found, the router will look for the method name. No method, no execution.

Finally, the router can check the privilege of the request against the permission required to run the service. 

So the ACL file name must be **acl/perdrix.json** [Check full implementation here](https://github.com/somanos/perdrix-server/blob/main/acl/perdrix.json)

```
{
…
  "services": {
    "site_create": {
      "scope": "hub",
      "permission": {
        "src": "write"
      }
    },
    "site_list": {
      "scope": "hub",
      "permission": {
        "src": "read"
      }
    }
  },
  "modules": {
    "private": "service/index",
    "public": "service/index"
  }
}
```

Since the identity management is already handled by Drumee Kernel, the user privilege within the hub is known for each request. 

The privileges assignment policy is delegated to the Drumee Administrator/User, who decides who has which privileges on which hubs (resources container).

### The micro service API

As aleady said, Drumee backend services does not require hard-coded route because there is only one single route, which is  /-/svc/module_name.method_name?arguments-list…

The service name is made of two parts separated by a dot. The first part is the module name. The second one is the method name.

Upon receiving the request, the Drumee kernel parses the couple module/method. If the module exists, it checks the request privilege against the method permission requirement.  
It’s a bitwise operation, like the POSIX one. 

If the privilege doesn’t match the requirement, the request is rejected and the method never executed.

So far, from the frontend request **this.postService("perdrix.site_create",…)**, we reach the module named perdrix and the method site_create as below. [Check full implentation here.](https://github.com/somanos/perdrix-server/blob/main/service/index.js)


```
  async site_create() {
    let args = this.input.get('args')
    let data = await Db.await_proc('site_create', args);
    this.output.data(data);
  }
```

Yes, that simple! [Watch out the result!](https://github.com/drumee/.github/blob/main/profile/images/perdrix.png)

All you need is to get data from the **input** component (provided by Drumee Kernel) passed it to a stored procedure through a Drumee DB API **await_proc**, with the first argument being the procedure name and the remaining being arguments expected by the procedure.

Once done, send the data back to the frontend through the **output** module, also provided by Drumee Kernel.

### Database security

Developers don't have to care about setup and secure database server. Drumee Bundle comes with a already ready-to-use database installation with application user credentials already setup.

SQL injection, uh? No way!

Drumee best practice to always access database through stored procedures.
• Drumee database API parse arguments and bind them to placeholders
• By using stored procedure, arguments must be declared inside the procedure
Therefore, any ill formed variables shall end up rejected.


This is a very tiny glimpse of Drumee potential. Imagine you have to handle files management. Not just some simple images, but any type of file, with tree structure, with the same operation you can do with a normal filesystem (upload, download, rename, remove, update, delete, move, copy…) all applicable on files as well as folders, recursively by just sending postService(‘media.copy’…).



# Get started
While Drumee User Interface, the client-side, can run on any moderne Web Browser, Drumee Server supports only Linux architecture, at the present time.

## Developers corner
Head to this Wiki page: 
- (if you want to contribute to Drumee OS)[https://github.com/drumee/documentation/wiki/Developer-Corner]
- if you want to create plugins for Drumee (Instructions are being written)

[Check out all Drumee projects](https://github.com/orgs/drumee/repositories?) 

## Use only Drumee core functionalities

Beyond its Web OS features, Drumee is also a standaone collaborative system with a wide range of features integrated into a single, seamless environment. You can use it for free functionalities such as :
- Files sharing
- Live messaging
- Video conferencing
- ...
Chose one of installation mode below and enjoy!
#### Install using Docker compose file 
The easiest way to use Drumee is to follow [the installation documentation here](https://github.com/drumee/docker-compose)
#### Install using Debian Packages 
If you prefere to install on a Bare Metal Server or Virtual Machine, please [head to this manual](https://github.com/drumee/docker-compose)

