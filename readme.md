react-i-router is a simple SSR compatible react routing library that doesn't rely on declarative routing.  
  
## Install  
```  
$ npm install --save react-i-router
```  
  
## Usage  
```jsx  
 <Router domain={window.location.host} currentUrl={window.location.href} routes={{ "/": () => <div> Home </div> }}/>
 ```  
  
The Router component needs a domain and currentUrl prop to parse the URL. This allows the library to work for SSR as well as client side rendering.  

The router can take an optional prefix parameter that you can use to match existing url patterns.
  
## Patterns  
  
| Pattern             	        | Matches                                                                   												  |  
|---------------------------|--------------------------------------------------------------------------------------------|  
| `/`                        	    | Matches domain url                                                       											  |  
| `/route`                      | Matches specific string                                                 										      |  
| `/route/:param`        | Matches specific string and mandatory parameter mapped to the param key   |  
| `/route/?optional`  | Matches specific string and optional parameter mapped to the optional key    |


## Methods

### Router.goto(url: string, silent: boolean, replace: boolean)
> Redirects the app to the given URL or path. If silent is set to true will not trigger rerender. If replace is set to true will replace the entry in history instead of pushing it.   

### Router.getRoute () : IRouteMatch
>  Returns the active IRouteMatch 
  ```javascript
  {     
	  url:  string,
	  currentPath:  string,
	  route:  string,
	  renderFunction:  Function,
	  params:  object,
	  queryParams:  object 
  }
 ```

### Router.set404(render404: Function)
> Sets the 404 page rendering method
```jsx
Router.set404(({ url, queryParams }) => <div>{url} not found</div>)
```

### Router.addListener(event: RouterEvent, cb: Function) / Router.removeListener(event: RouterEvent, cb: Function) 
> Adds a listener to supported events
```jsx
const log = (route) => console.log(route);
Router.addListener(RouterEvent.Update, log);
Router.removeListener(RouterEvent.Update, log);
```

## Components

### Link
```
    <Link activeClassName="is-active" href="/route">My internal link</Link>;
    <Link href="https://github.com/jeremiedubuis/react-i-router" external>My external link</Link>;
```

## Higher Order Components

### withRoute
The withRoute higher order component passes a route(IRouteMatch) prop to the wrapped component

## SSR

When rendering your App serverside you should use request parameters to populate the router's props.
