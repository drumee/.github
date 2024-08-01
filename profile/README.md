## What is Drumee
Drumee is a stand-alone collaborative system with all the main functionalities integrated into a single environment, offering same user experience than on a PC.

## Why?
- If you don't want to pay for cloud collaborative softwares
- If you don't want to store your data on the cloud
- If you want to have comprehensive control on your data
- If you want to develop a web application without writing a single line of HTML code.
- If you don't like mixing client-side code within side-side hook
- If your application needs to handle a lot of files and folder
- If need fine grain access control for your application
- If you want to create quickly a clean, safe and powerful web application
- If you want to think out of the box

## Architecture
Drumee breakdown is a set of three main components
- Identity Management (access control)
- File system Management (fine grain privilege control)
- Pure client-side rendering engine (pure JSON based)
![Drumee Rendering Engine](https://github.com/drumee/.github/blob/main/profile/images/letc.png)
## Principles
### Access control
Who are you and what do you want? Restful micro-service endpoint. Each service is assigned a required privilege (permission). The requested service shall be only executed if the user's privilege matchs the service permission requirement.
### File system Management
Unlike standard applications, Drumee doesn't rely on host file system management. In such a case, the whole host file system is directly exposed to threats that may passed through the application. MFS, for Meta File System Drumee, is an API set that makes file system handling much safer, easier, more flexible, scalable and powerful. 
![MFS principle](https://github.com/drumee/.github/blob/main/profile/images/mfs.png)
### User Interface Rendering Engine 
HTML makes user interface development easier, faster, portable, flexible and so on. But by design, HTML is a server-side language. How can we write user interface codes, which is a client-side program, with a language designed to run on a server? Well, we use frameworks that elevate some level of abstraction. But we always end up with :
* client-side codes are somehow generated/executed/processed by server, this means we have to add more server resources to do a job that may be done by the client. Furthermore, running a client code inside the server code may induce some risk of security beach.
* writing HTML code inside backend code. On my opinion, this approach ruins readability of code. A bad readability is the beginning of much ore messes. 
That's why Drumee runs its own User Interface Renderer called LETC, for Limitlessly Extensible Traversal Collection. [Discover LETC](https://drumee.com/-/#/sandbox)

## Get started
### Use Drumee as a standalone collaborative system
#### Install using Docker compose file 
[Read documentation here](https://github.com/drumee/docker-compose)
#### Install using Debian Packages 
#### Install using NPM

### Develop a Drumee plugin 
#### server-side plugin
#### client-side plugin
### Extend Drumee to create a specific application
### Drumee SDK