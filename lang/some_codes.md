# Android development


2014-12-01 Mon
1. [Hide keyboard](http://stackoverflow.com/questions/1109022/close-hide-the-android-soft-keyboard)
```
InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
imm.hideSoftInputFromWindow(mEditText.getWindowToken(), 0);
```
