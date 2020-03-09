# Frontend-Reference-Docs

[MDN][1] and [Javascript.info][2] links where applicable for more examples and/or in-depth explanations.

## CSS Defaults

Sometimes browsers add their own defaults, so this is an attempt to make things consistent across browsers.

```css
* {
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto,
    Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';
  margin: 0;
  padding: 0;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-kerning: auto;
}

:focus {
  outline: none;
}

::-moz-focus-inner {
  border: 0;
}

html {
  height: 100%;
  position: relative;
  -webkit-text-size-adjust: 100%;
}
```

## Making API Request

### XMLHttpRequest (supported by older browsers)

#### GET Request Example

```js
const xhr = new XMLHttpRequest();

// Make a get request to retrieve some fake JSON for testing
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts');

// If you want to send/receive credentials like cookies
xhr.withCredentials = true;
xhr.send();
xhr.onload = () => {
  console.log(xhr);
  if(xhr.status === 200){
    console.log(JSON.parse(xhr.response));
  }  else  {
    console.log('It didn\'t work D:', xhr.status, xhr.statusText)
  }
}
```

#### POST Request Example

```js 
const xhr = new XMLHttpRequest;
xhr.open('POST', 'https://example.com/login');
xhr.withCredentials = true;
xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
xhr.send(JSON.stringify({username: "Sam123", password: "secretpa$$word123"}));
xhr.onload = () => console.log(xhr.response);
```

[MDN - XMLHttpRequest :link:][3]

[Javscript.info - XMLHttpRequest :link:][4]

### Fetch

#### GET Request Example

```js
fetch('https://jsonplaceholder.typicode.com/posts')
.then(response => {
  return response.json();
})
.then(data => {
  console.log(data);
})
```

#### POST Request Example

```js
fetch('https://example.com/login', {
  method: 'POST',
  credentials: 'include',
  headers: {
    'Content-Type': 'application/json;charset=UTF-8',
  },
  body: JSON.stringify({username: "Sam123", password: "secretpa$$word123"});
})
.then(response => {
  return response.json();
})
.then(data => {
  console.log(data);
})
```
[MDN - Fetch :link:][5]

[Javascript.info - Fetch :link:][6]

#### Sending Form Data

```html
<form onsubmit="return login(event)">
  <label>
    Username:
    <input type="text" name="username">
  </label>
  <label> 
    Password: 
    <input type="text" name="password">
  </label>
</form>

<script>
  const login = async (e) => {
    e.preventDefault();
    const loginForm = document.querySelector('form');
    const formData = new FormData(loginForm);
    const response = await fetch('https://example.com/login', { method: 'POST', credentials: 'include', body: formData });
    const data = await response.json();
    console.log(data);
    return false;
  }
</script>
```

[MDN - FormData :link:][7]

[Javascript.info - FormData :link:][8]

## DOM Manipulation

### Document Fragment

If you have a lot of stuff you want to add to the DOM, I like to construct it in a DocumentFragment instead of appending it in the real DOM one by one.

```html
<div id="root"></div>

<script>
  const root = document.getElementById('root'); 
  const fragment = new DocumentFragment();
  
  Array.from(`don't-forget-to-drink-water`).forEach((v) => {
    const div = document.createElement('div');
    div.innerText = `${v}`
    fragment.appendChild(div);
  })
  
  root.appendChild(fragment);
</script>
```

[MDN - Document Fragment :link:][9]

[1]: https://developer.mozilla.org/en-US/
[2]: https://javascript.info/
[3]: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
[4]: https://javascript.info/xmlhttprequest
[5]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
[6]: https://javascript.info/fetch
[7]: https://developer.mozilla.org/en-US/docs/Web/API/FormData
[8]: https://javascript.info/formdata
[9]: https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment
