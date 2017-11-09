---
title: "Realm coherency"
date: 2017-11-09T14:25:45-06:00
draft: false
---

I had a nasty bug where I was backing objects to a realm database from an iOS collection view. It would occasionally crater
when I added or deleted objects from the collection. This appears to be a race/thread issue, where the thread reading the new
collection view size from the database got the old value, rather than the new. The solution appears to be forcing a sync
on the reader threader with realm.refresh():

'let realm  = try Realm()
realm.refresh()'
