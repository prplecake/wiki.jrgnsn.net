`CATALINA_HOME\webapps\ROOT` is the default webapp containing the default administrator's index page. It's possible that issues can arise by renaming your webapp to ROOT, so a better method is to simply redirect to your other app.

This can be accomplished by creating an **index.html** inside `$CATALINA_HOME\webapps\ROOT`.
You don't need to remove the index.jsp that's at that location, index.html will override it.

`index.html`:

```html
<html>
<head>
	<meta http-equiv="refresh" content="0;URL=https://REDIRECT/TO/PATH/" />
</head>
<body></body>
</html>
```

For example, to redirect example.com/ to /blog, the `<meta>`` tag would look like this:

```html
<meta http-equiv="refresh" content="0;URL=/blog" />
```
