# Architecture







## Basic
[CTS: Compatibility Test Suite](https://source.android.com/compatibility/cts-intro.html)

[Design](https://github.com/android/platform_frameworks_base/tree/master/docs/downloads/design)


Data area stack
 * stack over flow
 * out of memory

Heap: only out of memory

Method area: const, string


### Telephony
telephony.db
 * SMS & MMS & APN


## Four Components

### Service

AIDL
 * A.aidl
 * Implement A.stub
 * in Service.onBind, return binder



### Activity

Fragemnt lifecycle

Layout

View
 * ListView, TextView, Button
 * Tab, ActionBar
 * Menu


### Receiver

Sticky

Pending intent



### Content Provider

SQL, Cursor, ContentResolver



