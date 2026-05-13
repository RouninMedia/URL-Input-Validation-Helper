# `<input type="url">` Validation Helper
A native HTML `<input type="url">` requires any entered value to start with a scheme in order to be valid.

This short function will automatically prepend any value with the intended scheme:

```js
const myURLInput = document.querySelector('[type="url"]');

function prependURLWithScheme (e, scheme = 'https') {
  if (e.target.getAttribute('type') === 'url') {
    e.target.value = e.target.value.replaceAll(':', '');
    e.target.value = e.target.value.replaceAll('//', '');
    e.target.value = e.target.value.replaceAll(scheme, '');
    e.target.value = `${scheme}://` + e.target.value;
  }
}

myURLInput.addEventListener('input', prependURLWithScheme);

```

____________________

## We can also remove abandoned schemes:

```js
const myURLInput = document.querySelector('[type="url"]');

const removeDetachedScheme = (e, scheme = 'https') => {
  e.target.value = (e.target.value === `${scheme}://`) ? '' : e.target.value;
}

myURLInput.addEventListener('blur', removDetachedScheme);
```
