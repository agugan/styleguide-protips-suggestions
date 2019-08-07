# Pro Tips , Cheat Sheet, Call it whatever you want, if it helps you

## #4

- Always try to import relevant functions only (i.e Destructure imports) and remove unused imports. Try not to use `import * from “../some-dir”;`. As * means all the exported functions of “some-dir”will be imported there. This will increase the bundle size.

## #5

- When accessing observable in your template,do not to subscribe them in your components and reassign to a variable. Instead use async pipe which will automatically subscribe or unsubscribe them as the components gets destroy.

- If you really had to call subscribe method on the source observable, then use operators such as **take()**, **takeUntil()**, **first()**, which will automatically unsubscribe after use.

- Alternatively you can also assign the subscription to a variable and destroy in when your component/services are destroyed.

`component.ts/service.ts
    this.subscription = this.source.subscribe();

    ngOnDestroy(){
        this.subscription = undefined;
            or
        if(this.subscription) this.subscription.unsubscribe();
    }
  `

## #6

- If you have nested child components and you need to pass the data from the parent component, pass it via input property binding. If the data is observable, do not unsubscribe and send the data to child components, instead pass them as observable. DO the subscription at the last child component in hierarchy.

## #7

- **Type strictness**:  Try to use valid data types , union of data types etc in all your methods and variables. They ensure type-safety, eases your debugging and increases your code readability.

## #8

- Use ChangeDetectionStrategy.OnPush in all of your components, it will help to increase the performance in your app.

## #9

- When downgrading services, you have to explicitly provide them in your NgModule's providers array.
Downgrading treeshakeable providers(services that use `providedIn` syntax) results in injector not found error.
