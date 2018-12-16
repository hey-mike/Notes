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

- 3-Tier architectures

  - i.e. MVC architecture

- 4-Tier architectures
  - Tier 1: Serverce tier
  - Tier 2: Aggregation tier
  - Tier 3: Delivery tier
    - Aware of client profile (mobile, desktop, IOT, and so on), transforms data delivered by the Aggregation tier into client-specific formats. Cashed data would be fetched here, via CDN or otherwise.Selection of ads to insert into a webpage might be done here. This Tier is reponsible for optimizing data received from the Aggregation tier for an individual user. This layer can often be fully automated.
  - Tier 4: Client tier

## Website

It is better to use traditional way to create a static sites, simply use JQuery, HTML, CSS and vanalia JavaScript.

If there are more user interactions, or more UI components have to be managed, more like an application, then I will go with Angular/ React, but in general case, I will choose React, I can see React is exceptional to build widgets.

Moreover, if I want to build a large platform, for example, a PAAS business, I will choose Angular, due to sctrict type checking, it is imperative to maintain large code base.

## RAIL model

- Response: 100 ms to provide a response that acknowledges their action; otherwise, users will notice and get frustrated, and maybe retry the action, causing more problems down the line (we've all experienced this--the mad double- and triple-clicking).
- Animation: users will note a lag in animations if they are not performed at 60 fps. This will negatively affect the perceived performance (how the user feels about your app's speed).
- Idle: Once your application is done loading, it is idle (and also will be idle between actions) until a user performs an action.
- Load: Optimal load time is one second (or less). That doesn't mean your entire application loads in one second; it means the user sees content within one second. They get some sense that the current task (loading the page) is progressing in a meaningful way, rather than staring at a blank white screen. As we'll see, this is easier said than done!
