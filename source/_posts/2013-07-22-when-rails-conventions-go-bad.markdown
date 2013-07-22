---
layout: post
title: "when rails conventions go bad"
date: 2013-07-22 16:50
comments: true
categories: 
---
I was just helping a student with a crazy Rails error:

```ruby
ActiveRecord::StatementInvalid: SQLite3::ConstraintException: roles_users.created_at may not be NULL: INSERT INTO "roles_users" ("user_id", "role_id") VALUES (1, 3)
```

and it sent us down a path into Rails naming conventions.  I wanted to write this blog post mainly for myself because I always forget the naming conventions in a many to many relationship.

In Dave's app he has users and they have many roles.  He initially set up a join table, users_roles and used a has and belongs to many on both sides of the association. 

```ruby
class User

  has_and_belongs_to_many :roles

end

class Role

  has_and_belongs_to_many :users

end

```

In the console he was trying to do User.first.roles.create(:name => :instructor) which produced the above error.

The first naming convention he violated was the join table should be in alphabetical order.  The table should be called roles_users.  Now I wasn't sure why he was getting the error he was getting, why wasn't Rails generating the proper SQL to add the timestamp to the roles_users table?  I figured it probably could be fixed by just migrating to the best practice of using has_many :through.  As we moved down the has many through route I realized I could not remember the exact pluralization conventions.

Models must be singular and in alphabetical order.  The model should be

```ruby
class RoleUser

  belongs_to :role
  belongs_to :user
end
```

the table name should be plural, but only the last model in the join table should be pluralized.

role_users

the association should also pluralize only the second model
```ruby
class Role
  has_many :role_users
  has_many :users, :through => :role_users
end

class User
  has_many :role_users
  has_many :users, :through => :role_users
end