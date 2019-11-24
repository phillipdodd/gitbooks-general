# ESLint for Portal

## Intro

ESLint usage can save a lot of headaches if the time is taken to learn it. It is also good practice for things to come!

I will record here the things I find necessary to know when using ESLint with Portal, since it can be a bit... janky at times.

**To handle Entity Type** definitions, see **Specifying Globals**. 

**To handle methods throwing unused variable errors** see **Temporarily Disabling Rules**.

## Specifying Globals

[ESLint ](https://eslint.org/docs/user-guide/configuring)can be configured to **ignore** throwing undefined variable warnings for specific variables if they are defined as **global variables**. This can be done in two ways:

### In-File Comment

At the top of your `.js` file, include a comment that looks like this:

```javascript
/* global var1, var2*/

// or, to use flags:

/* global var1: writable, var2: readonly */
```

### .eslintrc.json File

In your `.eslinrc.json` configuration file, include the variables in the **globals** object. This method requires each to be assigned a _writable_ or _readonly_ flag.

```javascript
{
    "globals": {
        "var1": "writable",
        "var2": "readonly"
    }
}
```

{% hint style="info" %}
Adding names to this file is recommended for Portal due to the amount of **Entity Types** that will need to be defined here. ESLint usage will gradually become easier as this list grows.
{% endhint %}

## Temporarily Disabling Rules

This is important to know if for no other reason than to prevent `no-unused-vars` errors from being thrown when writing Entity Methods. There are two ways to go about this:

### ... for Single Lines

Here's the example from [their documentation](https://eslint.org/docs/user-guide/configuring). **Note** that the comments on the _same_ line use `eslint-disable-line` followed by which rules to disable, while the comments that _precede_ the line to disable include the word `next`: `es-lint-disable-next-line`

```javascript
alert('foo'); // eslint-disable-line no-alert, quotes, semi

// eslint-disable-next-line no-alert, quotes, semi
alert('foo');

alert('foo'); /* eslint-disable-line no-alert, quotes, semi */

/* eslint-disable-next-line no-alert, quotes, semi */
alert('foo');
```

{% hint style="info" %}
By not specifying **any** rules, it will disable **all** rules.
{% endhint %}

So, for writing Entity Methods, it is a simple matter of tossing a disable-next-line immediately preceding the definition:

```javascript
// eslint-disable-next-line no-unused-vars
function hasMissingItem() {
    //* do some entity shenanigans
}
```

### ... for Multiple Lines

Disabling multiple lines uses the commenting syntax `/* ... */` and requires _enabling_ eslint again after disabling it. Again, to use their example:

```javascript
/* eslint-disable no-alert, no-console */

alert('foo');
console.log('bar');

/* eslint-enable no-alert, no-console */
```

As with the Single Line disables, the which rules to ignore are specified in the comment. If none are specified, then all of them will be disabled.

