---
layout: post

title: Check the reason make your page re-render by changed props and state 
tip-number: 74
tip-username: tranvanhuyhoang 
tip-username-profile: https://github.com/tranvanhuyhoang
tip-tldr: The approach of the post is we will console.log at componentDidUpdate. Find out the reason make our component re-render (specifically is look for those states and props changed).

categories:
    - en
    - react
---

> Avoid your page re-render unnecessary is a thing very important in optimizing your app performance. 
>
> I often trace it through the way watching console.log and determine which state and props changed unnecessarily. After that, I handle that problem.

The approach of the post is we will console.log at `componentDidUpdate`. Find out the reason make our component re-render (specifically is look for those **states** and **props** changed). This post will example of both styles are **Class** and **Hook**.

## With Class

We apply this block code to `componentDidUpdate`:
``` javascript
    componentDidUpdate(prevProps, prevState) {
      Object.entries(this.props).forEach(([key, val]) =>
        prevProps[key] !== val && console.log(`Prop '${key}' changed `)
      );
      if (this.state) {
        Object.entries(this.state).forEach(([key, val]) =>
          prevState[key] !== val && console.log(`State '${key}' changed `)
        );
      }
    }
```

## With Hook

We apply function `useTraceUpdate` to our main function need to trace:

``` javascript
    function useTraceUpdate(props) {
        const prev = useRef(props);
        useEffect(() => {
            const changedProps = Object.entries(props).reduce((ps, [k, v]) => {
            if (prev.current[k] !== v) {
                ps[k] = [prev.current[k], v];
            }
            return ps;
            }, {});
            if (Object.keys(changedProps).length > 0) {
            console.log('Changed props:', changedProps);
            }
            prev.current = props;
        });
    }

    // Usage
    function MyComponent(props) {
        useTraceUpdate(props);
        return <div>{props.children}</div>;
    }
```

## Conclusion

That is a way that can help us trace the reason why our component re-render unnecessarily. After look for the reason, we can solve it and improve the performance of the application.
