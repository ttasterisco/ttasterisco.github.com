---
layout: post
title: MongoDB Admin Commands
summary:
---


; launch mongodb ...


<!--

; access the admin database
db = db.getSiblingDB('admin')
; authenticate with an admin account
db.auth("username", "password")

db.system.users.find()
db.system.users.update({user: "ttasterisco"}, { $set: { "roles": ["userAdminAnyDatabase", "clusterAdmin", "readWrite"]} })

show dbs

db.addUser({user:"username", pwd:"password", roles: ["readWrite"]})

-->