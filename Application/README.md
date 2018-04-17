# Application Development Notes

## Frontend technoloy choices

`ReactJS`: React has shorter learning curve since, it can be impletemented with `FlowJS` a type checking library developed by Facebook, flux pattern is well supported by `Redux` library.

There are also some good quality third party CSS framewok, such `Antd`, `Material UI`. However since ReactJS is using virtual DOM to update the view, it will be tricky to integrate those third party libray that manunipulate DOM directly, i.e. D3.JS.

`AngularJS (2)`: Compare to ReactJS, Angular 2/4 is more powerful by implementing TypeScript, one of the benefit is to raise compile time errors. It is more enterprise ready framework, that is why it takes more time for developers to learn.

Dependency Injection.

## Backend techology choices

NodeJS

## System architecture

Microservices: modularize system services ,it seems to be the trend for system design, since it fits into DevOps team with continouse delivery.

## Website

It is better to use traditional way to create a static sites, simply use JQuery, HTML, CSS and vanalia JavaScript.

If there are more user interactions, or more UI components have to be managed, more like an application, then I will go with Angular/ React, but in general case, I will choose React, I can see React is exceptional to build widgets.

Moreover, if I want to build a large platform, for example, a PAAS business, I will choose Angular, due to sctrict type checking, it is imperative to maintain large code base.