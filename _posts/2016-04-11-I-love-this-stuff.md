##The `.where` method

Active Record provides many excellent tools that allow users tointerface with a database.  Databases use a special purpose programing language called SQL (Structured Query Language) to manage their information.  Active Record (AR) takes a database information retrieval request -- or query -- made in Ruby and creates a request to the database in its native SQL.  In other words, it’s a SQL translator for Ruby.  AR allows us to communicate with the database and make these queries, through the methods in its query interface. These methods take in a variety of parameters and return an ‘association’ of an object or objects.  AR’s methods are flexible, so they can be applicable for many situations.  An excellent AR query tool is the `.where` method.

`.where` returns individual objects from a database that fit its conditions.  With `.where` you can define these conditions in several different ways to articulate however broad or specific of a query you want.  If you had a broad search request, and wanted all clients with ‘Mike’ as the value in their `first_name` field:

```ruby
Client.where(“first_name” => “Mike”)
```

AR translates this  to SQL:

```sql
SELECT "clients".* FROM "clients" WHERE "clients"."first_name" = $1  [["first_name", “Mike”]]
```

This would return an association with all ‘Clients’ with `first_name` of ‘Mike’.  This would likely return more than one object, due to the vague query using only one attribute. What if you wanted to get more specific with another condition, like returning any ‘Client’ with the `first_name` of ‘Mike’, and the `phone_number` of ‘4025555555’?  If you pass an array into the argument, then you can *add more than one conditional to the method.*  When you do this, the first ‘element’ passed sets the conditional’s keys. Following elements are the key’s corresponding values, listed in order:

```ruby
client = Client.where(["first_name = ? and phone_number = ?", "Mike", “4025555555”])```
```

The resulting SQL:
```sql
SELECT "clients".* FROM "clients" WHERE (first_name = 'Mike' and phone_number = ‘4025555555')
```

This will return an AR relation of ‘Clients’ with the `first_name` of ‘Mike’ and the `phone_number` of ‘4025555555’, which in this case would likely be an individual object.  Despite the fact that this (or any other `.where` search) may return a single object, it is still returned as a  relation and not the object itself.  This means that in order to access the attributes of the object itself, we would have to loop through it, like an array.

```ruby
client.each do |client|
client_address = client.address
end
```
To make this type of request more ‘readable’ and thus more maintainable, you could set the conditional key’s to placeholders, which are defined in a hash (the second element of the array):

```ruby
Client.where(["first_name = :name and phone_number = :number", { name: "Mike", number: "4025555555" }])
```

Results in the same SQL query:

```sql
SELECT "clients".* FROM "clients" WHERE (first_name = 'Mike' and phone_number = ‘4025555555’)
```

