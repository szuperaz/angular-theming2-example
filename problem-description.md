`stream-chat-angular` has two [Angular library dependencies](https://github.com/GetStream/stream-chat-angular/blob/master/projects/stream-chat-angular/package.json#L17):

- [ngx-popperjs](https://www.npmjs.com/package/ngx-popperjs)
- [angular-mentions](https://www.npmjs.com/package/angular-mentions)

If we create a StackBlitz project with `stream-chat-angular` we get the following build errors:

- `Cannot resolve type entity i4.MentionModule to symbol`
- `Cannot resolve type entity i24.NgxPopperjsModule to symbol`

These errors go away if we install `angular-mentions` and `ngx-popperjs` into our project -> but we shouldn’t need to install those manually in the first place, my guess based on the error is that some kind of Angular/ngcc complication didn't happen correctly after installing `stream-chat-angular`

Now the application compiles but we have runtime errors:

```
preview-d88182ac6931a.js:2 ERROR Error: inject() must be called from an injection context
    at injectInjectorOnly (core.umd.js? [sm]:5072:1)
    at ɵɵinject (core.umd.js? [sm]:5083:1)
    at Object.ɵɵdirectiveInject (core.umd.js? [sm]:15293:1)
    at NodeInjectorFactory.NgxPopperjsDirective_Factory [as factory] (ngx-popperjs.umd.js? [sm]:974:1)
    at getNodeInjectable (di.ts:634:36)
    at instantiateAllDirectives (shared.ts:1256:22)
    at createDirectivesInstances (shared.ts:583:7)
    at ɵɵelementStart (element.ts:151:3)
    at MessageComponent_ng_container_2_ng_container_1_div_4_Template (ɵcmp.js? [sm]:60:15)
    at executeTemplate (shared.ts:549:9)
```

The error is related to `NgxPopperjsDirective_Factory`, `angular-mentions` lib seems to be working fine, so the error is probably somehow related to `ngx-popperjs`.

The code works fine in a local environment.

We use Angular 12 to build `stream-chat-angular`.
