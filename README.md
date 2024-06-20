# kodluyoruzilkrepo
Kodluyoruz Eğitimi kapsamında açtığım ilk repo
README.md
"Building" is really just zipping. Create all archives relative to the `src` directory.

Before zipping, delete the `src/common/test` directory. This will prevent the autotests from ending up in the release.

An important preparatory step is to remove any system-generated hidden files that shouldn't be included in the release file (like Windows' `desktop.ini` and OS X's `.DS_Store`, etc.). This shell command will delete those unwanted files:

```
find . -name "desktop.ini" -or -name ".*" -and -not -name "." -and -not -name ".git*" -print0 | xargs -0 rm -rf
cd utils
node build.js
```


### Chrome and Opera extension

Create a file with a `.zip` extension containing these files and directories:
  14 changes: 14 additions & 0 deletions14  
src/common/options.js
@@ -71,6 +71,7 @@ function onLoad() {
  // Restore previously set options (asynchronously)
  //

  var optionsGetSuccessful = false;
  OptionsStore.get(function(prefs) {
    cssEdit.value = prefs['main-css'];
    cssSyntaxEdit.value = prefs['syntax-css'];
@@ -93,6 +94,8 @@ function onLoad() {

    // Start watching for changes to the styles.
    setInterval(checkChange, 100);

    optionsGetSuccessful = true;
  });

  // Load the changelist section
@@ -125,6 +128,17 @@ function onLoad() {
    }
  });

  // Older Thunderbird may try to open this options page in a new ChromeWindow, and it
  // won't work. So in that case we need to tell the user how they can actually open the
  // options page. This is pretty ungraceful, but few users will encouter it, and fewer as
  // time goes on.
  setTimeout(function() {
    if (!optionsGetSuccessful) {
      alert('It looks like you are running an older version of Thunderird.\nOpen the Markdown Here Options via the message window Tools menu.');
      window.close();
    }
  }, 500);

  loaded = true;
}
document.addEventListener('DOMContentLoaded', onLoad, false);
